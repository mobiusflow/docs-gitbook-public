---
description: Learn how to control services
---

# Starting, Stopping, and Hot Reloading a Service

Services can be started and stopped individually and if enabled, and set to run at start, will start automatically whenever the MobiusFlow instance is started. &#x20;

{% hint style="info" %}
For more information on enabling services and setting them to run at start refer to the [Service Settings](service-settings.md) article.
{% endhint %}

Some services have [settings](service-settings.md) which affect how they operate e.g. the ports used by the MQTT broker service. These settings are typically only loaded on service start so changes to these settings may require a service to be stopped and started before they take effect. If a service is running and any critical settings are changed MobiusFlow Toolbox will notify you that a restart is required.

In addition to service settings changes requiring a restart, changes to object settings will only take affect if a service is restarted or if a hot reload takes place. Any objects that have changes requiring a restart or hot reload are highlighted in the service's [objects](../objects/) page.

{% hint style="warning" %}
A hot reload only applies changes to objects and does not apply any service settings changes
{% endhint %}

## Start, Stop, and Hot Reload Controls

The controls used to start, stop, and hot reload services are located on the service's card on the Services page and on the service's objects page. The buttons have the following icons (Start, Stop, Hot Reload).

<figure><img src="../../../.gitbook/assets/Start, stop, reload buttons (1).png" alt=""><figcaption></figcaption></figure>

## Starting a Service

Services are started by clicking on the start button.&#x20;

When a service starts it first creates all of its objects, loads in any [persisted data](value-persistence.md) (if enabled) and then runs any logic such as raw sensor data decoding. You can only access objects on running services.

{% hint style="info" %}
Disabled services cannot be started.
{% endhint %}

## Stopping a Service

Services are stopped by clicking on the stop button.

If a service has persistence enabled the current resource values will be persisted before the service stops.

When a service is stopped all of its objects will be destroyed and will no longer be available for reading or writing.

## Hot Reloading a Service

Adding objects or configuration changes to objects on running services will only take affect if a service is restarted or if the service is hot reloaded.&#x20;

Hot reloading a service does not stop it. Instead all objects that have configuration changes are refreshed and new objects are created without affecting any other objects.

## 💥 Interactive Demo

{% embed url="https://demo.mobiusflow.com/demo/cmiftxmx0cbotb7b4t9y7mpxs?utm_source=link" %}
