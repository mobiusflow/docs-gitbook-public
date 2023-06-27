# MobiusFlow Uniform Resource Identifiers

Within a MobiusFlow system all nodes, services, objects and resources are identified by a unique address known as a Uniform Resource Identifier or **URI**. These URIs are hierarchical so given the URI for a Mobius resource it is possible to identify which object the resource belongs to, what the object type is, which service the object belongs to and which Mobius node the service is running on.

## Mobius URI Definition <a href="#mobiusflowuniformresourceidentifiers-mobiusuridefinition" id="mobiusflowuniformresourceidentifiers-mobiusuridefinition"></a>

An object’s URI (or name) is defined in 4 parts, namely the hub ID _(HID)_, service ID _(SID)_, object profile ID _(PID)_ and instance number _(INS)_. A fifth part is added when accessing a specific resource, the resource ID _(RID)_.

Each part of an object’s URI is a [hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal) uppercase string of a defined length (as shown in the table below). The URI’s parts are separated with a forward slash (/).

A full URI is typically defined as **HID/SID/PID/INS/RID**.

It is possible to address any part of the system by only using the required parts of the URI. e.g. to address a service only the first two parts of the URI are used **HID/SID** and to address an object only the first four parts are used **HID/SID/PID/INS**.

<table data-header-hidden><thead><tr><th width="138"></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>URI Section</strong></td><td><strong>Length</strong></td><td><strong>Example</strong></td><td><strong>Description</strong></td></tr><tr><td><strong>HID</strong></td><td>6</td><td>000001</td><td>The Mobius Hub or node ID. This should be unique within a <strong>Mobius</strong>Flow system.</td></tr><tr><td><strong>SID</strong></td><td>3</td><td>01F</td><td>The microservice ID. This must be unique for all services on a single node.</td></tr><tr><td><strong>PID</strong></td><td>4</td><td>003A</td><td>The object's profile ID. This describes the objects type. Object profiles determine what resources an object has available.</td></tr><tr><td><strong>INS</strong></td><td>4</td><td>0001</td><td>The object's instance number. This is unique for each object of a specific type belonging to a service.</td></tr><tr><td><strong>RID</strong></td><td>2</td><td>40</td><td>The resource ID</td></tr></tbody></table>

An example of an object URI for an object of instance 1, profile 3A, created by service 1F connected to hub 1 is:

_**000001/01F/003A/0001**_&#x20;

and if addressing resource 40 on that object the full URI would be:

_**000001/01F/003A/0001/40**_

## Mobius URI Wildcards <a href="#mobiusflowuniformresourceidentifiers-mobiusuriwildcards" id="mobiusflowuniformresourceidentifiers-mobiusuriwildcards"></a>

Under certain conditions, such as subscribing to a resource’s change of value event, it is possible to use wildcards in the URI. These wildcards are described in the table below and follow the [MQTT](https://iaconnects.atlassian.net/wiki/spaces/OD/pages/17990573) standard.

| **Wildcard** | **Meaning**                                             | **Example**        |
| ------------ | ------------------------------------------------------- | ------------------ |
| **+**        | Any value in this location                              | 000001/+/003A/+/40 |
| **#**        | Any value in this location and all subsequent locations | 000001/01F/#       |
