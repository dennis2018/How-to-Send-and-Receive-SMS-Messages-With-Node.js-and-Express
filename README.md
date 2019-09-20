# How-to-Send-and-Receive-SMS-Messages-With-Node.js-and-Express

[![GitHub Issues](https://img.shields.io/github/issues/IgorAntun/node-chat.svg)](https://github.com/dennis2018/How-to-Send-and-Receive-SMS-Messages-With-Node.js-and-Express/network/alerts) [![Current Version](https://img.shields.io/badge/version-1.0.7-green.svg)](https://github.com/IgorAntun/node-chat) 

### This series originally appeared on the Nexmo blog, but I wanted to add some more content to it especially for the DENNISMBURUTECH community.

Nexmo has a couple of APIs that allow you to send and receive a high volume of SMS anywhere in the world. Once you get your virtual phone number, you can use the APIs to manage outbound messages (“sending”) and inbound messages (“receiving”). In this article, you will learn how to send and receive SMS messages with Node.js and Express.

We will first send an SMS with Node.js and the old SMS API (Nexmo’s first API) and then rewrite that code to use the new Messages API to send the same SMS. We’ll then build a Webhook that can receive SMS messages using express. We’ll focus in this PART on sending and receiving SMS messages, but if you want to send and receive messages with Facebook Messenger, Viber or Whatsapp, you can do that as well with the Messages API.

## Prerequisites 
Before you begin, make sure you have:
- A Nexmo account
- Node.js installed on your machine
- ngrok to make the code on our local machine accessible to the outside world
- The Nexmo CLI: ``` npm install -g nexmo-cli ```

## Send an SMS Message With the SMS API

The SMS API is the first Nexmo API, and we’ll use it to send an SMS message to your phone number.

## Install Node.js Dependencies

First off, initialize an NPM package, otherwise, older versions of NPM will complain about installing a package without having a package.json first. Just use the defaults for init, and then install the nexmo Node.js package.

```
$ npm init
$ npm install nexmo

```

## Initialize Dependencies

We’ll create a new JavaScript file, let’s call it index.js.

```
$ touch index.js

```

We need to initialize the Nexmo node library we installed earlier, in the index.js file you created:

```
const Nexmo = require('nexmo')
 
const nexmo = new Nexmo({
  apiKey: NEXMO_API_KEY,
  apiSecret: NEXMO_API_SECRET
})
```

Replace the values in there with your actual API key and secret. You can find those on the “Getting Started” page in the Nexmo Dashboard.
