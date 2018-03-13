---
title: Overview
---

# Messages Overview [Developer Preview]

The Messaging API is a single API that enables easy integration with various communication channels such as: SMS, Facebook Messenger and Viber.

This API is currently in Developer Preview and you will need to [request access](https://www.nexmo.com/products/messages) to use it.

During Developer Preview we will expand the capabilities of the API. Please visit the API Reference for a comprehensive breakdown and on high level we currently support:

* Outbound text messages on SMS, Viber Service Messages and Facebook Messenger.
* Outbound media messages on Facebook Messenger.
* Inbound text, media and location messages on Facebook Messenger.

There may be bugs🐛 and quirks so we'd welcome your feedback - any suggestions you make help us shape the product. If you do need help, please email [support@nexmo.com](mailto:support@nexmo.com) and include Messages API in the subject line.

## Contents

In this document you can learn about:

* [Concepts](#concepts)
* [How to Get Started with Olympus](#getting-started)
* [Building Blocks](#building-blocks)
* [Guides](#guides)
* [Reference](#reference)

## Concepts

To use the Messages API, you may need to familiarise yourself with:

* **[Authentication](/concepts/guides/authentication)** - The Messages API is authenticated with JWT.
* **[Workflows](/olympus/workflows/overview)** - The Workflow API is used to combine messages together with logic to allow for failover.

## Getting Started

In this Getting Started section we will show you how you can send an SMS. The same steps taken here can be easily modified to send a message across Viber Service Messages, Facebook Messenger and any future channels that we add.

### 1. Configure your Delivery Receipt and Inbound Message endpoint with Nexmo

To recieve updates about the state of a message (i.e. "delivered" or "read") you have just sent and to recieve inbound messages from your customers you will need to configure an endpoint for Nexmo to send message to. If you don't have a webhook server set up you can use a service like [requestb.in](https://requestb.in/) for free.

From [Nexmo Dashboard](https://dashboard.nexmo.com) go to [Settings](https://dashboard.nexmo.com/settings).

Set the HTTP Method to POST and enter your endpoint in the fields labeled **Webhook URL for Inbound Message** and **Webhook URL for Delivery Receipt**:

```screenshot
script: app/screenshots/webhook-url-for-inbound-message.js
image: public/assets/screenshots/dashboardSettings.png
```

### 2. Generate a JWT to Authenticate with Nexmo

Future Nexmo APIs are authenticating with JSON Web Tokens (JWTs). This is a more secure method then API key and Secret and only requires a few more steps.

In order to create a JWT for you Nexmo API key you will need to create a Nexmo Voice Application (during the Developer Preview we will be adding Application support for the Messages and Workflows API). This can be done under the [Voice tab](https://dashboard.nexmo.com/voice/create-application) or using the [Nexmo CLI]( https://github.com/Nexmo/nexmo-cli) tool.

You will be asked to provide an Event URL and an Answer URL when creating a Voice Application. These are currently only used by the Voice API and are ignored by the Messages and Workflows APIs. Instead the Messages API and Workflows API use the Delivery Receipt and Inbound Message URLs that you set in [Settings](https://dashboard.nexmo.com/settings).

Once you have created a Voice application you can use the application ID and private key to generate a JWT. There is more information on [Voice Application management]( https://www.nexmo.com/blog/2017/06/29/voice-application-management-easier/) and the use of [Nexmo libraries](https://developer.nexmo.com/tools).

If you're using the Nexmo CLI the command is:

```curl
$ JWT="$(nexmo jwt:generate /path/to/private.key \application_id=NEXMO_APPLICATION_ID)"
$ echo $JWT
```

### 3. Send an SMS with Messages API

Sending an SMS message with the Messages API is straightforward. Replace the following variables in the example below:

Key | Description
-- | --
`NEXMO_APPLICATION_ID` |	The ID of the application that you created.
`FROM_NUMBER` | The phone number you are sending the message from in [E.164](https://en.wikipedia.org/wiki/E.164) format. For example `447700900000`.
`TO_NUMBER` | The phone number you are sending the message to in [E.164](https://en.wikipedia.org/wiki/E.164) format. For example `447700900000`.

| #### Prerequisites
|
| 1. [Rent a virtual number](/account/guides/numbers#rent-virtual-numbers)
|
| 2. [Create an application](/concepts/guides/applications#getting-started-with-applications)
|
| 3. Generate a JWT:
|
|     ```curl
|     $ JWT="$(nexmo jwt:generate /path/to/private.key \application_id=NEXMO_APPLICATION_ID)"
|     $ echo $JWT
|     ```

#### Example

```tabbed_examples
config: 'olympus.messages.send-sms'
```

## Building Blocks

* [Send an SMS with Messages API](/olympus/messages/building-blocks/send-an-sms-with-messages-api)
* [Send with Facebook Messenger](/olympus/messages/building-blocks/send-with-facebook-messenger)
* [Send a Viber Service Message](/olympus/messages/building-blocks/send-a-viber-service-message)
* [Send a message with failover](/olympus/workflows/building-blocks/send-a-message-with-failover)

## Guides

* [Facebook Messenger](/olympus/messages/guides/facebook-messenger)
* [Viber Service Messages](/olympus/messages/guides/viber-service-messages)

## Reference

* [Messages API Reference](/api/olympus/messages)
* [Workflows API Reference](/api/olympus/workflows)
