---
description: Creating and using object profiles
---

# Object Profiles

Object Profiles describe the shape of [Objects](../objects.md) i.e. what properties (resources) an objects has, the data type of each property (resource), and metadata describing the object and it properties.

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

{% hint style="warning" %}
Once an object profile has been created its PID cannot be changed.
{% endhint %}

## Resources

All live data in MobiusFlow is stored in object resources. Each resource stores a single simple value of a specific type. These types include

<table><thead><tr><th width="124.65234375"></th><th></th></tr></thead><tbody><tr><td><strong>bool</strong></td><td>Boolean value (true or false)</td></tr><tr><td><strong>string</strong></td><td>Text string value</td></tr><tr><td><strong>number</strong></td><td>Numeric floating point or integer value</td></tr><tr><td><strong>datetime</strong></td><td>A date and time value in ISO format e.g. 2025-11-23T18:56:08.175Z<br>These values are always in the UTC time zone as indicated by the Z<br>See '<a href="https://www.mma-tx.org/blog/14701/zulu-time-made-easy/">Zulu Time</a>'</td></tr><tr><td><strong>enum</strong></td><td>An enumerated value e.g. LARGE | MEDIUM | SMALL</td></tr></tbody></table>

When writing a value to a resource it should always be of the correct type although values will be coerced to the correct type if possible.

In addition to setting the data type for a resource you can also define some settings for each resource. These settings will depend on the type e.g. a string resource will have a setting for the maximum length and a number resource will have settings for the maximum and minimum value that can be stored.

## Codecs, Preprocessors, and UI Layouts

For each object profile you can also define a [Codec](codecs.md), [Preprocessor](preprocessors.md), and [UI Layout](ui-layouts.md).&#x20;

<table><thead><tr><th width="136.234375"></th><th></th></tr></thead><tbody><tr><td><strong>Codec</strong></td><td>Codecs are used to encode and decode raw telegrams from sensors and data sources</td></tr><tr><td><strong>Preprocessor</strong></td><td>Preprocessors are run every time a new value is written to a resource. They are used to modify the value before it is written e.g. change from °C to °F, or update another resource e.g. update a message counter</td></tr><tr><td><strong>UI Layout</strong></td><td>Define additional inputs on an object's settings page and map these inputs to resources to set default values. UI Layouts are often used to capture things like sensor ID when configuring objects</td></tr></tbody></table>
