---
description: Creating and using object profiles
---

# Object Profiles

Object Profiles describe the shape of [Objects](../objects/) i.e. what properties (resources) an objects has, the data type of each property (resource), and metadata describing the object and it properties.

{% hint style="info" %}
MobiusFlow object properties are called resources. A resource holds a single value associated with an object.&#x20;

E.g. an air quality sensor object may have separate resources for temperature, humidity, and CO<sub>2</sub> level.
{% endhint %}

For more information on objects and resources read the [MobiusFlow Architecture](../../mobiusflow-overview/mobiusflow-architecture.md) article.

Before creating objects you must first define an object profile. Profiles can be created from scratch, or based on a predefined template or existing object profile.&#x20;

{% hint style="success" %}
It is possible to [create objects](../objects/adding-objects-to-a-service.md) directly from a template. The object profile will be created for you.
{% endhint %}

## Profile IDs (PIDs)

All object profiles must have a unique profile ID or PID. This is a four digit hexadecimal number and can be any value from 0200 to FFFF as long as a profile with that PID does not already exist. The PID will form part of an object's URI identifying the object's type, and can be used when subscribing to object or resource COVs to filter by object type.&#x20;

See [MobiusFlow Uniform Resource Identifiers](../../mobiusflow-overview/mobiusflow-uniform-resource-identifiers-uris.md) for more information.

{% hint style="info" %}
Once an object profile is in use (an object of that type has been added to a service) its PID cannot be changed.
{% endhint %}

## Resources

All live data in MobiusFlow is stored in object resources. Each resource stores a single simple value of a specific type.&#x20;
