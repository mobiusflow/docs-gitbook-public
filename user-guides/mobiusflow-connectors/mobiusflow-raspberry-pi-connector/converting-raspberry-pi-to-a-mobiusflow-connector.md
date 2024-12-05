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

<table><thead><tr><th width="315">Transceiver </th><th>Notes</th></tr></thead><tbody><tr><td>TCM310 (Pi Hat)</td><td>868MHz (Europe) EnOcean transceiver to plug into Raspberry Pi header</td></tr><tr><td>TCM310U (Pi Hat)</td><td>902MHz (North America) EnOcean transceiver to plug into Raspberry Pi header</td></tr><tr><td>USB 300 (USB Stick)</td><td>868MHz (Europe) EnOcean transceiver to plug into Raspberry Pi USB Port</td></tr><tr><td>USB 500U (USB Stick)</td><td>902MHz (North America) EnOcean transceiver to plug into Raspberry Pi USB Port</td></tr></tbody></table>

## Etching SD Image

### BalenaCloud

MobiusFlow Raspberry Pi connectors run Balena OS. Athlough not required, if your organisation registers with BalenaCloud, Balena OS grants a direct VPN link to the connector, allowing configuration changes to be made over the internet.

When using more than 5 devices, BalenaCloud becomes a piad service. As such, we offer versions of the Balena images which do not support remote access and therefore do not require a subscription to BalneaCloud.

#### Without Remote Access

The following, no remote access images can be downloaded:

* [Raspberry Pi 4](https://mobiusflow.sharepoint.com/:u:/g/Eeg0HjyTqIJEvQW3bsOuSZkBWRlkcebyY64EEif75gB6cw?e=PJPDjm)
* [Raspberry Pi 5](https://mobiusflow.sharepoint.com/:u:/g/EeKlod_6xSVCuraKTxFosuEBh3OMTv9BKuuO2IfnyDrKoA?e=riMiFt)

#### With Remote Acccess

The following is an overview of the steps involved to use BalenaCloud with MobiusFlow RPI connectors:

1. Create BalenaCloud Account
2. Create BalenaCloud Fleet
3. Attach BalenaCloud Fleet to the corresponding MobiusFlow Connector Balena Application
   * [Raspberry Pi 4 Application](https://hub.balena.io/apps/2199438/mobiusflow-connector-rpi4)
   * [Raspberry Pi 5 Application](https://hub.balena.io/apps/2199441/mobiusflow-connector-rpi5)
4. Add a new device to the fleet and download the subsequent Balena image
5. Etch the image

We have a full guide on how to use the BalenaCloud with MobiusFlow itself [here](../../deploying-mobiusflow-on-prem/deploying-mobiusflow-to-approved-hardware-using-balenacloud/). Please note&#x20;

{% hint style="info" %}
The above guide differs in the context of MobiusFlow Connectors because the BalenaCloud Fleets should be linked to the MobiusFlow Connector BalenaCloud applications, instead of the standard MobiusFlow BalenaCloud applications.
{% endhint %}

### Etching

We recommend using the [Balena Etcher tool](https://etcher.balena.io/) to etch the images onto an SD Card. The tool is self-explanatory, but full full documentation of how to use the tool can be found [here](https://etcher-docs.balena.io/).

BalenaCloud charges hosting fees when more than 5 devices are associated to the account. If remote access to the Connector confiruation is not required, the device can be deleted from the BalenCloud fleet. The Connector software running on the device will remain, and the device will operate as normal.

