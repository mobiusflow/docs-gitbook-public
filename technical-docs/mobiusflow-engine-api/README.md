---
description: Description of MobiusFlow Engine RESTful API V1
---

# MobiusFlow Engine API

The **MobiusFlow Engine API** is used interface with MobiusFlow via **http** and **https**. The API allows clients to perform all functions within MobiusFlow, from managing user accounts, to getting and setting data, as well as manipulating the MobiusFlow configuration by adding, removing and editing MobiusFlow objects, services and flows.

Additionally, the API allows clients to subscribe to specific real-time events within happening within  a given MobiusFlow instance (see [subscription controller](subscription.md)). In this use case, the API will upgrade the client to use the Websocket protocol (**ws** / **wss**).

## Controllers

All API endpoints are described in the following subsections. The subsections are divided into the functional groups (controllers); [Authorization](authorization.md), [Discover](discover.md), [Node](node.md), [Service](service.md), [Object](object.md), [Profiles](profiles.md), [Command](command.md), [Flows](flows.md) and [Subscription](subscription.md).

## Protocols, Endpoints and Ports

If connecting to a local instance of MobiusFlow, the http protocol can be used. If connecting to an instance of MobiusFlow via the internet, https should be used. The API is always exposed on **port 8443**.

All endpoints lead with:

\{{_protocol_\}}**://**\{{_hostname_\}}**:8443/api/v1**

Where the protocol and hostname parameters are replaced with the true protocol and hostname. For example, in the case of connecting to a local instance of MobiusFlow, the leading path would look like:

**http://localhost:8443/api/v1**

## Further Documentation & Postman Collection

Swagger documentation describing the API in full, can be found [here](https://docs-engine-api.mobiusflow.io/static/index.html). This documentation includes example bodies and responses for every endpoint. Finally, a postman collection containing parameterised examples of all client calls can be downloaded below.

{% file src="../../.gitbook/assets/Mobius Engine API.postman_collection.json" %}
