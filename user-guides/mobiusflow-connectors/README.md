---
description: Overview of MobiusFlow Connectors
---

# MobiusFlow Connectors

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-10 at 12.36.16.png" alt="" width="375"><figcaption><p>MobiusFlow Connector</p></figcaption></figure>

The Connector collects data from sensors and sends data to actuators via standard wireless sensor protocols such as EnOcean and Workplace Occupancy, and sends this data securely to a MobiusFlow using an MQTT based Protocol.

Once the data has been received by a MobiusFlow instance, it is decoded and the associated MobiusFlow object is updated with the latest sensor readings which can then be processed by the gateway.

<figure><img src="../../.gitbook/assets/3500-26-02-0030_MF-mobiusflow-connector-diagram-0-2-0.png" alt=""><figcaption><p>Architecture</p></figcaption></figure>

A full guide on configuring MobiusFlow for use with Connectors can be found [here](configuring-mobiusflow-for-use-with-connectors.md).

## Connector Options

There are several hardware options for the MobiusFlow Connector software:

* [Official Connector](mobiusflow-official-connector/)
* [Raspberry Pi](mobiusflow-raspberry-pi-connector/)
