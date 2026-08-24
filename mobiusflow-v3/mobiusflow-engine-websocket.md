---
description: Usage of MobiusFlow Engine Websocket
---

# MobiusFlow Engine Websocket

The Engine websocket is a data interface which runs on top of the MobiusFlow Engine API on all MobiusFlow Engines.&#x20;

The websocket allows for extraction of event driven data via a subscribe / unsubscribe model.

Unlike the base Engine API which operated on request/response model, the websocket pushes data to you. This means you do not have to set up regular data / event polling to remain up to date on the state of the MobiusFlow Engine.

Before using the Engine Websocket we recomend you're familar with the following:

* [MobiusFlow URIs (& URI Wildcarding)](mobiusflow-overview/mobiusflow-uniform-resource-identifiers-uris.md)
* [Engine API](mobiusflow-engine-api-v3/)

The websocket allows subscriptions to the following MobiusFlow events:

[See event types](mobiusflow-engine-websocket.md#event-types).

## Connection Endpoint

Websocket connection endpoint exists on the MobiusFlow Engine Rest:

```
(GET)
/api/engine/v3/subscribe/connect
```

On initial connection, no authorization is required. This means you do not need to include any token within the request body or headers.

## Authorization

Once the inital websocket connection is made, the server will expect a follow up authorization message within 30 seconds in the following format:

```json
{
    "topic": "authorize",
    "payload": "Bearer 8e100e7bef9898963477f2c8a89eeedb8b679c221e446cf0249787119cc44b51e792b2a03d0ffb75ef68149c0cbea13d21c758443d44735027c25fecb7f9c992"
}
```

Where the token portion of the payload is a valid session token returned from an Engine API login call (_/api/engine/v3/auth/login_).

{% hint style="info" %}
Note: The token is packaged in bearer token format (The prefix Bearer is applied) e.g. "Bearer XXXXX"
{% endhint %}

If no authorization call is received by the server, the connection will be dropped.

Following successful authorization, subscription to any engine events can proceed.

## Subscribe / Unsubscribe

### Event Types

<table><thead><tr><th width="146.5078125">Event Type</th><th width="343.96484375">Notes</th><th>URI Format</th></tr></thead><tbody><tr><td>COV</td><td>Change of value of a specific MobiusFlow resource. URI parameter refers to specific resource to subscribe to change events on.</td><td>(To resource level): XXXXXX/XXX/XXXX/XXXX/XX</td></tr><tr><td>OBCOV</td><td>Change of value of any resource within a given MobiusFlow object. URI parameter refers to specific object to subscribe to change events on.</td><td>(To object level): XXXXXX/XXX/XXXX/XXXX</td></tr><tr><td>SRVCSTATUS</td><td>Change of service status of a given MobiusFlow service. URI parameter refers to the service to subscribe to status change events on.</td><td>(To service level): XXXXXX/XXX</td></tr><tr><td>BCMD</td><td>Subscribe to any MobiusFlow broadcast commands. URI controls which service / services to subscribe to broadcast commands on.</td><td>(To service level): XXXXXX/XXX</td></tr></tbody></table>

### Subscribe

Each event type can be subscribed to by sending messages in the following format:

```json
{
    "topic": "subscribe",
    "payload": {
        "type": <EVENT TYPE>,
        "uri": <URI>
    }
}
```

Where \<EVENT TYPE> is replaced by the event type (**COV, OBCOV, SRVCSTATUS, BCMD**).

For the BCMD event type the additional CMD property must be included to specify the command to you're subscribing too:

```json
{
    "topic": "subscribe",
    "payload": {
        "type": "BCMD",
        "uri": <URI>,
        "cmd": <CMD>
    }
}
```

Where \<CMD> should be replaced by any BCMD command type.

### Unsubscribe

Unsubscribing is achieved in an identical manner except the message topic should read unsubscribe:

```json
{
    "topic": "unsubscribe",
    "payload": {
        "type": <EVENT TYPE>,
        "uri": <URI>
    }
}
```

### URI Wildcarding

All subscriptions can be wildcarded using standard [URI wildcarding](mobiusflow-overview/mobiusflow-uniform-resource-identifiers-uris.md).
