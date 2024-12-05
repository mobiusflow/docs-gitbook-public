# MobiusFlow Overview

<figure><img src="../../.gitbook/assets/3500-01-06-01_0001_mobiusflow-logo-colour-black-on-transparent-1-0-0.jpg" alt="" width="188"><figcaption></figcaption></figure>

The MobiusFlow software has been developed as an MQTT object bus which normalises all device data into standardised MobiusFlow objects which allow interoperability between all devices either real or virtual in the field or Cloud.

MobiusFlow enables actuators, sensors & controllers to connect, control and communicate with each other and to the Cloud so that IoT solutions using scalable monitoring, visualisation and predictive analytics can provide valuable insights into your business and act upon them automatically.

* A complete control and communications platform
* Microservice based architecture
* Secure, open protocol based on MQTT
* Scalable to 1000s of devices
* Platform and language independent
* Does not depend on a network connection for local control
* Provides full discovery of nodes, objects and resources in all directions
* Pub / Sub change of value notifications
* All sensor and actuator data is normalised from any source such as [OPC UA](https://opcfoundation.org/about/opc-technologies/opc-ua/)/ [BACnet](http://www.bacnet.org/)/ [DALI](http://iaconnects.atlassian.net/wiki/spaces/OD/pages/17990637)/ [EnOcean](http://iaconnects.atlassian.net/wiki/spaces/OD/pages/17990584)/ LoRaWAN / Analog / Digital etc.&#x20;

MobiusFlow has been designed from the ground up as a micro service based design with a simple but common set of API commands. All communication between micro services is performed using the MQTT protocol, ensuring that micro services can be written in any programming language and will run on any device capable of TCP/IP network communications. The only requirement for any MobiusFlow system is that it contains at least one Node. This Node consists of a MobiusFlow Hub which initiates and facilitates communication between micro services in a secure way. Micro services can run on the same device as the Hub, or on another device such as a temperature sensor, connected to the Hub via a connection capable of transmitting via TCP/IP (provision has been made for future expansion, by adding translation services, to allow micro services to communicate with the Hub over any transmission medium capable to transmitting binary data).

Each Node is typically a stand-alone island which does not require any connection to any other device in order to perform local control. Nodes can be connected together via secure MobiusFlow Routers allowing the creation of a network of interconnected Nodes. When used in this configuration, Nodes can share data with each other and influence the control algorithms running on any connected Node.

Vanilla MQTT has some limitations in its usefulness as a peer to peer messaging and control protocol. It is based around the Publish / Subscribe pattern which is ideal where multiple devices are sending data to a single end point for logging etc. MQTT can be used where devices or services need to have a two way peer to peer flow of communication but the different services need to be aware of each other at design time. MobiusFlow defines a protocol layer above MQTT which enables discovery of devices and services at runtime and then allows two way peer to peer communication to take place, ensuring that new devices and services can be added at any time without having any design time knowledge of the other devices and services in a system.
