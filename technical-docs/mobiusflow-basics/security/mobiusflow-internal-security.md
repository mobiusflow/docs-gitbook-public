# MobiusFlow Internal Security

## Introduction <a href="#introduction" id="introduction"></a>

MobiusFlow is a software platform designed for control and monitoring of sensors and actuators in simple (single instance) or complex (multiple instances working together) systems (see [Mobius Overview](../mobiusflow-overview.md) for more info). It has a microservice based architecture where each microservice can contain both application logic and object state. Object types are predefined and contain any number of resources which represent the values associated to an object’s attributes (e.g. a temperature sensor may contain resources for Name, Location, Temperature etc.).\
\
A MobiusFlow node (a single instance of the software) contains a central hub and one or more microservices. All microservices contain an MQTT client and communicate with each other via the hub which is an MQTT broker. The broker is responsible for authenticating the services when they connect. The TCP/IP port used for internal MQTT comms is normally firewalled off to prevent any external traffic and all messages passed between microservices are encoded using [_JSON Web Token (JWT)_](https://support.iaconnects.co.uk/hc/en-gb/articles/360020873392) to ensure message integrity.\
\
If communication is required between Mobius nodes, a Mobius router is added to the configuration. This is a special microservice which handles external traffic between Mobius nodes. All traffic passed through a router is encoded with JWTs using pre-shared keys (PSKs) specifically for this purpose ensuring that no internal PSKs leave a Mobius node. External traffic is also MQTT based and can be secured with TLS if required.\
\
One of the most important part of MobiusFlow is the “ Mobius protocol” over MQTT. This is a predefined set of MQTT topics based around the Mobius object URIs which allows “two way point to point” messaging via MQTT. This means that Mobius nodes and microservices can discover other nodes, services, objects and resources and microservices can read and write resource values on objects belonging to any other microservice on any node within a Mobius system. In addition to reading a writing, a microservice can subscribe to object or resource level change of value (COV) messages.\
\
&#xNAN;_&#x54;he MobiusFlow protocol is similar to the LWM2M protocol but over MQTT._

The [Mobius architecture](../mobiusflow-architecture.md) is designed to allow efficient communication for IoT Devices whilst providing structure and definable trust boundaries.

There are 2 ways to move messages to and from a [mobius node ](https://support.iaconnects.co.uk/hc/en-gb/articles/360021111731)one is via the [mobius router ](https://support.iaconnects.co.uk/hc/en-gb/articles/360021111731)designed for this task, and preserving the integrity of the the message within the node. the other is with a dedicated [service](https://support.iaconnects.co.uk/hc/en-gb/articles/360021111731), this breaches that integrity to a degree but may be desirable and even necessary in some situations.&#x20;

### Node Internal Communication <a href="#node_internal_communication" id="node_internal_communication"></a>

With Each node consisting of the base of a hub and one or more services, and optionally routers. If for the purpose of this initial discussion assume that the services are only communicating with local hardware, or handling logic, therefore having no mechanism for communicating off of the local hardware. We will discuss how this can be achieved later on.

As the hub is created a pre-shared key (psk) file is generated, these can also be changed using the configuration service. each valid service must have a copy of its psk, to successfully authenticate with the hub. The hub will have the corresponding psk in its psk file. This key is used as a secret key as part of a [JSON Web Token (JWT)](https://support.iaconnects.co.uk/hc/en-gb/articles/360020873392).

### Service Authentication <a href="#service_authentication" id="service_authentication"></a>

&#x20;When a service connects to a hub it uses the [MQTT built in username / password authentication](https://www.hivemq.com/blog/mqtt-security-fundamentals-authentication-username-password/). The MQTT username is the service's [profile ID (PID)](https://support.iaconnects.co.uk/hc/en-gb/articles/360020867912) and [service (SID) ](https://support.iaconnects.co.uk/hc/en-gb/articles/360020867912)001F/01F and the MQTT password is a JSON object containing the services PID and SID with a timestamp which is then converted into a JWT (JSON Web Token). The time stamp ensures tight time synchronisation is a requirement and provides greater integrity.

If the service signs its JWT with the same psk as is stored in the hub's psk file it will successfully complete the authentication process to the hub. On doing this it will be sent a copy of the hubs psk file, giving the service the ability to the received directly signed messages from authorised services.

After successful authentication the service will have a copy of the psk of all services that are authorised to communicate through the hub. The service will then with no further action from the hub be able to validate the authenticity and integrity of messages that have come from a service on the same node.&#x20;

### Service Communication <a href="#service_communication" id="service_communication"></a>

Once passing traffic the MQTT message will consist of:

the JSON Web Token will also carry the topic, the message payload itself, and a timestamp this will all be hashed along with the service own key creating a [HMAC ](https://en.wikipedia.org/wiki/Hash-based_message_authentication_code)to allow integrity checking:

The time stamp will allow for the message to have a validity life span that can be configured for all services connected to the hub. Internally all messages will be signed in this way and therefore provide a high degree of integrity to the internal communication.

Services may be intentionally created to connect to external interfaces such as a service the connects to remote I/O via TCP/IP or an Azure IoT hub Client, if it is desired to configure a node in this scenario, it is recommended to utilise two interconnected nodes one that handles the external communications and one that handles the more trusted internal communication, the nodes could exist on the same hardware. doing so would allow the creation of multiple trust boundaries

### Node External Communication <a href="#node_external_communication" id="node_external_communication"></a>

Although as just discussed it is not impossible to create service that communicate to external interfaces, it is not recommended to use these on the same node as it compromises the integrity of the node. It is preferable to utilise a known route into and out from the node, it is recommended that this route is a [mobius router](https://support.iaconnects.co.uk/hc/en-gb/articles/360021111731).

Routers are split into two parts, one side of the router communicates internally with its associated hub and all of the services within a node, while the other side of the router communicates externally through a 'no-mans' broker to other routers on other nodes. All external communication is done using MQTT over the [WebSocket ](https://en.wikipedia.org/wiki/WebSocket)protocol. This could be done over a secure or non-secure connection (ws:// or ws s://).

The internal side of the router acts in exactly the same way as a service, but will automatically subscribe to all messages from every other service within that node.

The external side of the router will have the ability to sign its messages in the same fashion as the services do for internal communication, it will have two pre shared keys and internal or service psk and an external psk.

### Node Peering <a href="#node_peering" id="node_peering"></a>

&#x20;To allow router to validate the authenticity and integrity of messages form other routers, the external psks will be required to be manually shared between all the routers that want to take part in this communication. the result is that the external psk file will contain the keys of all authorised routers and therefore nodes.

This communication is done over the WebSocket protocol as it reduces the need to configure firewalls to allow MQTT communication. node peering is best used in an enclosed environment where there is a high degree of confidence in the integrity of the network with which the communication is taking place. This is like to require the input of network and cyber security professionals.

Node Peering will require the provision of a MQTT broker capable of using [MQTT over WebSockets](http://www.hivemq.com/blog/mqtt-over-websockets-with-hivemq). this will be a function that will be optionally provided by the mobius router.

### Larger Node Deployments <a href="#larger_node_deployments" id="larger_node_deployments"></a>

&#x20;In larger deployments of nodes peering may not be viable because of the administrative overhead, or there may be low confidence in the network integrity. there may also be a require to not only ensure Authenticity and Integrity of messages, but also confidentiality.

to achieve this the nodes should utilise WebSockets over [Transport Layer Security ](https://en.wikipedia.org/wiki/Transport_Layer_Security)(TLS), this is in fact simply a [HTTP ](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)upgrade in the same way WebSockets are used, on a [HTTPS ](https://en.wikipedia.org/wiki/HTTPS)connection

In this case it will almost always be easier to provide the node with access to the public internet where things like server name resolution and certificate control are well practised and understood.

&#x20;Due to the large complexity in provisioning the system in this scenario, It is envisaged at this stage that IAconnects will provide the service that provides the functions of the architecture shown above.
