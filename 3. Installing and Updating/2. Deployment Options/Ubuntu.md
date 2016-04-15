# Deploying Rocket.Chat on Ubuntu

This guide explains how to deploy your own Rocket.Chat instance to a Ubuntu Linux machine using the command line.

## 1. Install Dependencies

- `Node.js`
- `MongoDB`
- `curl`
- `graphicsmagick`

```shell
# SYSTEM CONFIGURATION
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org curl graphicsmagick

# We have to also install `npm`, which is the Node.js package manager. You can do this by typing:
sudo apt-get install npm

# If you encountered some errors when trying to install npm
# try to install nodejs in the first place.
# The nodejs package contains the nodejs binary as well as npm, so you don't need to install npm separately.
sudo apt-get install nodejs

# OR
# An alternative that can get you a more recent version of Node.js is to add a PPA maintained by NodeSource
curl -sL https://deb.nodesource.com/setup | sudo bash -
# After running the setup script from nodesource, you can install the Node.js package
# in the same way that you did above
sudo apt-get install nodejs
# In order for some npm packages to work (such as those that require building from source)
# you will need to install the build-essentials package:
sudo apt-get install build-essential
# for more please view the link below.





# Install a tool to let us change the node version.
sudo npm install -g n

# Meteor needs at least this version of node to work.
sudo n 0.10.40
```

More on [nodejs installation](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-an-ubuntu-14-04-server)


## 2. Install Rocket.Chat

Download Stable version of Rocket.Chat (or pick a version from [our releases page](https://rocket.chat/releases)):

```
curl -L https://rocket.chat/releases/latest/download -o rocket.chat.tgz
```

Then untar the binary release:

```
tar zxvf rocket.chat.tgz
```

this will expand everything into a `bundle` directory.

Next, make sure MongoDB server is already up and running.  Then, set environment variables and run the Rocket.Chat server:

```
mv bundle Rocket.Chat
cd Rocket.Chat/programs/server
npm install
cd ../..

export ROOT_URL=http://your-host-name.com-as-accessed-from-internet:3000/
export MONGO_URL=mongodb://localhost:27017/rocketchat
export PORT=3000

node main.js
```
You **MUST** set the `ROOT_URL` environment variable to the Internet accessible URL to your server.

This will start the Rocket.Chat server running.

If you would like to start Rocket.Chat on an alternative port, use the environment variable PORT.

**Note: If using port 80 you will have to run as root.  This is because it is a privileged port.**

If you choose to do this.  You need to do something like this:
```
sudo ROOT_URL=http://your-host-name.com-as-accessed-from-internet/ \
    MONGO_URL=mongodb://localhost:27017/rocketchat \
    PORT=80 \
    node main.js

# Or...
sudo su
export ROOT_URL=http://your-host-name.com-as-accessed-from-internet/
export MONGO_URL=mongodb://localhost:27017/rocketchat
export PORT=80

node main.js
```

NOTE:  If you need to keep the server up and running across reboots, use a task manager such as forever, PM2 or write your own shell management scripts.

## 3. Setup MongoDB Replica Set

Rocket.Chat uses the [MongoDB replica set](http://docs.mongodb.org/manual/replication/) **OPTIONALLY** to improve performance via Meteor Oplog tailing.  To configure the replica set:

#### For older MongoDB versions (2.4 and bellow)

Append `replSet=001-rs` into `mongod.conf` file:

```shell
$ echo replSet=001-rs >> /etc/mongod.conf
```

And restart Mongo:

```shell
$ service mongod restart
$ mongo
```

#### For new MongoDB versions (2.6 and above)

Using YAML syntax add this section into `mongod.conf`:

```
replication:
      replSetName:  "001-rs"
```

Restart Mongo:

```shell
$ service mongod restart
$ mongo
```

Start the MongoDB shell and initiate the replica set:

```shell
$ mongo
> rs.initiate()
```

The result should look like this

```
{
  "info2" : "no configuration explicitly specified -- making one",
  "me" : "localhost:27017",
  "info" : "Config now saved locally.  Should come online in about a minute.",
  "ok" : 1
}
```

After a few seconds, you should see your prompt turn into `001-rs:PRIMARY> `, this indicates the replica set is being used. Type `exit` to get back to your regular shell.

After you configured replica set, you **MUST** add the following environment variable before restarting Rocket.Chat server for it to take effect:

```
MONGO_OPLOG_URL=mongodb://localhost:27017/local
```


## 4. Configure Rocket.Chat

Rocket.Chat is installed and needs to be configured. Follow these guides to properly configure everything your instance needs:

1. [Creating the First Admin](server-management-create-the-first-admin)
2. [Run Rocket.Chat behind a SSL Reverse Proxy](installing-and-updating-4-configuring-ssl-reverse-proxy-with-nginx)

## 5. Update an already installed instance

In summary do the following:

1. Make sure server is down
1. Change into the directory where you have the `Rocket.Chat` directory
1. remove the old server executables
  * `rm -rf Rocket.Chat`
1. Repeat Installation [step](#2-install-rocketchat)

You can always [update directly](https://github.com/RocketChat/Rocket.Chat/issues/2408) to the newest version, the database migrations will execute from the old version to the new version.
