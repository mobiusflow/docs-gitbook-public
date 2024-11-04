---
description: How to convert a Raspberry Pi into a MobiusFlow Connector
---

# Converting Raspberry Pi to a MobiusFlow Connector

## Hardware Requirements

### Raspberry Pi

A Raspberry Pi is required. Currently support Raspberry Pi models include:

* Raspberry Pi 4
* Raspberry Pi 5

An SD card for each Raspberry Pi is also required to store the connector image. We recommend a minimum storage of 16GB.

### Transceivers / Interfacing Hardware

Most protocol types require specific hardware to translate that protocol to the Raspberry Pi.

#### EnOcean

The following transceivers are supported. Only 1 is required per Pi:

<table><thead><tr><th width="315">Transceiver </th><th></th></tr></thead><tbody><tr><td>TCM310 Pi Hat</td><td>868MHz (Europe) EnOcean transceiver to plug into Raspberry Pi header</td></tr><tr><td>TCM310U Pi Hat</td><td>902MHz (North America) EnOcean transceiver to plug into Raspberry Pi header</td></tr><tr><td>USB 300 Stick</td><td>868MHz (Europe) EnOcean transceiver to plug into Raspberry Pi USB Port</td></tr><tr><td>USB 300U Stick</td><td>902MHz (North America) EnOcean transceiver to plug into Raspberry Pi USB Port</td></tr></tbody></table>

## Etching SD Image

MobiusFlow Raspberry Pi connectors can offer remote access functionality via BalenaCloud, however this is not required. As such, the hosting options of the connector must be considered.

### Hosting Options

<table><thead><tr><th width="152">Balena Cloud Option</th><th width="154">Remote Access</th><th width="130">Cost</th><th>Setup Complexity</th></tr></thead><tbody><tr><td>MobiusFlow Hosted</td><td>Yes</td><td>Recurring Payment</td><td>Simple</td></tr><tr><td>Self Hosted</td><td>Yes</td><td>See <a href="https://www.balena.io/pricing">BalenaCloud pricing</a>.</td><td>Requires setup of a Balena Cloud account and Fleet</td></tr><tr><td>Not Hosted</td><td>No</td><td>None</td><td>Simple</td></tr></tbody></table>

#### MobiusFlow Hosted

The following images can be downloaded for etching:

| Board          | Image Download                |
| -------------- | ----------------------------- |
| Raspberry Pi 4 | Coming Soon - Contact Support |
| Raspberry Pi 5 | Coming Soon - Contact Support |

#### Self Hosted

The following is an overview of the steps involved:

* Create BalenaCloud Account
* Create BalenaCloud Fleet
* Attach BalenaCloud Fleet to the corresponding MobiusFlow Connector Balena Application
* Add a new device to the fleet and download the subsequent Balena image
* Etch the image

We have a full guide on how to use the BalenaCloud with MobiusFlow itself [here](../../deploying-mobiusflow-on-prem/deploying-mobiusflow-to-dedicated-hardware-using-balenacloud/). Please note this differs in the context of MobiusFlow Connectors because the BalenaCloud Fleets should be linked to the MobiusFlow Connector BalenaCloud applications instead of the standard MobiusFlow BalenaCloud applications.

#### Not Hosted

| Board          | Image Download                |
| -------------- | ----------------------------- |
| Raspberry Pi 4 | Coming Soon - Contact Support |
| Raspberry Pi 5 | Coming Soon - Contact Support |

### Etching

We recommend using the [Balena Etcher tool](https://etcher.balena.io/) to etch the images onto an SD Card. The tool is self-explanatory, but full full documentation of how to use the tool can be found [here](https://etcher-docs.balena.io/).

