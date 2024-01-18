---
description: Add your device to a balenaCloud fleet
---

# Adding Your First Device

## What You Will Need?

{% hint style="info" %}
This guide assumes you will be using a Raspberry Pi 4. The instructions are the same for the UP and Intel NUC devices with the exception of loading the initial balenaOS onto your device.

More information and instructions for adding other device types can be found [here](https://docs.balena.io/learn/getting-started/raspberrypi4-64/nodejs/).
{% endhint %}

1. A **balenaCloud account** with Microservices access (this requires a paid account)
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

Place your **microSD card** into your **SD card adaptor** and connect it to your laptop or PC

{% hint style="danger" %}
All data on your SD card will be overwritten!
{% endhint %}

Open **balenaEtcher**

Select **Flash from file** and choose the balenaOS image you downloaded above

Select your **SD card** as the **target**

Click on the **Flash** button

balenaEtcher will burn the balenaOS to your SD card and make it a bootable image. Wait for this to complete and for the image to be verified

Remove the **SD card** from the SD card adaptor and insert it into your **Raspberry Pi 4's SD card slot**

Plug the **Ethernet cable** into your Raspberry Pi 4's Ethernet port and your network

Power up your Raspberry Pi 4

## Confirming Your Device is Connected to balenaCloud

After a few minutes your new device will appear in the balenaCloud dashboard. Navigate to your balenaCloud dashboard, select your fleet and view the **fleet's Summary page**.

You device will be **added to the list** at the bottom of the page. It will be given a random name which you can change on the device's summary page

{% hint style="warning" %}
If your device does not appear in the list, check that it is powered up and that the network port you have it plugged into has an internet connection.
{% endhint %}

<figure><img src="../../.gitbook/assets/Balena Confirm Device Connected.png" alt=""><figcaption><p>Viewing the fleet's device list</p></figcaption></figure>

You have successfully added a new device to your balenaCloud fleet. To deploy **Mobius**Flow® to this device go to [Deploy **Mobius**Flow® to Your Fleet](deploy-mobiusflow-to-your-fleet.md)
