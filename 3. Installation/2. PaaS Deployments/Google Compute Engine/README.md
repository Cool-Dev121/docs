# Deploying Rocket.Chat on Google Compute Engine

1. Create a compute instance with a linux image (i.e the default debian)

2. SSH to the instance

3. run the following to install docker:
    `sudo wget -qO- https://get.docker.com/ | sh`

4. install a docker image for mongo db
   `sudo docker run --name db -d mongo --smallfiles`

5. install a docker image for rocketchat and connect it to mongodb. `ROOT:URL` should be substituted your own:

   `sudo docker run --name rocketchat -p 80:80 --env ROOT_URL=https://www.test.com --env MONGO_URL=mongodb://db/meteor --link db -d rocketchat/rocket.chat`

   You are now runing rocket chat on compute engine. You can open a browser with the external IP of the instance.

If you want the containers to start each time the instance reboots configure the following to the instance.

* click on the instance in the and hit "edit"
* Under "Custom metadata" add an item with
```
key: "startup-script"
value "sudo docker start db
sudo docker start rocketchat"
```

