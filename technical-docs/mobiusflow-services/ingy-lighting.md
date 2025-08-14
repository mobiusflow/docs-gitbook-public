---
description: >-
  Article explaining how to use MobiusFlow INGY service. It is recommended you
  read this article in its entirety before using the MobiusFlow INGY
  integration.
---

# INGY Lighting

## Overview

The MobiusFlow INGY integration implements the following features:

* Changing lighting level set points of group scenes
* Switching between lighting scenes of a given group
* Adding / removing devices from groups
* Acquisition of data from INGY devices
* Direct interfacing with INGY API and Datastream

This article explains how to use the INGY service to achieve all of the above.

## Connecting to INGY Gateway

To interface with an INGY system, an INGY gateway must be present on the project site. These INGY gateways can be acquired directly from INGY.

### MQTT

MobiusFlow uses an MQTT connection to allow two-way communication between MobiusFlow and INGY.

INGY creates 3 MQTT user types, each with different sets of permissions. MobiusFlow requires usage of the _datastream_ and _MQTT JSON server_  (API) users.

### Connecting to Local INGY Gateway

Ensure the INGY gateway is accessible by MobiusFlow over an on-site (or otherwise) network. As it is likely the local IP address of the INGY gateway will be directly referenced within MobiusFlow, it is recommended that the INGY gateway's IP address should reserved so it does not get reassigned.

When configuring the service settings, ensure the 'Connect via INGY cloud' option is **unchecked**.

These MQTT user credentials can be found in the _Gateway MQTT server_ section of the INGY gateway configuration page.

### Connecting via INGY Cloud

In some situations, it may be suitable to connect to the INGY gateway over the internet. This is not recommended for any situation requiring control. In this case, contact INGY support to arrange them to set up both Datastream and API forwarding via their cloud. They will send you back the connection information.

When configuring the service settings, ensure the 'Connect via INGY cloud' option is **checked**.

### INGY Service Settings / Requirements

Once the INGY service has been added, the following configuration window is shown:

<figure><img src="../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

The following fields must be populated to allow MobiusFlow the connect the INGY gateway.

<table><thead><tr><th width="170">Setting</th><th>Explanation</th></tr></thead><tbody><tr><td>Connect via INGY Cloud</td><td>Checkbox to determine if MobiusFlow should connect to the gateway via INGY's cloud.</td></tr><tr><td>MQTT Broker</td><td>The IP location of the MQTT broker (IP address, DNS name, or otherwise). For MQTT over TLS include <em>mqtts://</em> prefix, otherwise, inclusion of protocol is not required. <strong>This is set if the 'Connect via INGY cloud' is checked</strong>.</td></tr><tr><td>MQTT Base Topic</td><td><strong>Only required if the Connect via INGY Cloud option is checked</strong>. In the form of &#x3C;CUSTOMER_NAME>/&#x3C;SITE_NAME>. This information can be aquired from INGY if unknown.</td></tr><tr><td>MQTT Port</td><td>Run by INGY on 1883 by default. <strong>This is automatically set if the 'Connect via INGY cloud' is checked</strong>.</td></tr><tr><td>MQTT Username (Datastream)</td><td>Found on INGY gateway configuration page.</td></tr><tr><td>MQTT Password (Datastream)</td><td>Found on INGY gateway configuration page.</td></tr><tr><td>MQTT Username (JSON API)</td><td>.Found on INGY gateway configuration page.</td></tr><tr><td>MQTT Password (JSON API)</td><td>Found on INGY gateway configuration page</td></tr><tr><td>INGY Firmware Version</td><td>85, 94, etc. To use mixed firmware versions, use multiple INGY services each with different firmware versions.</td></tr></tbody></table>

### Checking connection

The INGY service will attempt to connect via MQTT to the INGY gateway when the service is started. As such, to test the connection, start the service and observe the service status:

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption><p>Service status showing successful MQTT connection</p></figcaption></figure>

## Lighting Control

Lighting control is exclusively performed by commanding lighting groups to change to different scenes.

For every INGY lighting group, add an _ingy\_group_ (PID 028A) MobiusFlow object to represent the group within MobiusFlow. The group number of the INGY group can be set in the object settings.

{% hint style="warning" %}
Note that: If INGY groups have been pre-configured in the using the INGY App, ensure the group number matches that of group number displayed in the INGY App. See full section [here](ingy-lighting.md#groups-pre-configured-using-ingy-app).
{% endhint %}

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption><p>New INGY group object with a group number 7001486</p></figcaption></figure>

Viewing the resources on an INGY group object shows:

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

### Groups pre-configured using INGY App

If using a group the has been pre-configured using the INGY App, ensure the group number is MobiusFlow is set equal to the group number of the group previously created in the INGY App.

If a group with a matching group number has been set up within the INGY App, MobiusFlow will automatically pull (given some time) the _sceneSetLevel_ values of any scenes which have already been set up using the app.

The scene number matches the display order shown in the INGY App. As such, the first scene shown in the list on the INGY App is scene 0, the second is scene 1, the third is scene 2, and so on.

### Scene Settings

Each lighting group supports 8 different scenes (numbered 0 - 7). These may have been previously set up using the INGY app. MobiusFlow will automatically query the level set point of each scene and will display this in the corresponding _knownLevel_ resource. MobiusFlow can also be used to change each scene's level set point (0 - 100) by setting that scene's corresponding setLevel resource. The resource will indicate the message is being sent. To resend the message, simply set the resource again.

{% hint style="warning" %}
Note that: If the INGY App has been used to pre-set up some scenes, MobiusFlow will still allow you to change these settings. As such, it as advised to adhere to a common source of truth, either configuring all scenes within the INGY App or within MobiusFlow.
{% endhint %}

It may be possible that the real-world scene setting levels or MobiusFlow have become out of synchronous. This could have been caused if they were changed by something that was not MobiusFlow, such the INGY app or INGY API. To avoid this, consider periodically setting the setLevel resources to ensure the INGY groups are kept in sync.

### Changing Scene

MobiusFlow automatically queries which scene is currently being exhibited by the group, and shows this information in the _knownScene_ resource.

Changing the currently exhibited scene on a given group is done by setting the _sceneSetting_ resource to scene number of the desired scene. The resource will indicate the scene change message is being sent to the INGY group.

Alternatively, changing the current scene can be handled by using the INGY Set Scene flows node.

<figure><img src="../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

When configured, this node is pointed at an INGY group object, and will receive an input payload (0 - 7) representing the desired scene number. The node automatically handles the resource changes to cause the group to change scene.

## Devices and Querying

MobiusFlow objects can added to represent real-world INGY devices. These objects are used to query and encapsulate the data coming from these devices in addition to control which group a given device is a member of.

Searching _ingy_ in the objects library will display the list of options of MobiusFlow objects that can represent the real-world INGY devices.

<figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

Add these options in the correct quantities to represent the INGY devices within MobiusFlow.

Every INGY object type will require the entry of the INGY node address (wirepas address) as well some other information:

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

If knowing the current lighting level of any lighting device is required, ensure _Auto Query Level_ is checked to ensure MobiusFlow automatically pulls current level data from this device.

### INGY Partition

Some INGY nodes can be partitioned to act as separate controllable devices. Represent these partitions using multiple MobiusFlow objects with the same Node Address but different partition numbers. If the INGY node has not been partitioned, the partition number should be set to the default of 0.

### Grouping

The known group membership of all devices is automatically queried by MobiusFlow and this data is stored into _knownGroupMembership_ resource.

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

The group membership of a given device can be changed by setting the _setGroup_ resource. Once changed, the resource will show the set group message is being sent. The _knownGroupMembership_ resource should reflect this change after a period of time.

Sometimes it may be required that the command to group a given INGY device needs to be re-sent. This often can occur if the device is offline when the original setGroup command is sent. In this situation, simply set the _setGroup_ resource again. This will cause MobiusFlow to resend the set group command.

### Data

MobiusFlow will automatically pull all possible data from the known INGY nodes into corresponding MobiusFlow objects.

## Direct interfacing with INGY API

Two flow nodes have been written to aid direct interfacing with the INGY API.

{% hint style="info" %}
Note that all INGY flow nodes share the MobiusFlow connection configuration node. If this has not been created already, the node will prompt you to set up the connection between flows and MobiusFlow.
{% endhint %}

### INGY Spy Node

The INGY Spy node is used to view all the Datastream and API messages coming from INGY gateway. This includes data sent out over the INGY gateway's datastream as well as directly viewing all API commands and responses.

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

The INGY spy node can be aimed to a given MobiusFlow INGY service within it's config, and set up with debug nodes as shown above. The two outputs map to the datastream and api respectively.

### INGY Send API Command Node

The INGY send raw command node is used to send direct API command to the INGY API.

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

The node must be aimed at a specific MobiusFlow INGY service within the node's configuration.

The node takes input messages who's payload must be formatted to be a valid INGY API command as shown in the INGY API documentation. The response to this command will be outputted from the nodes output.

It is recommended a function is used to set the command body as shown in the example flow below:

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

In the above example the code in the function node is a as follows:

<pre class="language-javascript"><code class="lang-javascript"><strong>msg.payload = {
</strong>    version: 85,
    type: "volatile_partition",
    command: "QUERY_CAPABILITIES",
    destination: 'broadcast'
}
return msg;
</code></pre>
