# Adding Your First Device

After signing up to [balena.io](https://www.balena.io) follow their instructions to create a fleet and add your first device. We have simplified the process so you will only need to perform some of the actions they list. The steps below outline the process but for more information see the balena.io [documentation](https://docs.balena.io/learn/getting-started/raspberrypi3/nodejs/#create-a-fleet).

## What You Will Need?

{% hint style="info" %}
This guide assumes you will be using a Raspberry Pi 4. The instructions are the same for the UP and Intel NUC devices with the exception of loading the initial balenaOS onto your device.
{% endhint %}

{% hint style="success" %}
Works with Windows® or macOS®
{% endhint %}

1. A **balena.io account** with Microservices access (this requires a paid account)
2. A **balenaCloud Raspberry Pi 4 Fleet** (see [Creating a Fleet](creating-a-fleet.md))
3. A **Raspberry Pi 4** with minimum 1Gb RAM and 8Gb storage (eMMC or microSD card. The following instructions are for an SD card)
4. A **power supply** for your Raspberry Pi 4
5. An **Ethernet network cable**
6. An internet router with a free Ethernet port (or an Ethernet port on your LAN with **internet access**)
7. An **SD card adaptor** for your laptop or PC
8. **balenaEtcher** installed on your laptop or PC. You can download balenaEtcher [here](https://www.balena.io/etcher)

## Adding a Device

Navigate to your [balenaCloud dashboard](https://dashboard.balena-cloud.com/?) and login in

Navigate to the **Fleets** page

Click on the fleet you want to add a device to

Click on the **Add device** button

<figure><img src="../../.gitbook/assets/Balena Add Device.png" alt=""><figcaption><p>Add a new device</p></figcaption></figure>

Leave all of the **default settings**. You can add a WiFi network (client or AP) later.&#x20;

Select the **Download balenaOS** option in the drop down button. The balenaOS will start to download

<figure><img src="../../.gitbook/assets/Balena Add Device Details.png" alt=""><figcaption><p>Add new device details</p></figcaption></figure>

## Burning the balenaOS onto the SD Card

Place your microSD card into your SD card reader and connect it to your laptop or PC

