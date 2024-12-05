# Deploying MobiusFlow in MobiusFlow Cloud

For most use cases, Deploying MobiusFlow in the MobiusFlow Cloud is simplest and most cost effective hosting option.

Customers can create new MobiusFlow instances themselves using the MobiusFlow manager platform. A full guide on how to use this platform can be found [here](mobiusflow-manager.md).

{% hint style="warning" %}
MobiusFlow a hosting fee for hosting instances in the MobiusFlow cloud. As such, purchaser permissions are required.
{% endhint %}

When creating a new MobiusFlow instance using manager ensure the _Host instance on MobiusFlow Cloud_ option is checked:

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>MobiusFlow manager Instance creation wizard</p></figcaption></figure>

{% hint style="info" %}
If this option is not available, this is because you do not have purchaser permissions within this fleet.
{% endhint %}

On creation, there are several options that must be populated:

#### Hostname

This is the URL the new MobiusFlow cloud instance will be hosted on. In the above example, Manager has automatically suggested _average-pug-2488_. As such, new Cloud instance will be accessible at the URL _average-pug-2488.mobiusflow.io_.

#### Build Type

This selects the version of MobiusFlow to use. If use for the MobiusFlow LoRaWAN LNS is required, ensure the MobiusFlow V2 with LoRaWAN Stack option is selected.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

#### Region

This specifies the region of the world the new Cloud instance is to be hosted on. It is recommended to host the instance as near to where it will be used as possible.\\



Once a MobiusFlow Cloud hosted instance as online, an Environment is created, in-turn controlling how the instance can communicate with the outside world. A full article on this environment can be found [here](../technical-docs/mobiusflow-cloud-hosted-environment.md).&#x20;
