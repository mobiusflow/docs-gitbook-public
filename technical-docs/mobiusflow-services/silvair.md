---
description: >-
  This article explains how to use the MobiusFlow Silvair service for Silvair
  Cloud integration.
---

# Silvair

## Overview

The MobiusFlow Silvair service is used to pull data from the Silvair cloud. The Silvair cloud in-turn links with Silvair devices allowing MobiusFlow to directly receive data from these devices.

{% hint style="info" %}
As the Silvair cloud is online, note that, this service is only functional on online instances of MobiusFlow.
{% endhint %}

Each MobiusFlow Silvair service connects to a single Silvair project. As such, if multiple Silvair projects are required, use multiple MobiusFlow Silvair services.

The service gives the option to either allow the user to manually populate the devices, or simply automatically pull the devices found in a given Silvair project, into MobiusFlow.

To authenticate with the Silvair cloud, a Silvair user is required. It is a recommended a dedicated MobiusFlow be made within the Silvair cloud for MobiusFlow to use. This means you do not need to provide you personal account information to your MobiusFlow instance.

## Service Configuration

The following screenshots shows configuration settings for the service:

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

The following table explains the function of each setting field:

| Setting                       | Explanation                                                                                                                                                        |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Email                         | Email address of the Silvair user to authenticate against                                                                                                          |
| Password                      | Password of the Silvair user to authenticate against                                                                                                               |
| Partner ID                    | Your Silvair partner ID                                                                                                                                            |
| Project ID                    | The Silvair project ID this MobiusFlow service will interface with.                                                                                                |
| Object Dead Time              | The amount of time (in minutes) to elapse before a given Silvair object is considered dead. Further explained [here](silvair.md#dead-time). Set to 120 if unknown. |
| Auto Pull Config from Silvair | Controls whether or not Silvair devices from this project should be automatically pulled in when the services begins. In most cases, this is recommended.          |

## Checking Connection

When the settings are populate correctly, the service status will show that it is connected to the Silvair's WebSocket:

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Authentication Failure

In some cases the authentication can fail:

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

This can happen for two reasons.&#x20;

1. Either your username and password is incorrect, or your do not have the correct permission to access this project. If this is the case, please contact Silvair support.
2. Silvair limits the number of authentication attempts in a given time period. As such, if you've attempt many service restarts, or you've recently performed many logins using the credentials, this may cause the auth issue. If this is the case, wait 5 minutes and try again.

## Silvair Devices

Silvair devices provide many useful pieces of lighting information depending on the device.&#x20;

All Silvair devices are represented by a single MobiusFlow object type, profile 02C6 labelled as silvair\_luminaire.

Every Silvair devices has a unique node name. This is information is used in MobiusFlow to virtually link a MobiusFlow Silvair object to the real-world device.

### Manually Adding Silvair Devices

Adding a Silvair device manually requires the population of the Silvair Node Name for that device in the object settings:

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Once the service is started, if the Node Name exists in the Silvair project, MobiusFlow will automatically populate the object with any information the silvair device sends.

### Auto-Pulling Silvair Devices

Enabling Auto Pull in the service settings means MobiusFlow will automatically attempt to pull all the Silvair devices in the project into MobiusFlow objects. It will ensure they are kept synchronised so any changes made in the Silvair cloud will be reflected in MobiusFlow.

The Service will attempt to populate any useful information where it can, such as names and locations. If you choose to overwrite this information, the service will allow you to do so.

### Dead Time

The Dead Time, set within the services settings, controls how much time must elapse (in minutes) before the service considers a given device to be offline (dead).

This information is reflected in resource 17 of any child objects within the service:

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

This is useful in both the Flows and MobiusFlow view as it offers a quick and simple way to check if there is an issue with a given device.
