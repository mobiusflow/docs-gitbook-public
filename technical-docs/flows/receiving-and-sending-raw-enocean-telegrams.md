# Receiving and Sending Raw EnOcean Telegrams

This article aims to explain how raw EnOcean telegrams can be sent and received within MobiusFlow. The article briefly covers the supported telegram types and illustrates how these types affect the setup of a given flow.

## Receiving <a href="#receiving" id="receiving"></a>

### Overview <a href="#overview" id="overview"></a>

EnOcean telegrams can be received and injected into a given flow using the Subscribe to Broadcast Command node, labeled 'sub bcmd'. This node is shown below.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="195"><figcaption><p>Sub bcmd node</p></figcaption></figure>

Within the node's configuration, you can specify a Mobius Command ID. This Command ID controls which type of incoming telegrams the node receives.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt="" width="467"><figcaption><p>Sub bcmd node configuration pane</p></figcaption></figure>

Once an incoming telegram of the specified type is detected by the sub bcmd node, the node will forward this telegram out of its output.

### Command Types <a href="#command_types" id="command_types"></a>

The table below shows which Command ID entries relate to which telegram types. The table also shows screenshots of each Command ID being used within the sub bcmd node configuration.

<table data-header-hidden><thead><tr><th width="158.33333333333331"></th><th width="260"></th><th></th></tr></thead><tbody><tr><td><strong>Type</strong></td><td><strong>Command ID</strong></td><td><strong>Example Screenshot</strong></td></tr><tr><td><p>ERP1</p><p>(EnOcean Radio Protocol 1- Fixed Length)</p></td><td>ENOCEAN_RADIO_ERP1</td><td><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt="" data-size="original"></td></tr><tr><td>ERP1 VLD (EnOcean Radio Protocol 1 - Variable Length</td><td>ENOCEAN_RADIO_ERP1_VLD</td><td><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt="" data-size="original"></td></tr><tr><td>MSC (Manufactuere Specific Commands)</td><td>ENOCEAN_RADIO_MSC</td><td><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1).png" alt="" data-size="original"></td></tr><tr><td>RMC (Remote Management Command)</td><td>ENOCEAN_RADIO_RMC</td><td><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1).png" alt="" data-size="original"></td></tr></tbody></table>

### Example <a href="#example" id="example"></a>

In this example, a Sub BCMD node is used to subscribe to incoming EnOcean RMC telegrams. The sub bcmd node is linked to a debug node to allow the telegram to be displayed. This setup is shown in the flow below.

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1).png" alt="" width="399"><figcaption></figcaption></figure>

The configuration of the sub bcmd node is shown below.

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1).png" alt="" width="467"><figcaption><p>Sub bcmd node configured to respond to ENOCEAN_RADIO_RMC telegrams</p></figcaption></figure>

## Sending <a href="#sending" id="sending"></a>

This sections covers how to send EnOcean telegrams using the MobiusFlow Connector hardware.

{% hint style="warning" %}
Note that, sending is only support for MobiusFlow Connectors running firmware version v3.2.0 or later. Downloads links to the firmware version can be found [here](../../user-guides/mobiusflow-connectors/mobiusflow-official-connector/#download-connector-firmware).
{% endhint %}

### MobiusFlow Versions v1.x.x (v1.19.9 and newer) <a href="#sending" id="sending"></a>

EnOcean telegrams can be sent from the flows using the Send Broadcast Command node, labeled 'send bcmd'. This node is shown below.&#x20;

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt="" width="152"><figcaption><p>Send bcmd node</p></figcaption></figure>

On opening the node's configuration, a Command ID is required to specify the function of the node. To allow the node to send EnOcean telegrams, the Command ID should read 'ENOCEAN\_RADIO\_TX'. This is shown in the configuration window below.

<figure><img src="../../.gitbook/assets/image (8) (1) (1).png" alt="" width="468"><figcaption><p>Send bcmd node configured EnOcean telegrams</p></figcaption></figure>

The node accepts and forwards data contained within the **payload** of incoming messages. The appropriate incoming message structure is shown below.

```javascript
msg.payload = {
 connectorURI: /*(Connector MobiusFlow URI)*/,
 rawData: /*(Command Data)*/,
}
```

<table><thead><tr><th width="160">Property</th><th>Explanation</th></tr></thead><tbody><tr><td>connectorURI</td><td>The URI of the MobiusFlow Connector that will be used to transmit the EnOcean telegram.</td></tr><tr><td>rawData</td><td>An array of single-byte numbers containing the transmission data. The length of this array will depend on the telegram type.</td></tr></tbody></table>

Below is shown an example configuration of a function node that can be used to generate a payload of the required format.

<figure><img src="../../.gitbook/assets/image (10) (1).png" alt="" width="356"><figcaption></figcaption></figure>

This data is also shown in the following code block.

```javascript
msg.payload = {
    connectorURI: '000001/024/FFC0/0001',
    rawData: [
        0x00,
        0x07,
        0x07,
        0x01,
        0xf6,
        0x70,
        0x00,
        0x00,
        0x00,
        0x0A,
        0x30,
        0x01,
        0xff,
        0xff,
        0xff,
        0xff,
        0xff,
        0x00
    ]
}
return msg;
```

### MobiusFlow Versions v2.x.x

As well as supporting the Sub BCMD node method from MobiusFlow versions 1.x.x, MobiusFlow 2.x.x introduces the EnOcean Connector TX node for further ease of sending EnOcean telegrams.

<figure><img src="../../.gitbook/assets/image (11).png" alt="" width="207"><figcaption><p>EnOcean Connector TX node</p></figcaption></figure>

Within the node's configuration, you must specify a MobiusFlow connector in which telegrams will be sent from.

<figure><img src="../../.gitbook/assets/image (12).png" alt="" width="467"><figcaption><p>Configuration of EnOcean Connector TX node</p></figcaption></figure>

The URI of the connector can either be typed in, or it can be searched for using the search button. In the above example, the connector with URI '000001/024/FFC0/0001' has been selected.

The node will send any data within the payload of the incoming message. A screenshot of example code of a function node used to set this payload is given below.

<figure><img src="../../.gitbook/assets/image (13).png" alt="" width="234"><figcaption></figcaption></figure>

This code is also given in the following code block.

```javascript
msg.payload = [
    0x00,
    0x07,
    0x07,
    0x01,
    0xf6,
    0x70,
    0x00,
    0x00,
    0x00,
    0x0B,
    0x30,
    0x01,
    0xff,
    0xff,
    0xff,
    0xff,
    0xff,
    0x00
]
return msg;
```

### Checksums and Sync Byte <a href="#h_01esk467vt0fpwxys3kzrvjb7r" id="h_01esk467vt0fpwxys3kzrvjb7r"></a>

All EnOcean telegram types feature a sync byte and some checksum bytes to ensure message integrity. When forming a telegram, the user **does not need to include the sync byte or checksum bytes**, as these are automatically added by MobiusFlow.

For further information about EnOcean telegrams structures we recommend consulting documentation provided by EnOcean.
