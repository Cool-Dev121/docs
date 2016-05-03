# Docker Compose

Instead of using the standard Docker commands, you may wish for a bit more automated management of the deployment. This is where the use of Docker-compose may come in handy. Note: as stated by Docker, docker-compose is [not yet recommended for production use](https://docs.docker.com/compose/production/) at this time.

* Make sure you have [Docker](https://docs.docker.com/engine/installation/) and [Docker-compose](https://docs.docker.com/compose/install/) installed and operational.
* Create `docker-compose.yml` based on [our example](https://raw.githubusercontent.com/RocketChat/Rocket.Chat/develop/docker-compose.yml).  This is the ONLY file you will need.  You can create this file on your own machine by copy and pasting the content.
* Edit `image: rocketchat/rocket.chat:develop` to specify which image you wish to use (see section [Docker Images Available](https://github.com/RocketChat/Rocket.Chat.Docs/blob/master/content/Deployment/docker%20images%20available.md) )
* Edit `ROOT_URL` to match your domain name or IP address

Start the mongodb server by:

```
docker-compose up -d mongo
```

Mongo supports 24 x 7 operations and live backup.  You should not need to restart it too frequently.  See  [mongodb documentations](https://docs.mongodb.org/manual/) for proper operation and management of a mongo server.

Once you're sure that mongodb is up and running:

```
docker-compose up -d rocketchat
```

Optionally, if you want to manage your messages and configuration information, edit the file again to uncomment the volume mounts.   Make sure you have a `data` subdirectory to mount and store the data.

Optiionally, if you want a bot, so you don't have to talk to yourself, after you've created an admin user and also a bot user, edit the file `docker-compose.yml` again to change the variables `ROCKETCHAT_USER` and `ROCKETCHAT_PASSWORD` in the hubot section and then start up hubot:

```
docker-compose up -d hubot
```

To update the `rocketchat` docker image to the latest version, you can use the following commands. Your data should not be affected by this, since it's located in the `mongo` image.

```
docker pull rocketchat/rocket.chat:develop
docker-compose stop rocketchat
docker-compose rm rocketchat
docker-compose up -d rocketchat
```
