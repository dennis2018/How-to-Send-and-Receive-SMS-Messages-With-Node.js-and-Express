# How-to-Send-and-Receive-SMS-Messages-With-Node.js-and-Express

[![GitHub Stars](https://img.shields.io/github/stars/IgorAntun/node-chat.svg)](https://github.com/IgorAntun/node-chat/stargazers) [![GitHub Issues](https://img.shields.io/github/issues/IgorAntun/node-chat.svg)](https://github.com/IgorAntun/node-chat/issues) [![Current Version](https://img.shields.io/badge/version-1.0.7-green.svg)](https://github.com/IgorAntun/node-chat) [![Live Demo](https://img.shields.io/badge/demo-online-green.svg)](https://igorantun.com/chat) [![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/IgorAntun/node-chat?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

### This article originally appeared on the Nexmo blog, but I wanted to add some more content to it especially for the DENNISMBURUTECH community.

Nexmo has a couple of APIs that allow you to send and receive a high volume of SMS anywhere in the world. Once you get your virtual phone number, you can use the APIs to manage outbound messages (“sending”) and inbound messages (“receiving”). In this article, you will learn how to send and receive SMS messages with Node.js and Express.

We will first send an SMS with Node.js and the old SMS API (Nexmo’s first API) and then rewrite that code to use the new Messages API to send the same SMS. We’ll then build a Webhook that can receive SMS messages using express. We’ll focus in this PART on sending and receiving SMS messages, but if you want to send and receive messages with Facebook Messenger, Viber or Whatsapp, you can do that as well with the Messages API.

## Prerequisites 
Before you begin, make sure you have:
- A Nexmo account
- Node.js installed on your machine
- ngrok to make the code on our local machine accessible to the outside world
- The Nexmo CLI: ``` npm install -g nexmo-cli ```
