---
description: License your MobiusFlow® instance
---

# Adding Your Licence

All **Mobius**Flow® instances require a valid licence to run. Licences define the maximum number of **Mobius**Flow® objects that you can add to an instance. For more information about **Mobius**Flow® licences refer to the [Licensing](../../technical-docs/licensing-v1.19.1-and-later.md) page.

## What You Will Need?

1. A valid MobiusFlow® licence (licences can only be used on one device)

## Adding Your Licence to a BalenaCloud Device

Licences are added to balenaCloud devices by setting a device variable. All required device variables are created automatically when you deploy **Mobius**Flow® to a fleet. For more information see [Device Variables](set-the-hub-id.md).

{% hint style="danger" %}
Licences must be added by **overriding a device's licence variable** and **NOT** changing the fleet's variables.
{% endhint %}

Navigate to your [balenaCloud dashboard](https://dashboard.balena-cloud.com/?) and login in

Navigate to the correct **fleet** and **device**

Select the **Device Variables** page. You will see a list of all of the device's variables with override buttons next to each variable

<figure><img src="../../.gitbook/assets/Balena Variables.png" alt=""><figcaption><p>Device Variables for a device</p></figcaption></figure>

Click the **override** button next to the **MOBIUS\_LICENCE** variable

In the popup delete the text _\<replace with your licence code> and_ **enter your licence code**&#x20;

Leave all other settings as their default values and click the **Add** button

<figure><img src="../../.gitbook/assets/Balena Set Licence.png" alt=""><figcaption><p>Add a licence code</p></figcaption></figure>

Your licence code will be shown in the Device Variables list (see [Device Variables](set-the-hub-id.md) for more information on all of the device variables shown in this list)

**Mobius**Flow® will **restart** to install the licence&#x20;

<figure><img src="../../.gitbook/assets/Balena Licence Entered.png" alt=""><figcaption><p>Licence entered</p></figcaption></figure>

## Updating or Replacing a Licence

{% hint style="info" %}
If you extend an expired licence or you purchase a larger licence you do not need to update the licence code
{% endhint %}

Under some circumstances it may be necessary to enter a new licence code. In order to make the new licence code work follow the procedure above to enter a new code

You will also need to tell **Mobius**Flow® to renew its licence by setting the Device Variable MOBIUS\_LICENCE\_RENEW to true

Click the **override** button next to the **MOBIUS\_LICENCE\_RENEW** variable

In the popup change the value from **false** to **true**&#x20;

Leave all other settings as their default values and click the **Add** button

Wait for **Mobius**Flow® to restart, confirm that the new licence is working and reset the Device Variable MOBIUS\_LICENCE\_RENEW to false

Click the **override** button next to the **MOBIUS\_LICENCE\_RENEW** variable

In the popup change the value from **true** to **false**&#x20;

Leave all other settings as their default values and click the **Add** button

{% hint style="success" %}
Congratulations, you have deployed your first **Mobius**Flow® device on balenaCloud.
{% endhint %}
