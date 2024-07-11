---
description: Configure your MobiusFlow® Connector and connect it to a MobiusFlow® instance
---

# Configuring MobiusFlow Connectors

<figure><img src="../../../.gitbook/assets/Screenshot 2023-03-10 at 12.36.16.png" alt=""><figcaption></figcaption></figure>

The Connector collects data from sensors and sends data to actuators via standard wireless sensor protocols such as EnOcean and Workplace Occupancy, and sends this data securely to a **Mobius**Flow® Gateway or **Mobius**Flow® Virtual Cloud Gateway using the MQTT based **Mobius**Flow® Sensor Protocol.

Once the data has been received by a **Mobius**Flow® Gateway it is decoded and the associated **Mobius**Flow® object is updated with the latest sensor readings which can then be processed by the gateway.

<figure><img src="../../../.gitbook/assets/3500-26-02-0030_MF-mobiusflow-connector-diagram-0-2-0.png" alt=""><figcaption><p>Architecture</p></figcaption></figure>

## Part Numbers

It is possible to have up to two radios for wireless sensors in a single connector. This is useful when you have combination of sensors using different protocols.&#x20;

The current options are _EnOcean_ and _Workplace Occupancy_ using either 868MHz for the EMEA region of 915MHz for the USA and Canada.

<table><thead><tr><th width="157">Part Number</th><th width="208">Region</th><th width="161" data-type="checkbox">EnOcean</th><th data-type="checkbox">Workplace Occupancy</th></tr></thead><tbody><tr><td><strong>EXT00102</strong></td><td>EMEA (868MHz)</td><td>true</td><td>false</td></tr><tr><td><strong>EXT00110</strong></td><td>EMEA (868MHz)</td><td>false</td><td>true</td></tr><tr><td><strong>EXT00112</strong></td><td>EMEA (868MHz)</td><td>true</td><td>true</td></tr><tr><td><strong>EXT10102</strong></td><td>US (915MHz)</td><td>true</td><td>false</td></tr><tr><td><strong>EXT10110</strong></td><td>US (915MHz)</td><td>false</td><td>true</td></tr><tr><td><strong>EXT10112</strong></td><td>US (915MHz)</td><td>true</td><td>true</td></tr></tbody></table>

## Download Connector Firmware

### v3.1.1

{% file src="../../../.gitbook/assets/EXTxxxxx_v3.1.1.zip" %}

### v3.2.0

{% file src="../../../.gitbook/assets/EXTxxxxx_v3.2.0.zip" %}
