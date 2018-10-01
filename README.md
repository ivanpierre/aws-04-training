# aws-04-training
Project to test various possibilities of AWS deployment with a PWA app with servers

## Goals
Every piece of the whole app can be deployed in various way through AWS or in-premices. The goal is to keep code unique and only manage the deployment to obtain the desired configuration.

Deployment procedures should be created to make the correct works for each. It can be through Docker, Launch template or `cli` shells.

Two deployment for each case should be available. 
  * Developpement. With all access to all dev tools as REPL, editors, ssh, compilers, BD access, for all element of the app.
  * Production. With complete lock of undue access.

Both should evidently have crypted communication, if possible.

Normally all AWS modules for the training should be used.

## Structure of apps

Clojure and ClojureScripts are the language of choice as code can be compiled to both generate JavaScript code and JVM code for various implementations of the server part, or to choose how to serve client part.

### Client part

According to Henrik Joreteg, _“PWA is the single biggest thing to happen on the mobile web since Steve introduced the iPhone!”_

It's a [Progressive Web App](https://developers.google.com/web/progressive-web-apps/) 

Writen in ClojureScript and compiled in JavaScript. It should work on all premises (Windows, OCX, Linux, iOS, Android) and should be installable with Chrome, FireFox. Support for Opera, 

It will contain various parts :

#### A [Single Page Application](https://developers.google.com/web/progressive-web-apps/).
Witch should communicate in HTTPS:.

In development mode figweel is lauched by the app and nREPL communicate on a fixed port. Beware Security Groups and ACLs.
#### A [Service Worker](https://developers.google.com/web/fundamentals/primers/service-workers/).
  * To get the push notifications from servers
  * To cache and synchronize server data
  * To get SPA updates

In development mode nREPL communicate on a fixed port.
#### An optional server
If server is on-premises and on the client in the worker, this will be configured by environment for compilation. Production code will delete unused code, so it will not unusefully put in the package if not necessary.

The server code will be the same as the JVM one as we can compile both. The only warning is in the libraries used to fullfil the tasks (dual compilation).

### Server part
This will dispatch api call to access DB, PLUs, Images, ... And to update these even locally and cached or directly to servers. 

In case there is no Internet connection, the worker will use the cache or stored data created by the application before a new connection updates the server with local new data.

Various interfaces will be written for each accesses according to configuration. Call will be defined by project.clj file witch will use the correct entry point for server launch.

## Implementation

Client and Server apps are currently here:

  * https://github.com/ivanpierre/portable-pos-client
  * https://github.com/ivanpierre/portable-pos-server

It's for now a WIP (work in progress) see RELEASE-NOTES.md for information of the state in every git repositories.
