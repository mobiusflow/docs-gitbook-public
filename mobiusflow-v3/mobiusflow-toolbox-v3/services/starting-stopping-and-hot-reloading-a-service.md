---
description: Learn how to control services
---

# Starting, Stopping, and Hot Reloading a Service

Services can be started and stopped individually and if enabled and set to run at start will automatically start whenever the MobiusFlow instance is started. &#x20;

{% hint style="info" %}
For more information on enabling services and setting them to run at start refer to the [Service Settings](service-settings.md) article.
{% endhint %}

When a service starts it first creates all of its objects, loads in any [persisted data](value-persistence.md) (if enabled) and then runs any logic such as raw sensor data decoding. You can only access objects on running services.

Some services have [settings](service-settings.md) which affect how they operate e.g. the ports used by the MQTT broker service. These settings are typically only loaded on service start so changes to these settings may require a service to be stopped and started before they take effect. If a service is running and any critical settings are changed MobiusFlow Toolbox will notify you that a restart is required.

In addition to service settings changes requiring a restart, changes to object settings will only take affect if a service is restarted or if a hot reload takes place. Any objects that have changes requiring a restart or hot reload are highlighted in the service's [objects](../objects.md) page.

{% hint style="warning" %}
A hot reload only applies changes to objects and does not apply any service settings changes
{% endhint %}

## Starting Services

Any services that are stopped can be started from the&#x20;
