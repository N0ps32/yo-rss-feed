Yo RSS Feed
===========

About
-----

Yo RSS feed is the framework used by the following YO "services"
*  SATWYO (Sends you a YO every time a new SATW comic is published)
*  XKCDINFO (Sends you a YO every time a new XKCD comic is published
    
You can use it to create your own YO services that can digest RSS feeds and
inform subscribed users about content updates.

The default behaviour is that the specified RSS feed is parsed and the first article link
is written into a cache-file. Every time the server detects a new link all subscribed users will be
notified. If a user sends a YO to your service the latest cached link will be returned.

Installation
------------

Clone the code into a folder on your computer.
Now create a file called config.json in the folder to configure the script.

Full configuration example:

    {
        "api-key": "",
        "update-interval": "120", //minutes
        "feed-url": "http://feeds.feedburner.com/satwcomic",
        "cache-file": "/home/sampleuser/app/application.cache",
        "http": {
            "port": 30000,
            "endpoint": "/webhook"
        }
    }

If you don't specify an option the default value will be used.
The default cache-file will be created in the same folder as the "App.js" script and will be named "application.cache".

The application will start an HTTP server on your computer when you run the script to receive webhook callbacks from YO.
It is recommended to change the endpoint to a random value like "/webhook/3B1D46D9A30B190".

**Everybody who knows your endpoint URL can send YO messages to your users. Make sure to keep it secret!**

Now enter your API key into the configuration file and configure the Callback URL in the YO dashboard to point to your
servers secret callback endpoint.

Finally run

    npm install

in your folder to install all needed dependencies.


You can run the script by executing

    node App.js
    
in your folder. Please note that the script will not start itself as a daemon if you want that you can use
something like pm2 to start the script.

Tests
-----

To run the included unit tests and lint the project run

    grunt
    
in the project folder. Note that you need to install the dev-dependencies and have grunt-cli installed on your system.
