---
description: >-
  Explaining how to use MobiusFlow Juniper Mist service to pull BLE data from
  the Mist network into MobiusFlow
---

# Juniper Mist

The MobiusFlow Juniper Mist service works by interfacing with a given site on the Juniper Mist cloud. It is currently not possible to connect directly to a Mist AP due to limitations of the Mist network itself.

The service is used to subscribe to BLE data updates within the Mist cloud.

{% hint style="info" %}
Note: For full data decryption, this service is designed to be used in conjunction with a BLE devices service. See [section explaining this](juniper-mist.md#use-with-ble-devices-service).
{% endhint %}

## Requirements from Mist Cloud

Find the following in Mist Cloud:

* **Site ID**: Most easily found by looking in the URL when browsed to the site on the Mist portal. The URL's take the form of https://**\<HOSTNAME>**/admin/?org\_id=\<ORG\_ID>#!psk/**\<SITE\_ID>**.
* **Region**: Use the **HOSTNAME** in the URL and the following table to find the region.

<table data-search="false"><thead><tr><th>HOSTNAME</th><th>Region</th></tr></thead><tbody><tr><td>manage.mist.com</td><td>Global 01</td></tr><tr><td>manage.gc1.mist.com</td><td>Global 02</td></tr><tr><td>manage.ac2.mist.com</td><td>Global 03</td></tr><tr><td>manage.gc2.mist.com</td><td>Global 04</td></tr><tr><td>manage.gc4.mist.com</td><td>Global 05</td></tr><tr><td>manage.eu.mist.com</td><td>EMEA 01</td></tr><tr><td>manage.gc3.mist.com</td><td>EMEA 02</td></tr><tr><td>manage.ac6.mist.com</td><td>EMEA 03</td></tr><tr><td>manage.gc6.mist.com</td><td>EMEA 04</td></tr><tr><td>manage.ac5.mist.com</td><td>APAC 01</td></tr><tr><td>manage.gc5.mist.com</td><td>APAC 02</td></tr><tr><td>manage.gc7.mist.com</td><td>APAC 03</td></tr></tbody></table>

* **Mist Authentication Key**: This can be created on the Mist portal in **Organization > Settings > API Token > Create Token**.

<figure><img src="../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

For most secure setup we recommend scoping the new API key as **Observer** of a **Specific Site** (the Site you're connecting to here).

<figure><img src="../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

## Configuration the Service

Add a Juniper Mist service to your MobiusFlow configuration:

<figure><img src="../../.gitbook/assets/Screenshot 2026-09-23 at 16.47.28.png" alt=""><figcaption></figcaption></figure>

Open the service settings of the new service:

<figure><img src="../../.gitbook/assets/Screenshot 2026-09-23 at 16.48.01.png" alt=""><figcaption></figcaption></figure>

Populate the settings you acquired from the Mist portal + Save:

<figure><img src="../../.gitbook/assets/Screenshot 2026-09-23 at 16.49.05.png" alt=""><figcaption></figcaption></figure>

Start the now configure service:

<figure><img src="../../.gitbook/assets/Screenshot 2026-09-23 at 16.49.57.png" alt=""><figcaption></figcaption></figure>

If the service connects and is operating correctly it will show:

<figure><img src="../../.gitbook/assets/Screenshot 2026-09-23 at 16.50.56.png" alt=""><figcaption></figcaption></figure>



## Use with BLE Devices service

The Juniper Mist service simply forwards raw BLE data. It does not perform any decoding. As such, once the service has received the data, it is forwarded to the MobiusFlow hub (via a BCMD BLE\_RX command). The hub will forward the data to any listening BLE devices services. The BLE devices service is where the raw BLE data is decoded and MobiusFlow objects are populated. [See full article on the BLE devices service here](ble-devices.md).

This means, to implement full end-to-end data transfer and decoding, this service is designed to be used in conjunction with the BLE Devices service.
