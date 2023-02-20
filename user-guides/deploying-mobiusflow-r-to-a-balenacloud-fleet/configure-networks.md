---
description: Configure the network interfaces for a balenaCloud device
---

# Configure Networks

The configuration of the network interfaces of a **Mobius**Flow® balenaCloud device is handled by the **manage** microservice. All configuration is stored in a JSON file which can be updated by plugging in a properly configured **USB memory stick** or through the **balenaCloud device terminal**.

## Network Configuration File Structure

{% hint style="warning" %}
As each device type has different configurations and names for the underlying network interfaces, the structure of the network configuration may differ depending on the device type you are using
{% endhint %}

{% tabs %}
{% tab title="Aaeon Up / Intel NUC" %}
```json
[
  {
    "connection": {
      "enabled": true,
      "type": "ethernet",
      "id": "Wired connection 1",
      "interface-name": "enp2s0"
    },
    "ipv4": {
      "method": "auto",
      "address": "",
      "prefix": 24,
      "gateway": "",
      "dns": ""
    }
  },
  {
    "connection": {
      "enabled": true,
      "type": "ethernet",
      "id": "Wired connection 2",
      "interface-name": "enp3s0"
    },
    "ipv4": {
      "method": "manual",
      "address": "192.168.1.100",
      "prefix": 24,
      "gateway": "",
      "dns": ""
    }
  },
  {
    "connection": {
      "enabled": false,
      "type": "wifi",
      "id": "WiFi connection 1",
      "interface-name": "wlp4s0"
    },
    "ipv4": {
      "method": "auto",
      "address": "",
      "prefix": 24,
      "gateway": "",
      "dns": ""
    },
    "wifi": {
      "ssid": ""
    },
    "wifi-security": {
      "psk": "",
      "auth-alg": "open",
      "key-mgmt": "wpa-psk"
    }
  },
  {
    "connection": {
      "enabled": false,
      "type": "hotspot",
      "id": "WiFi hotspot 1",
      "interface-name": "wlp4s0"
    },
    "wifi": {
      "ssid": "",
      "channel": 6
    },
    "wifi-security": {
      "psk": "",
      "key-mgmt": "wpa-psk"
    }
  },
  {
    "connection": {
      "enabled": true,
      "type": "gsm",
      "id": "GSM connection 1",
      "interface-name": "cdc-wdm0"
    },
    "gsm": {
      "apn": "arkessa.com",
      "username": "arkessa",
      "password": "arkessa"
    }
  }
]
```
{% endtab %}

{% tab title="Raspberry Pi 4" %}
```json
[
  {
    "connection": {
      "enabled": true,
      "type": "ethernet",
      "id": "Wired connection 1",
      "interface-name": "eth0"
    },
    "ipv4": {
      "method": "auto",
      "address": "",
      "prefix": 24,
      "gateway": "",
      "dns": ""
    }
  },
  {
    "connection": {
      "enabled": false,
      "type": "wifi",
      "id": "WiFi connection 1",
      "interface-name": "wlan0"
    },
    "ipv4": {
      "method": "auto",
      "address": "",
      "prefix": 24,
      "gateway": "",
      "dns": ""
    },
    "wifi": {
      "ssid": ""
    },
    "wifi-security": {
      "psk": "",
      "auth-alg": "open",
      "key-mgmt": "wpa-psk"
    }
  },
  {
    "connection": {
      "enabled": false,
      "type": "hotspot",
      "id": "WiFi hotspot 1",
      "interface-name": "wlan0"
    },
    "wifi": {
      "ssid": "",
      "channel": 6
    },
    "wifi-security": {
      "psk": "",
      "key-mgmt": "wpa-psk"
    }
  }
]
```
{% endtab %}
{% endtabs %}

## Editing the Network Configuration

### Using the balenaCloud Device Terminal

Navigate to your [balenaCloud dashboard](https://dashboard.balena-cloud.com/?) and login in

Navigate to the **Device Summary** page of the device you want to configure

Open a terminal in the manage microservice

<figure><img src="../../.gitbook/assets/Balena Manage Terminal.png" alt=""><figcaption><p>balenaCloud device manage terminal</p></figcaption></figure>

Change to the **/data/.mobius/manage** directory and edit the **networks.json** file by running the following commands:

```shell
cd /data/.mobius/manage
vi networks.json
```

This will open the network configuration file for editing using the **vi editor**

<figure><img src="../../.gitbook/assets/Balena Edit Networks.png" alt=""><figcaption><p>Edit networks.json file</p></figcaption></figure>

Make any required changes and save the file

**Exit** the terminal and **restart the manage microservice** by clicking on the **restart** icon next to the manage service

<figure><img src="../../.gitbook/assets/Balena Microservices.png" alt=""><figcaption><p>Restart the manage microservice</p></figcaption></figure>

{% hint style="danger" %}
Be careful when changing the network interface you are using to connect the device to the internet as you could prevent the device from connecting to balenaCloud.
{% endhint %}

### Using a USB Memory Stick

Using a USB memory stick to update the network interfaces is useful when none of the network interfaces is configured to connect to the internet so it is not possible to use the balenaCloud device terminal. You will obviously need physical access to the device to use this method.

Format the USB memory stick as **FAT32**

Rename the USB memory to **MOBIUSCONF**

Create a file on the USB memory stick called **networks.json**

Open the file on your laptop or PC in your favourite text editor and paste in the correct JSON configuration from the examples above

Make any required changes

Save the file and unplug the USB memory stick from your laptop or PC

Plug the USB memory stick into any of the USB ports on your device

Reboot your device

When the device reboots it will copy the **networks.json** onto the device and use the new configuration for its network interfaces (this will take a minute or two)

You can then remove the USB memory stick and your device will continue to use the new network configuration.
