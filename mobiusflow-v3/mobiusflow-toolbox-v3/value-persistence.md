---
description: Configuring value persistence
---

# Value Persistence

Value persistence ensures that objects keep their values between restarts.&#x20;

In MobiusFlow versions before v3 any restart would cause all resources to be reset to their default values. This would often cause anomalies or loss of data such as all temperature values dropping to zero, meter readings being lost or people counts resetting.&#x20;

MobiusFlow 3 has solved this problem by adding optional value persistence. This can be configured on a service by service basis in the service settings. To access a service's settings follow the instructions [here](services/service-settings.md).

<figure><img src="../../.gitbook/assets/Service Settings Details.png" alt=""><figcaption></figcaption></figure>

When a service starts it first creates all objects with their default values and then applies any persisted values before running.&#x20;

## Enabling / Disabling Persistence

You can enable or disable persistence on each service. Changing the persistence enabled state will affect all objects belonging to that service.&#x20;

{% hint style="info" %}
If you wish to have persistence enabled only for some objects consider adding another service and putting splitting your objects between services
{% endhint %}

You can enable or disable persistence by clicking on the **Enable Persistence** switch in the service's settings.&#x20;

{% hint style="success" %}
If persistence is not required consider switching it off as it will add some CPU load.
{% endhint %}

Disabling persistence will also delete any persisted values. If you need to reset the persisted values you can disable and then re-enable persistence.

## Setting the Persistence Interval

In order to lower CPU load values are only persisted at regular intervals and not on every value change. You can set this interval (in minutes) in the service's settings. Try to find a reasonable balance between saving the current values and load on the system. The more objects a service has, the greater the CPU load required to persist the values.

{% hint style="info" %}
In addition to persisting values at a regular interval, values are also persisted when you manually stop a service.
{% endhint %}

## Default Settings

Services have persistence enabled with an interval of 5 minutes by default.

***

## 💥 Interactive Demo

{% embed url="https://demo.mobiusflow.com/demo/cmi69g6bv3u42b7b4oq79ymra?utm_source=link" fullWidth="false" %}
