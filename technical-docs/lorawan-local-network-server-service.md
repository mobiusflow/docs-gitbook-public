---
description: Technical Documentation of how to use LoRaWAN Local Network Server
---

# LoRaWAN Local Network Server - Service

## Overview

You can add the LoRaWAN LNS Service (labelled as _lorawan local network server_) to the MobiusFlow from the service library.

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

The service requires the region to be set. If mulitple regions are required, using muliple LoRaWAN LNS services is neccessary.

{% hint style="info" %}
If muliple LoRaWAN LNS service are used on the same instance, both will use the same LNS backend.
{% endhint %}

### Integrated Device Types

If a device is integrated, MobiusFlow will atomically handle the decoding of device data and the movement of this data into corresponding MobiusFlow objects (Uplink). Some devices also support downlink, i.e. sending data from MobiusFlow to the device. For integrated device types, if there is a public downlink encoder available, MobiusFlow will automatically handle the encoding and sending of data to devices of that type.

#### List of Integrated Device Types

\<Coming soon>

#### Unintegrated Device Types

All LoRaWAN devices intend to be integrated in future. To request integration of a new device type, please contact MobiusFlow support at info@mobiusflow.com.

Data can still be received from and sent to unintegrated device types, however the users must handle data decoding and encoding manually. A full explanation of working with unintegrated device types can be found in [this section](lorawan-local-network-server-service.md#using-unintegrated-device-types).

### Supported Regions

Currently supported regions are shown in the following list:

* EU868
* US915\_0

Support for all regions is planned for the near future. To request support for a specific region, please contact MobiusFlow support at info@mobiusflow.com.

## Connecting a LoRaWAN Gateway to MobiusFlow

### Adding the Gateway to MobiusFlow

LoRaWAN gateways are added as MobiusFlow objects to the LoRaWAN LNS service. When viewing the configuration of LoRaWAN LNS service, search for lorawan\_gateway in the object library. A lorawan\_gateway object (PID 028D) should be added for each physical LoRaWAN gateway MobiusFlow will connect to.

For each lorawan\_gateway object, the 16 character (Hex) Gateway ID must be populated to match that of the ID of the physical LoRaWAN gateway. Ensure the object settings are saved. As with all MobiusFlow services, a stop/start cycle or hot reload must be performed if any settings are changed or  objects are added or removed.

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption><p>LoRaWAN LNS Service config, showing a newly added lorawan_gateway object and populated Gateway ID of AABBCCDDEE112233</p></figcaption></figure>

### Setting up the Connection on the Gateway

Ensure the MobiusFlow is accessible by the LoRaWAN gateway, i.e. if MobiusFlow is running in the cloud, ensure the gateway has an internet connection. Alternatively, if MobiusFlow is running on-prem, ensure the LoRaWAN gateway has access to it over the local network.

The connection between LoRaWAN gateway and MobiusFlow uses Semtech UDP. Set up a Semtech UDP packet forwarder on each gateway with the following paramaters.

#### Hostname

Use the standard TCP/IP hostname of the gateway. If the gateway is running in the cloud and hosted by MobiusFlow, it will be in the form _xxx.mobiusflow.io_ e.g. _grand-eagle-11.mobiusflow.io_. If MobiusFlow is being hosted on-prem or elsewhere, use the IP address of the host or DNS designation of the host. **Do not** include any protocol or a port in the hostname.

#### Port Number

The Semtech UDP packet forwarded allows both an inbound and outbound port to be specified in the configuration. Ensure the same port number is used for both inbound and outbound.

The exact port number depends on which region the gateway is operating in. See the table below for all port numbers by region.

| Region   | Port |
| -------- | ---- |
| EU868    | 1700 |
| US915\_0 | 1701 |

{% hint style="warning" %}
It is critical the correct port i used. The gateway may still be able to connect if the incorrect port is used, however this will cause the LNS to confuse the region of this gateway causing further problems.
{% endhint %}

#### Opening of Network Ports

Ensure the required ports are open on the gateway's network. Also ensure the required ports are open on the network where MobiusFlow is running. If the instance of MobiusFlow is hosted in the MobiusFlow cloud, the ports for all region types will be open by default.

## Connecting a LoRaWAN Device

To add a device, when inside the LoRaWAN LNS Service's configuration, search for that device type in the objects library and add instance of it.

For each new object, the Device EUI and Device App Key (OTAA Key) must be populate to match that of the device.

Ensure the settings are saved. As with all MobiusFlow services, a stop/start cycle or hot reload must be performed if any settings are changed or  objects are added or removed.

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption><p>LoRaWAN LNS Service config, showing a newly added MileSight VS121 Occupancy object and populated Device EUI of 112233445566AABB &#x26; Device App Key of 00000000000000000000000000000011</p></figcaption></figure>

If the credentials are set correctly, the device is in range of the LoRaWAN gateway, and the LoRaWAN gateway is connected to MobiusFlow, live decoded data from the device will now appear within the new object's resources.

## Downlink (Sending commands to a device)

The flows can be used to enqueue downlink messages to some device types. MobiusFlow is packaged with a set of MobiusFlow/LoRaWAN specific nodes designed to work with the LoRaWAN LNS service.

#### LoRaWAN Send Downlink Node

To enqueue downlink messages to device types that have been integrated with MobiusFlow, use the _lorawan send downlink_ node type shown below.

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

This node will accept into its input an incoming unencoded payload as per how the manufacture's downlink encoder accepts messages.

Inside the node's configuration allows specification of which device the downlink messages will be enqueued on. This is done by specifying the device's MobiusFlow URI which can either be pasted in or searched for.

<figure><img src="../.gitbook/assets/image (46).png" alt="" width="561"><figcaption><p>Populated node configuration with example URI 000001/020/0291/0002</p></figcaption></figure>

The node's output will send messages informing the user of the result of the attempted downlink enqueue action.

Results include a success, a failure due to an incorrectly structured input payload (included in the error message is information regarding the correct payload structure), or failure due to this device type not supporting downlink all together.

#### Checking Enqueued Messages

The number of  currently enqueued messages can be found for each device by viewing resource 21 of that object representing that device.

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption><p>Viewing the resources of a LoRaWAN device object on a LoRaWAN LNS service, noting resource 21 (enqueued count)</p></figcaption></figure>

#### Example Flow

The following example uses an inject input to trigger the inital message. Then a function node formats to message's payload into the correct format for the device type. The lorawan send downlink node has been set to connect to a specific MobiusFlow object. The debug is used to monitor the output of the lorawan send downlink node so the user is informed if the action was a success or failure.

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption><p>Simplest use of lorawan send downlink node</p></figcaption></figure>

The contents of the function node using to format the payload is follows:

```javascript
// this is an example
msg.payload = {
    config1: 0,
    config2: 3,
    mode: 'normal',
    action: 'open'
}
return msg;
```

### Raw Downlink

For some device types, manufactures do not release downlink encoders, and as such it is not possible to integrate this functionality into MobiusFlow. It is however possible to write your own in the flows and then send this via the LoRaWAN LNS service to be enqueued directly to a LoRaWAN device. This is done using same basic flow as regular downlink however using the _lorawan send raw_ node.

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption><p>Example flow use lorawan send raw node</p></figcaption></figure>

The lorawan send raw node bypasses helpers and checks provided by MobiusFlow objects. As such, the node's configuration requires the specification of a LoRaWAN device EUI instead of a MobiusFlow object's URI.

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption><p>Configuration of lorawan send raw node showing example device EUI of AABBCCDDEEFF1122</p></figcaption></figure>

The node does not have an output. This is because it uses a 'fire-and-forget' style mechanism and therefore cannot monitor if the action was successful or not.

The message payload must be fully encoded inside the function node. The result of this encoding must be a simple javascript string (not base 64 encoded). The LoRaWAN LNS service will automatically convert this into a string of bytes before the enqueue action.

The contents of the above example function node are shown below.

```javascript
function myEncoderFunction(payload) {
    // do the encoding
    let encodedPayload = payload;
    return encodedPayload;
}

// start with an unencoded payload
msg.payload = {
    some: 'this_is_not_encoded',
}

// ensure it is encoded into a string as per datasheet guidlines
msg.payload = myEncoderFunction(msg.payload) // encoded string
return msg;
```

## Using Unintegrated Device Types

Reading the sections on [connecting a device](lorawan-local-network-server-service.md#connecting-a-lorawan-device) and [downlink](lorawan-local-network-server-service.md#downlink-sending-commands-to-a-device) are recommended before reading this section.

For unintegrated device types, that is device types that MobiusFlow does not feature inbuilt uplink decoders, downlink encoders and shaped MobiusFlow objects, the _lorawan\_generic\_device_ object type can be used.

<figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption><p>lorawan_generic_device object configuration pane</p></figcaption></figure>

As with all LoRaWAN object, the device EUI and App Key must be set to match of the LoRaWAN device.

### Uplink

To the object's configuration is set with the correct device EUI and App Key, data will be pulled into the MobiusFlow object as with all other LoRaWAN object types. Unlike these object types, the data will not be decoded and left a raw string in resource 40. The data can then be handled / post-processed by the user  in the flows at will.

### Downlink

Downlink is handled in the same manner as for integrated device types. If using the lorawan\_send\_downlink node, for the lorawan\_generic\_device object type no checks are made regarding the format of the payload. As such, ensure the message is pre-encoded into a raw string. The LoRaWAN LNS will convert this into bytes before enqueuing the message.

The lorawan\_send\_raw node can also be used as before to enqueue downlink message to unintegrated device types.

## LNS Backend (Chirpstack)

The MobiusFlow LNS Service uses Chirpstack V4 as an LNS backend. As such, for debugging purposes it is possible to log into this backend if required. Chirpstack runs on port 8081, to browse to this port to access chirpstack.

Every MobiusFlow LNS Service contains a statistics object. This includes some information about the health of the LNS as well as the chirpstack login credentials.

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption><p>LNS Stats Object Resources</p></figcaption></figure>
