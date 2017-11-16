## Running Multiple Instances Per Host To Improve Performance

You may find that Rocket.Chat slows down once you have a lot of concurrent users. When this sluggishness begins,
you will likely see Rocket.Chat node process approaching 100% CPU (even if the host CPU load is low). This is
due to the single-threaded nature of Node.js applications; they can't take advantage of multiple cores natively.

While its possible to scale out by adding more servers (and this is recommended for HA purposes), you can achieve
better utilization of your existing hardware by running multiple instances of the Rocket.Chat application
(Node.js/Meteor app) on your current host(s). Of course, you only want to do this if you're already running on
a multi-core machine. A reasonable rule-of-thumb may be to run `N-1` Rocket.Chat instances, where `N=num_cores`.

Running multiple instances of Rocket.Chat on a single host requires a reverse proxy in front of your application.
This tutorial assumes that you've already followed the tutorial for [Running behind a Nginx SSL Reverse Proxy](https://rocket.chat/docs/installation/manual-installation/configuring-ssl-reverse-proxy).

There's essentially just three steps:
  1. Enable ReplicaSet on your MongoDB installation (https://docs.mongodb.com/manual/tutorial/deploy-replica-set/)
  2. Start multiple instances of Rocket.Chat bound to different ports
  3. Update your proxy to point at all local Rocket.Chat instances

We'll be working with Nginx in our examples, but it should be possible with other reverse proxies as well.

## Run multiple instances of Rocket.Chat

We'll assume that you've configured Rocket.Chat to run as a systemd service. Since we want to run multiple instances
simultaneously, we need to run at least two services. The only difference is the service name and port.
If you don't have a service yet, the easiest way to do this for Rocket.Chat is to create a file in /usr/lib/systemd/system/
and call it rocketchat.service
```
[Unit]
Description=Rocket.Chat Server
After=syslog.target
After=network.target

[Service]
Type=simple
Restart=always
StandardOutput=syslog
SyslogIdentifier=RocketChat
User=rocketchat
Group=rocketchat
Environment=MONGO_URL=mongodb://your_mongodb:27017/your_database?replicaSet=your_replica_set_name
Environment=MONGO_OPLOG_URL=mongodb://your_mongodb1:27017/local?replicaSet=your_replica_set_name
Environment=ROOT_URL=https://your_rocketchat_domain.com
Environment=PORT=3000
WorkingDirectory=/path.to.rocketchat/rocket.chat
ExecStart=/usr/local/bin/node /path.to.rocketchat/rocket.chat/bundle/main.js

[Install]
WantedBy=multi-user.target
```
Make sure the User and Group exist and both have read/write/execute Permissions for the rocketchat.
Now you can run start, stop, restart, and status your rocketchat service.

If you want multiple Services create another file in /usr/lib/systemd/system and call it rocketchat@.service with the following content:
```
[Unit]
Description=Rocket.Chat Server
After=syslog.target
After=network.target

[Service]
Type=simple
Restart=always
StandardOutput=syslog
SyslogIdentifier=RocketChat
User=rocketchat
Group=rocketchat
Environment=MONGO_URL=mongodb://your_mongodb:27017/your_database?replicaSet=your_replica_set_name
Environment=MONGO_OPLOG_URL=mongodb://your_mongodb1:27017/local?replicaSet=your_replica_set_name
Environment=ROOT_URL=https://your_rocketchat_domain.com
Environment=PORT=%I
WorkingDirectory=/path.to.rocketchat/rocket.chat
ExecStart=/usr/local/bin/node /path.to.rocketchat/rocket.chat/bundle/main.js

[Install]
WantedBy=rocketchat.service
```
Start the other RocketChat Services with

    systemctl start rocketchat@3001 (or any other desired port after the @)

If you want to run rocketchat at boot just enable the services with

    systemctl enable rocketchat

The other Services will be enable since they are "WantedBy"=RocketChat.service

## Update your Nginx proxy config

Edit ```/etc/nginx/sites-enabled/default``` or if you use nginx from docker ```/etc/nginx/conf.d/default.conf```
and be sure to use your actual hostname in lieu of the sample hostname "your_hostname.com" below.

You just need to setup a backend if one doesn't already exist. Add all local Rocket.Chat instances to it.
Then swap out the host listed in the proxy section for the backend you defined with no port.

Continuing the example, we'll update our Nginx config to point to the two Rocket.Chat instances
that we started running on ports 3001 and 3002.

```
# Upstreams
upstream backend {
    server 127.0.0.1:3000;
    server 127.0.0.1:3001;
    #server 127.0.0.1:3002;
    #server 127.0.0.1:3003;
    .
    .
    .
}
```

Now just replace `proxy_pass http://IP:3000/;` with `proxy_pass http://backend;`.
Updating the [sample Nginx configuration](https://rocket.chat/docs/installation/manual-installation/configuring-ssl-reverse-proxy#running-behind-a-nginx-ssl-reverse-proxy)
would result in a config like this:

```
# HTTPS Server
server {
    listen 443;
    server_name your_hostname.com;

    error_log /var/log/nginx/rocketchat.access.log;

    ssl on;
    ssl_certificate /etc/nginx/certificate.crt;
    ssl_certificate_key /etc/nginx/certificate.key;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # don’t use SSLv3 ref: POODLE

    location / {
        proxy_pass http://backend;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $http_host;

        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forward-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forward-Proto http;
        proxy_set_header X-Nginx-Proxy true;

        proxy_redirect off;
    }
}
```

Now restart Nginx: ```service nginx restart```

Visit https://your_hostname.com just as before the update. **Ooh, so fast!**

To confirm you're actually using both services like you'd expect, you can stop one rocketchat
service at a time and confirm that chat still works. Restart that service and stop the other.
Still work? Yep, you're using both services!
