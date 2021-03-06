---
title: "Send Verification Flow"
category: "reference"
type: "content"
source: "https://github.com/uport-project/specs/blob/develop/flows/verification.md"
---

# Send Verification Flow

A client application can verify information about a user

The following shows the basic flow:

![Verified Claim Flow](verification.png)

A more complete example of using this with a simple Identify Verification service can be seen here. In this case the user starts with a [Selective Disclosure Flow](selectivedisclosure.md) to an issuer. An offline process could be in place where the user now shows their passport to the Issuer after which they will receive an identity verification in their mobile app.

![Example Identity Verified Claim Flow](identityverification.png)

## Endpoint

The request should be sent to the following URLs:

- `https://id.uport.me/req/[JWT]`

*The following endpoints are deprecated*

- `me.uport:add`
- `https://id.uport.me/add`

## Send Verifications

Create a [Verified Claims](../messages/verification.md) and attach it to the `https://id.uport.me/req/` url. Present this URL to the user and the app will open.

Example:

`https://id.uport.me/req/eyJ0eXAiOiJKV1QiLCJhbGciOiJFUzI1NksifQ.eyJp...`

### Deprecated Flows

A deprecated version adds it to the uPort mobile app in the `attestations` query parameter.

Example:

`me.uport:add?attestations=eyJ0eXAiOiJKV1QiLCJhbGciOiJFUzI1NksifQ.eyJp...`

The attributes `redirect_url` and `callback_type` can also be appended to the URL as encoded query parameters to specify how you want the response and control returned. For more details see [Messages](./index.md#json-web-token).


## Client Callback

The client app MAY include a URL where the response is returned from the user. This can be a HTTPS URL or a custom app URL which receives the response. The callback is strictly optional and is mainly used if you need to acknowledge in your UX that the attestation has been received.

### Successful Response

param  | Description
------ | -----------
status | always `ok`
