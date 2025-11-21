---
description: Configuring services
---

# Service Settings

To update a service's settings, first click on Services in the main menu and then find the correct service card.

On the service card toolbar click on the **Settings** button to open the service settings dialog.

<figure><img src="../../../.gitbook/assets/Default service settings.png" alt=""><figcaption></figcaption></figure>

The service settings dialog is shown above. All services have these default settings, but some services may have additional service specific settings. It is beyond the scope of this article to describe any service specific settings, please see the article for that specific service type for more information.

{% hint style="success" %}
Some service settings changes may require a service restart to take effect. If a service is running you will be notified if you need to restart the service
{% endhint %}

## General Settings

### SID

The SID or Service ID is a three digit hexadecimal number. It forms part of a [MobiusFlow Uniform Resource Identifier](../../mobiusflow-overview/mobiusflow-uniform-resource-identifiers-uris.md).

When a service is [added](adding-services.md) it is given the next available SID, but this can be changed if required. SIDs must be unique within a MobiusFlow instance so you cannot assign a service an existing SID.

### Name

The service name can be freely assigned. It has no relevance within a MobiusFlow instance and is just used in MobiusFlow Toolbox to make it easier for you to distinguish between your services.

### Enable Service

Services can be Enabled or Disabled. Disabled services do not run at startup and cannot be manually started.

### Run at Start

If a service is enabled and it is set to Run at Start the service will be automatically started when the MobiusFlow instance starts. If Run at Start is switched off for a service it will not start automatically but can be started manually by clicking on the service's start button.

## Value Persistence

Value persistence ensures that objects keep their values between restarts. Please see the [Value Persistence](../value-persistence.md) article for more information.

## Logging Levels

A service and its underlying connection to the rest of the instance (the spoke) each have their own logging levels. Currently these logs are only visible in the terminal on the computer running the MobiusFlow instance and are not visible in Toolbox. We aim to make this available in a future version for developers.&#x20;

The default logging levels are set to Info. Please do NOT change these unless instructed by a MobiusFlow engineer during a support incident as excessive logging could cause significant additional CPU load.

## Service Specific Settings

Some services have their own service specific settings. The exact settings will depend on the service type. These are shown at the bottom of the service settings dialog. An example for the MQTT Broker service is shown below.

<figure><img src="../../../.gitbook/assets/Service specific settings.png" alt=""><figcaption></figcaption></figure>

## 💥 Interactive Demo

{% embed url="https://demo.mobiusflow.com/demo/cmi7m8wp55gnsb7b4mp65riif?utm_source=link" %}
