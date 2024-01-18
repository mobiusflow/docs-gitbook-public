---
description: Configure a connector to connect to a MobiusFlow® instance
---

# Configuring a Connector

## What You Will Need?

1. A device with a **web browser** such as a laptop, tablet or smart phone, capable of connecting to a **2.4GHz WiFi** access point
2. A SIM card removal tool, large paper clip or pin to push the configuration mode button
3. A powered **Mobius**Flow® connector
4. The connector's **Serial Number**

## Enabling Configuration Mode

{% hint style="warning" %}
If you leave the connector in configuration mode for more than 5 minutes it will automatically reboot and leave configuration mode
{% endhint %}

The connector's configuration mode can be enabled in two ways:

### Using the Configuration button

Using a pin hold in the **configuration mode button** (inside the small hole to the right of the USB connector) on the front panel for **2 seconds**

Release the button and the **green LED** will flash rapidly

Using your laptop / tablet / smartphone look for a **WiFi network** with the same name as the connectors serial number

Connect to this network and enter the connector's **Config Mode Password**. The default is _**mobiusflow**_

Open a web browser on your laptop / tablet / smartphone and enter **http://192.168.4.1** into the browsers address bar and hit enter&#x20;

The web browser will show the connector's configuration Home page

### Using a Web Browser

{% hint style="info" %}
This method is only available if you already know the IP address of the connector
{% endhint %}

Make sure that the connector and your laptop / tablet / smart phone are connected to the same Ethernet network

Open a web browser and browse to **\<your connector IP address>:8080** e.g. 192.168.1.20:8080

You will need to enter a user name and password. The user name is **admin** and the password is the same as the connector's **Config Mode Password**. The default is _**mobiusflow**_

After a short delay the web browser will redirect to the connector's configuration Home page

