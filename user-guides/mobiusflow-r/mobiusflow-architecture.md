# MobiusFlow Architecture

## Mobius system <a href="#mobius_system" id="mobius_system"></a>

A typical Mobius system consists of a single or multiple Mobius nodes connected together via a TCP/IP network. Each node is capable of operating independently of the rest of the system, but nodes can interact with each other to form a complex system. All node interaction takes place through one or more brokers via a node’s router.In a multi-node system, the location of the broker is not important. It can reside on the same device as one of the nodes or on an independent device.

Each node is classed as, and exhibits the behavior of, an [edge computing](https://en.wikipedia.org/wiki/Edge\_computing) device. In this context edge devices are not only field devices but could also be on the _edge_ of a server or cloud server providing the server with connectivity to all of the true edge or field devices.

The IA Mobius Servers and Gateways, Lighting Control Modules, and Building Control Modules are all Mobius nodes.

![](https://support.iaconnects.co.uk/hc/article\_attachments/360017722712/Mobius\_System\_Overview.png)

## Mobius nodes <a href="#mobius_nodes" id="mobius_nodes"></a>

A Mobius node consists of a central Mobius **hub**, one or more Mobius **services** and optionally one or more Mobius **routers**.

Services contain the service logic and an object data store. Connections to sensors, actuators and other communication interfaces such as Modbus or BACnet can be added depending on the service’s purpose and controlled through the service's logic.

The object data store models the physical or virtual connections and provides a standardised method for services and other nodes to communicate and share data with each other through Mobius objects.

All of the communications between services through the hub or nodes through routers and brokers is based on the [MQTT](http://iaconnects.atlassian.net/wiki/spaces/OD/pages/17990573) protocol. The MobiusFlow protocol has been defined on top of this MQTT protocol providing a well-defined API enabling different physical devices and protocols to communicate with each other in a consistent way.   &#x20;

Mobius nodes follow the [microservice](https://en.wikipedia.org/wiki/Microservices) architecture pattern, where each service is a stand-alone process capable of communication with other microservices creating a large application from small manageable pieces.

Routers are used to cross node boundaries. They provide a secure mechanism for nodes to share data using the MobiusFlow protocol.

![](https://support.iaconnects.co.uk/hc/article\_attachments/360017723292/Mobius\_Node.png)

### Logical structure of a node <a href="#logical_structure_of_a_node" id="logical_structure_of_a_node"></a>

The logical structure of a node is detailed below. This diagram shows the hierarchical relationship between all of the parts which make up a node and how objects contain resources, services contain objects and hubs connect to services and routers.

The Mobius URI structure allows addressing any part of a node at any depth.

![Mobius\_Logical\_Structure.png](https://support.iaconnects.co.uk/hc/article\_attachments/360017608911/Mobius\_Logical\_Structure.png)

### Hubs <a href="#hubs" id="hubs"></a>

A Mobius hub is the foundation of a **node**. At its heart, a Mobius hub is just an MQTT broker which manages and links Mobius **services** and Mobius **routers**. Hubs are responsible for ensuring that all services and routers are valid members of a node by verifying their pre-shared authentication key on connection.

Each hub within a Mobius system is given a unique ID. This is a six digit hex number which forms the first part of the Mobius URI hierarchy. When referencing a hub, for example during a discovery process, this unique ID must be used (see [MobiusFlow Uniform Resource Identifiers](mobiusflow-uniform-resource-identifiers.md)).

When service or router connects to a hub, and has been validated, the hub provides it with a copy of the Mobius object profiles and pre-shared keys files, ensuring that all services and routers connected to the hub are able to communicate and understand one another.

### Services <a href="#services" id="services"></a>

Mobius services are the engines which drive MobiusFlow. Each service is essentially a microservice performing a specific task and possibly acting as an interface to a piece of hardware or a 3rd party service such as Microsoft's Azure platform or the IBM Cloud.

All services MUST implement the full MobiusFlow protocol to enable them to connect to hub and communicate with other services. In addition to implementing the MobiusFlow protocol, services can create Mobius objects to store and share data and can also contain service specific logic to perform the task that they are designed for. When creating services, try an keep them focused on one task and create additional services to perform other tasks. This ensures that services are reusable and Mobius systems can be configured to only contain the logic that they require.

Each service within a Mobius node is given a unique ID. This is a three digit hex number which forms the second part of the Mobius URI hierarchy. When referencing a service, for example during a discovery process, this unique ID must be used (see [MobiusFlow Uniform Resource Identifiers](mobiusflow-uniform-resource-identifiers.md)).

### Routers <a href="#routers" id="routers"></a>

Mobius routers control all MobiusFlow communication into and out of a node. This ensures that nodes are secure and allows nodes to discover each other within a MobiusFlow system.

Routers are split into two parts, one side of the router communicates internally with its associated hub and all of the services within a node, while the other side of the router communicates externally through a 'no-mans' broker to other routers on other nodes. All external communication is done using MQTT over the [WebSocket](https://en.wikipedia.org/wiki/WebSocket) protocol. This could be done over a secure or non-secure connection (ws:// or wss://).

Routers are capable of routing messages between services belonging to different nodes, essentially allowing a service on one node to read, write and subscribe to change-of-value events on objects in another node.

## Mobius objects <a href="#mobius_objects" id="mobius_objects"></a>

The key to the MobiusFlow system is Mobius objects. These objects typically model real-world objects and provide a mechanism for sharing data and storing state in a consistent way. Each object has a unique identifier or [Mobius URI](mobiusflow-uniform-resource-identifiers.md) which can be discovered and used by any part of the MobiusFlow system.

Mobius objects are predefined in an object profiles file which is passed to a services by the hub when a service connects.

Each object within a Mobius node is given a unique ID. This ID consists of two parts and is made up of the object profile ID (PID) which describes the object's type, and the object's instance number (INS). The PID is a four digit hex number which forms the third part of the Mobius URI hierarchy and the INS is a four digit hex number which forms the fourth part of the Mobius URI hierarchy. When referencing an object, for example during a discovery process, this unique ID must be used (see [MobiusFlow Uniform Resource Identifiers](mobiusflow-uniform-resource-identifiers.md)).

### Object resources <a href="#object_resources" id="object_resources"></a>

Mobius objects contain one or more resources. It is these resources which are used to define objects that mimic or represent real-world objects. An example of a single object is a room temperature sensor. This object may have resources which define the sensor’s name, location, asset reference, engineering units, set point and actual measured value.

Each resource is capable of storing a single value which can currently be of type **Boolean**, **Number,** **String, DateTime or TimeSpan**. Resources also store meta-data about the value. The actual meta-data depends on the value type chosen. Resources can be read only or read/write. Read only resources have their values set when they are created.&#x20;

Each resource within an object is given a unique ID. This is a two digit hex number which forms the fifth and final part of the Mobius URI hierarchy. When referencing a resource, for example during a read, this unique ID must be used (see [MobiusFlow Uniform Resource Identifiers](mobiusflow-uniform-resource-identifiers.md)).

#### Present value and the priority array <a href="#present_value_and_the_priority_array" id="present_value_and_the_priority_array"></a>

Resources store their values in a priority array. This priority array works in a similar manner to a [BACnet](http://www.bacnet.org/) priority array. The array has 16 possible locations with location 1 being the highest priority and location 16 being the lowest priority.

When reading the value of a resource the actual value is returned in the **PV**(present value) property. The **PV** is always equal to the value of the highest active (non null) priority in the resource's priority array.&#x20;

```json
{null,null,null,null,null,null,null,null,null,null,null,null,null,null,12,null} -> PV = 12 (priority 15)
{null,null,null,null,null,null,null,null,56,null,null,null,null,null,12,null} -> PV = 56 (priority 9)
{null,null,78.5,null,null,null,null,null,56,null,null,null,null,null,12,null} -> PV = 78.5 (priority 3)
```
