---
description: How to convert a Raspberry Pi into a MobiusFlow Connector
---

# Converting Raspberry Pi to a MobiusFlow Connector

## Hardware Requirements

### Raspberry Pi

A Raspberry Pi is required. Currently supported Raspberry Pi models include:

* Raspberry Pi 4
* Raspberry Pi 5

An SD card for each Raspberry Pi is required to store the connector image. We recommend a minimum storage of 8GB.

### Transceiver Hardware

Most protocol types require specific hardware to translate that protocol to the Raspberry Pi.

#### EnOcean

The following transceiver types are supported. Only 1 is required per Pi:

<table><thead><tr><th width="315">Transceiver </th><th></th></tr></thead><tbody><tr><td>TCM310 (Pi Hat)</td><td>868MHz (Europe) EnOcean transceiver to plug into Raspberry Pi header</td></tr><tr><td>TCM310U (Pi Hat)</td><td>902MHz (North America) EnOcean transceiver to plug into Raspberry Pi header</td></tr><tr><td>USB 300 (USB Stick)</td><td>868MHz (Europe) EnOcean transceiver to plug into Raspberry Pi USB Port</td></tr><tr><td>USB 300U (USB Stick)</td><td>902MHz (North America) EnOcean transceiver to plug into Raspberry Pi USB Port</td></tr></tbody></table>

## Etching SD Image

### BalenaCloud

MobiusFlow Raspberry Pi connectors can offer remote access functionality via BalenaCloud, however this is not required.

The following is an overview of the steps involved:

1. Create BalenaCloud Account
2. Create BalenaCloud Fleet
3. Attach BalenaCloud Fleet to the corresponding MobiusFlow Connector Balena Application
   * Raspberry Pi 4 Application
   * Raspberry Pi 5 Application
4. Add a new device to the fleet and download the subsequent Balena image
5. Etch the image

We have a full guide on how to use the BalenaCloud with MobiusFlow itself [here](../../deploying-mobiusflow-on-prem/deploying-mobiusflow-to-dedicated-hardware-using-balenacloud/). Please note this differs in the context of MobiusFlow Connectors because the BalenaCloud Fleets should be linked to the MobiusFlow Connector BalenaCloud applications instead of the standard MobiusFlow BalenaCloud applications.

### Etching

We recommend using the [Balena Etcher tool](https://etcher.balena.io/) to etch the images onto an SD Card. The tool is self-explanatory, but full full documentation of how to use the tool can be found [here](https://etcher-docs.balena.io/).

BalenaCloud charges hosting fees when more than 5 devices are associated to the account. If remote access to the Connector confiruation is not required, the device can be deleted from the BalenCloud fleet. The Connector software running on the device will remain, and the device will operate as normal.

