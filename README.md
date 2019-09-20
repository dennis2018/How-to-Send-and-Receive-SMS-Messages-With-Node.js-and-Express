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

## Send the SMS Message
The Nexmo library has a method for sending the SMS with the SMS API, and that’s nexmo.message.sendSms. The method takes as parameters 3 strings and an object: the Nexmo number from which to send the SMS, the phone number where to deliver the SMS, the text of the message and options for the SMS encoding. It also accepts a callback that gets called when the API request is done.

The response data contains an array for all the messages that were sent, with information about their status. In most cases, it’s going to be 1 element in that array, but if the SMS was longer than 160 characters, it gets split into a multipart SMS, and then the array contains data about each part sent. If the status of the message is 0, the SMS was sent successfully, otherwise, the error data for the message is on the error-text property of the message.

Because my text has an emoji in it, I’m setting the type unicode in the options object, otherwise, that emoji is going to be sent on the network as ?.

```
let text = "👋Hello from Nexmo";
 
nexmo.message.sendSms("Nexmo", "TO_NUMBER", text, {
  type: "unicode"
}, (err, responseData) => {
  if (err) {
    console.log(err);
  } else {
    if (responseData.messages[0]['status'] === "0") {
      console.log("Message sent successfully.");
    } else {
      console.log(`Message failed with error: ${responseData.messages[0]['error-text']}`);
    }
  }
})

```

If your carrier network supports alphanumeric sender IDs, FROM can be text instead of a phone number(for my example it’s DENNISMBURUTECH. If your network doesn’t support alphanumeric sender IDs (for example in the US) it has to be a phone number.

Depending on the country you’re trying to send the SMS to, there are regulations that require you to own the phone number you’re sending the SMS from, so you’ll have to buy a Nexmo phone number. You can do so in the Nexmo Dashboard or via the CLI:

```
 $ nexmo number:buy  --country_code US --confirm
```

You can run the code and receive the SMS message with:

```
$ node index.js
```

## Send an SMS Message With the New Messages API

There is a newer Nexmo API that deals with sending text messages called the Messages API. It is a multi-channel API, that can send a message via different channels, such as SMS, Facebook Messenger, Viber, and Whatsapp. The API is in Beta right now, so if we want to use it to send the same SMS message, we’ll need to install the beta version of the Nexmo node library.

```
$ npm install nexmo@beta
```

## Run ngrok

If you haven’t used ngrok before, there is a blog post that explains how to use it. If you’re familiar with ngrok, run it with http on the 3000 port.

