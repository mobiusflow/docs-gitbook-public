---
description: Usage of MobiusFlow Historian Websocket
---

# MobiusFlow Historian Websocket

The Historian websocket is a data interface which runs on top of the MobiusFlow Historian Data API on all MobiusFlow Historians.&#x20;

The websocket allows you to listen to real-time incoming data updates on MobiusFlow historian. This avoids the requirement to query recent historical data via the Historian Data API to extract the most recent data.

Before using the Historian Websocket we recommend you're familiar with the following:

* [Historian](mobiusflow-historian.md)
* [Historian API](mobiusflow-historian-data-api-v3/)

## Connection Endpoint

Websocket connection endpoint exists on the MobiusFlow Historian Data API:

```
(GET)
/api/engine/v3/ws/connect
```

On initial connection, no authorization is required. This means you do not need to include any token within the request body or headers.

## Authorization

Once the initial websocket connection is made, the server will expect a follow up authorization message within 30 seconds in the following format:

```json
{
    "topic": "authorize",
    "payload": "8e100e7bef9898963477f2c8a89eeed"
}
```

Where the the payload is a valid [api key generated via MobiusFlow View](mobiusflow-historian-websocket.md#creating-an-api-key).&#x20;

If no authorization call is received by the server, the connection will be dropped. Following successful authorization, the websocket will automatically push all data updates.

### Creating an API Key

To add this, click your user tag within MobiusFlow View, then click **Manage Data API Keys**:

<figure><img src="../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

Then within Data API Key Management, click **Add Key**:

<figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

Once you create a key, ensure you copy it for usage as it will not be revealed again.
