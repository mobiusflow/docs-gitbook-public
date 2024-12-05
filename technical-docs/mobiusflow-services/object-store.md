---
description: Article covering MobiusFlow Object Store service
---

# Object Store

The _Object Store_ service can be considered a service type only for storing MobiusFlow objects. It has no functional backend. This means, unlike most other MobiusFlow services, the service will not interact with the objects stored on it.

## Uses

* For storing non-service specific objects such as the _Numeric Value_ objects or _String Value_ objects (Often these will be used if values are being calculated based on other objects)
* Manually writing to an object type, instead of relying on its functional parent service (e.g. manually writing the data into a LoRaWAN device object from the Flows, instead of using the _LoRaWAN LNS_ service)
* Testing
* Diagnostics

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption><p>An example Numeric Value object residing on an Object Store Service</p></figcaption></figure>

## Limitation

Although it is possible to place any object type in an _Object Store_ service, because the service has no functional backend, it cannot interact with most object types in fully functional way. For example, adding a LoRaWAN device object to an _Object Store_ service is possible, however the object will not be automatically populated by incoming LoRaWAN messages. If the LoRaWAN device object was placed into its functional parent service (_LoRaWAN LNS_ service / _LoRaWAN Devices_ service) instead, it would function as normal, as these service types have the correct backend to work with this object type.
