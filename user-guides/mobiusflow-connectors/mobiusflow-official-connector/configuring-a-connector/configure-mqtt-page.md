---
description: Configure the MQTT connection to MobiusFlow®
---

# Configure MQTT Page

MobiusFlow® connectors send and receive data via MQTT. You need to configure the MQTT settings to match the configuration you set in the [Configuring **Mobius**Flow®](../../configuring-mobiusflow-for-use-with-connectors.md) section of this guide.&#x20;

<figure><img src="../../../../.gitbook/assets/Screenshot 2023-03-10 at 16.17.12.png" alt=""><figcaption><p>MQTT configuration</p></figcaption></figure>

## MQTT Broker Settings

You can choose any MQTT **client ID** but this must be unique for your MQTT broker. The default is the connector's serial number

Enter the **IP Address** or **URL** of the MQTT broker. You do not need to specify MQTT:// or MQTTS:// before the URL

Enter the MQTT **Port** number. This is normally 1883 or 8883 for TLS enabled connections

If required enter the MQTT broker authorisation **Username** and **Password**. These can be left blank if no authentication is required

Enter the same pre-shared key (PSK) as you entered in the [Configuring **Mobius**Flow®](../../configuring-mobiusflow-for-use-with-connectors.md) section of this guide

## Security

If you are using TLS make sure you check the **TLS using CA Certificate** option. You must also set the correct **CA Server Certificate** on the [Manage Certificates](manage-certificates-page.md) page

You may also choose to use a Client Certificate and Key. Check this option if required and ensure that you have setup your client certificate and key on the [Manage Certificates](manage-certificates-page.md) page

## Save Settings

Once you have configured all MQTT settings click the **Save** button

Click the **Home** button on the settings saved confirmation page to return to the Home page
