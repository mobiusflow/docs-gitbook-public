---
description: Deploy MobiusFlow® to a balenaCloud fleet
---

# Deploy MobiusFlow® to Your Fleet

## What You Will Need?

1. A **balenaCloud account** with Microservices access (this requires a paid account)
2. A compatible balenaCloud fleet (Up Board, Intel NUC or Raspberry Pi 4)

{% hint style="danger" %}
You should always backup your MobiusFlow® device before deploying a new version.

See [Backup and Restore](../mobiusflow-r/backup-and-restore.md) for more details
{% endhint %}

## Deploying from balenaHub

{% hint style="info" %}
[BalenaHub](https://hub.balena.io/apps) is a market place for balena.io compatible applications ready to be deployed to your device with just a few clicks.
{% endhint %}

Navigate to your [balenaCloud dashboard](https://dashboard.balena-cloud.com/?) and login in

Navigate to [balenaHub](https://hub.balena.io/apps) to select which version of **Mobius**Flow® to deploy

Navigate to the **Apps** page

Search for **MobiusFlow**

<figure><img src="../../.gitbook/assets/BalenaHub Search.png" alt=""><figcaption><p>balenaHub search</p></figcaption></figure>

Select the correct **device type**

Click on the **Deploy** button

<figure><img src="../../.gitbook/assets/BalenaHub Deploy.png" alt=""><figcaption><p>Deploy MobiusFlow® to fleet</p></figcaption></figure>

Balena will switch to your **balenaCloud dashboard**

You can **create a new fleet** here or deploy to an **existing fleet**. If creating a new fleet refer to the [Creating a Fleet](creating-a-fleet.md) section for details on what settings are required

<figure><img src="../../.gitbook/assets/Balena Deploy to Fleet.png" alt=""><figcaption><p>Create new fleet or deplot to existing fleet</p></figcaption></figure>

If you already have a new fleet or want to upgrade the **Mobius**Flow® version on existing devices, select **Use an existing fleet instead**

<figure><img src="../../.gitbook/assets/Balena Deploy to Existing Fleet.png" alt=""><figcaption><p>Choose an existing fleet</p></figcaption></figure>

Select the fleet from the drop down and click on the **Deploy to fleet** button

After a few seconds you will see the **new release** being built for your fleet

<figure><img src="../../.gitbook/assets/Balena Build Release.png" alt=""><figcaption><p>New release building</p></figcaption></figure>

This will take a minute or two. Once the build is complete you will see the release on the dashboard. All devices, which have not been pinned to a specific release, in your fleet will automatically start to update to the new release.

You can also view the release history in the Releases page of your fleet.

<figure><img src="../../.gitbook/assets/Balena Release Built.png" alt=""><figcaption><p>New release deployed</p></figcaption></figure>

Click on a device Summary to see which release it is running. You can also pin device to specific releases on this screen

<figure><img src="../../.gitbook/assets/Balena Device Details - Release.png" alt=""><figcaption><p>Device details</p></figcaption></figure>

{% hint style="success" %}
Congratulations, you have deployed your first **Mobius**Flow® device on balenaCloud.

Go and grab a coffee before jumping into the **Mobius**Flow® user guide to see how easy it is to get sensors and more connected to your favourite applications...
{% endhint %}
