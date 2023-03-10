---
description: Configure a MobiusFlow® instance for connectors
---

# Configuring MobiusFlow®

## What You Will Need?

1. Your connector's serial number (see label on bottom of connector)
2. A running instance of **Mobius**Flow®
3. A configured MQTT broker (this is usually an MQTT broker running in your **Mobius**Flow® instance

The configuration screenshots in the guide assume you are using an MQTT broker running in the same instance of **Mobius**Flow®. You should adjust the configuration to suit your setup. An example of the broker configuration is shown below

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-10 at 13.22.20.png" alt=""><figcaption><p>Example configuration of an MQTT broker</p></figcaption></figure>

## Configuring MobiusFlow®

Login in to your MobiusFlow® instance and navigate to the **Configuration** tab

Drag a **mobius connectors** service from the palatte on the left into the centre configuration tree

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-10 at 13.25.34.png" alt=""><figcaption><p>Add mobius connectors service</p></figcaption></figure>

Ensure that **Enabled** and **Run At Start** or ticked and optionally  add a service description

In the **MQTT Broker field** enter the I**P address** or fully qualified domain name (**FQDN**) of your MQTT broker. If you are using a broker configured in the same **Mobius**Flow® instance enter _localhost_

{% hint style="info" %}
If you are using an MQTT broker running in the same MobiusFlow® instance enter _localhost_ into the MQTT Broker field.

You can prefix your broker name with MQTTS:// to enable TLS for this connection e.g. MQTTS://my-broker.com
{% endhint %}

Enter the port that the broker is listening on into the **MQTT Port field**

{% hint style="info" %}
This is usually **1883** for unsecured connections or **8883** for TLS connections.

If you entered _localhost_ into the field above use 1883
{% endhint %}

If your MQTT broker requires a username and password for authentication enter these into the **MQTT Username** and **MQTT Password** fields. You can leave these two fields blank if your MQTT broker does not require them

Click **Save Changes**

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-10 at 13.26.43.png" alt=""><figcaption><p>Configured service</p></figcaption></figure>

Search for a **mobiusFlowConnector** **object** in the left hand palatte and drag one onto the **mobius connectors service** you have just configured

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-10 at 13.28.00.png" alt=""><figcaption><p>Add a mobiusFlowConnector object</p></figcaption></figure>

Optionally change the Name, and add a Description and Location. Leave the default Instance and Parent field values

{% hint style="info" %}
Changing the **Name** will make it easier to find the connector in the diagnostics tab
{% endhint %}

In the **Serial Number field** enter the serial number of the connector you are adding. This can be found on the label on the bottom of the connector and usually starts MF\_00

The connection between the connector and the **Mobius**Flow® instance is authorised and encoded with a pre-shared key (**PSK**) or password. You can freely define this PSK but the same key must be entered into the **Mobius**Flow® configuration **and** the corresponding connector.

{% hint style="info" %}
We recommend a difficult to guess pre-shared key of at least 16 characters
{% endhint %}

Click **Save Changes**

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-10 at 14.11.40.png" alt=""><figcaption><p>Configure connector serial number and pre-shared key</p></figcaption></figure>

## Starting the mobius connectors Service

Navigate to the Diagnostics page

Click on the mobius connectors service **start button** ▶️

The service will start and show that it has connected to the MQTT broker

<div>

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-10 at 14.13.16.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-10 at 14.13.25.png" alt=""><figcaption></figcaption></figure>

</div>

{% hint style="danger" %}
If you make any changes to the mobius connectors service, any configured connectors, or add a new connector you should restart the mobius connectors to make the new configuration take effect
{% endhint %}
