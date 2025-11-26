---
description: What are MobiusFlow objects and how are they used?
---

# Objects

MobiusFlow objects represent real or virtual devices such as sensors, rooms, pieces of equipment, and machinery. All objects are based on an [Object Profile](object-profiles/) which describes the shape of the object i.e. what properties (resources) an objects has, the data type of each property (resource), and metadata describing the object and it properties.

{% hint style="info" %}
MobiusFlow object properties are called resources. A resource holds a single value associated with an object.&#x20;

E.g. an air quality sensor object may have separate resources for temperature, humidity, and CO<sub>2</sub> level.
{% endhint %}

For more information on objects and resources read the [MobiusFlow Architecture](../mobiusflow-overview/mobiusflow-architecture.md) article.

Objects must belong to a [service](/broken/pages/fc5828fd69cf8222a5b30c1ce49550ad90180cd3). To add new objects or configure existing objects on a service open the Service's Objects page by clicking on the service in the main menu or clicking on the main body of a service's card on the Services page.

<figure><img src="../../.gitbook/assets/Objects page.png" alt=""><figcaption></figcaption></figure>
