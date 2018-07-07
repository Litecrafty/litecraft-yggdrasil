# Litecraft Node.js yggdrasil
[![Build Status](https://travis-ci.org/Litecrafty/litecraft-yggdrasil.svg?branch=master)](https://travis-ci.org/Litecrafty/litecraft-yggdrasil)
[![npm](https://img.shields.io/npm/v/litecraft-yggdrasil.svg)](https://www.npmjs.com/package/litecraft-yggdrasil)
[![npm](https://img.shields.io/npm/dy/litecraft-yggdrasil.svg)](https://www.npmjs.com/package/litecraft-yggdrasil)

A Node.js client for doing requests to yggdrasil, the Mojang authentication system, used for Minecraft and Scrolls.

# Usage
    $ npm install litecraft-yggdrasil

## Client
```js
//init
const ygg = require('litecraft-yggdrasil')({
  //Optional settings object
  host: 'https://authserver.mojang.com' //Optional custom host. No trailing slash.
});

//Authenticate a user
ygg.auth({
  token: '', //Optional. Client token.
  agent: '', //Agent name. Defaults to 'Minecraft'
  version: 1, //Agent version. Defaults to 1
  user: '', //Username
  pass: '' //Password
}, function(err, data) {});

//Refresh an accessToken
ygg.refresh(oldtoken, clienttoken, function(err, newtoken, response body){});

//Validate an accessToken
ygg.validate(token, function(isValid){});

//Invalidate all accessTokens
ygg.signout(username, password, function(err));
```

## Server
```js
const yggserver = require('yggdrasil').server({
  //Optional settings object
  host: 'https://authserver.mojang.com' //Optional custom host. No trailing slash.
});

//Join a server (clientside)
yggserver.join(token, profile, serverid, sharedsecret, serverkey, function(err, response body){});

//Join a server (serverside)
yggserver.hasJoined(username, serverid, sharedsecret, serverkey, function(err, client info){});
```

## With ES6 Named Exports
```js
/**
 * Import Client or Server from 'yggdrasil/es6'.
 * Note that the library is stateless when imported this way vs the CommonJS way.
 */
import { Client as ygg, Server as yggServ } from 'yggdrasil/es6'

// Use it like you normally would.

ygg.validate(token, function(isValid){})

yggServ.join(token, profile, serverid, sharedsecret, serverkey, function(err, response body){});
```

# See also
* [Authentication protocol documentation](http://wiki.vg/Authentication)
