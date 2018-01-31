# Documentation Status Map

This is a map of all of the Rocket.Chat Documentation articles

Here you can also find what articles are incomplete and missing.

<span style="color:red">Red Colored Text</span> means that this article is missing from the documentation and need to be added.

<span style="color:orange">Orange Colored Text</span> means that this article is in the documentation but is incomplete or outdated.

<style>

  span.missing {
        color: red;
  }

  span.missing a {
        color: red;
  }

  span.incomplete {
      color: orange;
  }

  span.incomplete a {
        color: orange;
  }

</style>

- Contributing
    - Developing
    - Google Summer of Code
    - Promoting
    - Reporting Issues
    - Security:
        - Responsible Disclosure Policy
    - Translating
- Getting Support
- Installation:

    - Rocket.Chat Cloud
    - PaaS Deployments:
        - Aliyun
        - AWS
        - Cloudron.io
        - Digital Ocean
        - DPlatform
        - Galaxy
        - Google Computer Engine
        - Heroku
        - Hyper.sh
        - IBM Bluemix
        - IndieHosters
        - Koozali
        - Layershift
        - OpenShift
        - ReadySpace
        - Sandstorm.io
        - Scalingo
        - Sloppy.io
        - WeDeploy
    - Docker containers:
        - Generic Linux
        - systemd
        - Available Images
        - Docker Compose
    - Manual Installation:

        - CentOS
        - Debian
        - FreeBSD:
        - Universal
        - MacOSX
        - Multiple Instances to Improve Performance
        - OpenSUSE
        - <span class="incomplete">[RedHat](../missing-and-outdated-list/index.html#redhat)</span>

        - Ubuntu:
            - Snaps:
                - AutoSSl
        - Windows 10 Pro
        - Windows Server:
            - <span class="incomplete">[Releases](../missing-and-outdated-list/index.html#releases)</span>
        - Configuring SSL Reverse Proxy
        - PM2, Systemd, Upstart
        - Running in a sub folder

    - Automation tools:
        - Ansible
        - Openshift
        - Vagrant
    - Mobile and Desktop Apps
    - <span class="incomplete">[Updating](../missing-and-outdated-list/index.html#updating)</span>
        - From 0.x.x to 0.40.0
    - Minimum Requirements

- User guides:
    - Connecting to a Server
    - Registration
    - Login
    - Channels
    - Messaging
    - Channel Actions
    - Managing your Account
    - <span class="incomplete">[Voice and Video Calls](../missing-and-outdated-list/index.html#voice-and-video-calls)</span>
    - <span class="missing">[ScreenSharing](../missing-and-outdated-list/index.html#screensharing)</span>
- Administrator guides:
    - Account Settings
    - <span class="missing">[Analytics](../missing-and-outdated-list/index.html#analytics)</span>
    - Authentication:
        - CAS
        - Ldap
        - <span class="incomplete">[Oauth](../missing-and-outdated-list/index.html#oauth)</span>
        - SAML
        - <span class="missing">[WordPress](../missing-and-outdated-list/index.html#WordPress)</span>
    - <span class="missing">[Customizing the UI](../missing-and-outdated-list/index.html#Customizing-the-UI)</span>:
        - <span class="missing">[Layout](../missing-and-outdated-list/index.html#Layout)</span>
        - <span class="missing">[Assets](../missing-and-outdated-list/index.html#Assets)</span>
    - Database-Migration
    - Email:
        - Setup
        - Editing Emails Content
        - Mailer
        - Direct Reply
    - File Upload:
        - Amazon S3
        - Minio
        - <span class="missing">[GridFS](../missing-and-outdated-list/index.html#GridFS)</span>
        - <span class="missing">[Local File System](../missing-and-outdated-list/index.html#Local-File-System)</span>
    - <span class="missing">[General Settings](../missing-and-outdated-list/index.html#General-Settings)</span>
        - <span class="missing">[General Section](../missing-and-outdated-list/index.html#General-Section)</span>
        - <span class="missing">[Message Section](../missing-and-outdated-list/index.html#Message-Section)</span>
    - Hubot
    - Import:
        - CSV
        - HipChat:
            - <span class="incomplete">[Cloud](../missing-and-outdated-list/index.html#hipchat-cloud)</span>
            - Enterprise
        - Slack:
            - SlackBridge
    - Integrations:
        - Zapier:
            - Using Zaps
        - Azure Alerts
        - BitBucket
        - Giphy
        - GitHub
        - GitLab
        - Google-Calendar
        - Guggy
        - Jenkins
        - Jira
        - NewRelic
        - nixstats
        - Osticket
        - PagerDuty
        - Prometheus
        - ReplyGif
        - ReviewBoard
        - RunDeck
        - Sentry
        - Telegram
        - Travis CI
        - Trello
        - uptimerobot
    - <span class="missing">[Internal Hubot](../missing-and-outdated-list/index.html#Internal-Hubot)</span>
    - Jitsi Video Bridge
    - Livechat:
        - Livechat Queues
    - Notifications:
        - Push Notifications
    - <span class="incomplete">[Permissions](../missing-and-outdated-list/index.html#Permissions)</span>
    - Plug-ins:
        - Drupal
        - Pidgin
    - Create the First Admin
- Developer guides:
    - Quick Start
    - Branches and Releases
    - Code Styleguide:
        - <span class="incomplete">[Less](../missing-and-outdated-list/index.html#Less)</span>
    - Iframe Integration:
        - <span class="missing">[Authentication](../missing-and-outdated-list/index.html#Authentication)</span>
        - Commands
        - Events
    - <span class="missing">[Internationalization](../missing-and-outdated-list/index.html#Internationalization)</span>
    - Livechat API
    - Mobile Apps
    - Realtime-API:
        - Method Calls:
            - Login
            - Logout
            - Register User
            - Get User Roles
            - List Custom Emoji
            - Load History
            - Get Room Roles
            - Get Subscriptions
            - Get Rooms
            - Get Public Settings
            - Get Permissions
            - User Presence
            - Notify Room Stream
            - Send Message
            - Delete Message
            - Update Message
            - Pin Message
            - Unpin Message
            - Set Reaction
            - Create Channels
            - Create Private Groups
            - Delete Rooms
            - Archive Rooms
            - Unarchive Rooms
            - Joining Channels
            - Leaving Rooms
            - Hiding Rooms
            - Opening Rooms
            - Favoriting Rooms
            - Save Room Settings
        - Subscriptions:
            - Stream Notify All
            - Stream Notify User
            - Stream Notify Room
            - Stream Room Messages
        - The Message Object
        - The Room Object
        - Livechat API:
            - getInitialData
            - registerGuest
            - sendMessageLivechat
            - sendOfflineMessage
        - Rest API:
        - Authentication:
            - login
            - logout
            - me
        - Channels:
            - addAll
            - addModerator
            - addOwner
            - archive
            - cleanHistory
            - close
            - create
            - getIntegrations
            - history
            - info
            - invite
            - kick
            - leave
            - list.joined
            - list
            - open
            - removeModerator
            - removeOwner
            - rename
            - setDescription
            - setJoinCode
            - setPurpose
            - setReadOnly
            - SetTopic
            - setType
            - unarchive
        - Chat:
            - delete
            - getMessage
            - pinMessage
            - postMessage
            - react
            - starMessage
            - unPinMessage
            - unStarMessage
            - update
        - Commands:
            - get
            - list
            - run
        - Groups:
            - addAll
            - addModerator
            - addOwner
            - archive
            - close
            - create
            - getIntegrations
            - history
            - info
            - invite
            - kick
            - leave
            - list
            - open
            - removeModerator
            - removeOwner
            - rename
            - setDescription
            - setPurpose
            - setReadOnly
            - SetTopic
            - setType
            - unarchive
        - Im:
            - close
            - history
            - list.everyone
            - list
            - messages.others
            - open
            - setTopic
        - Integration:
            - create
            - list
            - remove
        - Livechat:
            - department
            - sms-incoming
            - users
        - Miscellaneous:
            - info
        - Settings:
            - get
            - update
        - Users:
            - create
            - createToken
            - delete
            - getAvatar
            - getPresence
            - info
            - list
            - register
            - resetAvatar
            - setAvatar
            - update
        - Offset and Count and Sort Info
        - Query and Fields Info
        - <span class="incomplete">[Schema Definition](../missing-and-outdated-list#Schema-Definition)</span>
        - <span class="incomplete">[Testing](../missing-and-outdated-list#Testing)</span>
        - Troubleshooting
        - UI and Theming:
        - Colors
        - Components
        - Themes
- Community Cookbook:
    - Remote Video Monitoring
