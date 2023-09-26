# Receiving and Sending Raw EnOcean Telegrams

This article aims to explain how EnOcean telegrams can be sent and received within **Mobius**Flow. The article briefly covers the supported telegram types and illustrates how these types affect the setup of a given flow.

## Receiving <a href="#receiving" id="receiving"></a>

### Overview <a href="#overview" id="overview"></a>

EnOcean telegrams can be received and injected into a given flow using the Subscribe to Broadcast Command node, labeled 'sub bcmd'. This node is shown below.

![](<../.gitbook/assets/image (2) (1) (1).png>)

Upon opening the node configuration, the Command ID config parameter is presented. The EnOcean telegram type to be injected into the flow is specified here. This is shown in the screenshot below.

![mceclip1.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079640511/mceclip1.png)

Once an incoming telegram of the specified type is detected by the sub bcmd node, the node will forward this telegram out of its output.

### Command Types <a href="#command_types" id="command_types"></a>

The table below shows which Command ID entries relate to which telegram types. The table also shows screenshots of each Command ID being used within the sub bcmd node configuration.

| **Type**                                                   | **Command ID**            | **Example Screenshot**                                                                              |
| ---------------------------------------------------------- | ------------------------- | --------------------------------------------------------------------------------------------------- |
| <p>ERP1</p><p>(EnOcean Radio Protocol 1- Fixed Length)</p> | ENOCEAN\_RADIO\_ERP1      | ![mceclip2.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079642071/mceclip2.png) |
| ERP1 VLD (EnOcean Radio Protocol 1 - Variable Length       | ENOCEAN\_RADIO\_ERP1\_VLD | ![mceclip3.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079487792/mceclip3.png) |
| MSC (Manufactuere Specific Commands)                       | ENOCEAN\_RADIO\_MSC       | ![mceclip4.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079487872/mceclip4.png) |
| RMC (Remote Management Command)                            | ENOCEAN\_RADIO\_RMC       | ![mceclip5.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079642391/mceclip5.png) |

### Example <a href="#example" id="example"></a>

In this example, a sub bcmd node is used to subscribe to incoming EnOcean RMC telegrams. The sub bcmd node is linked to a debug node to allow the telegram to be displayed. This setup is shown in the flow below.

![mceclip9.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079643151/mceclip9.png)

The configuration of the sub bcmd node is shown below.

![mceclip5.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079642391/mceclip5.png)

Following the deployment, an incoming RMC telegram was received. This was displayed in the debug panel using the debug node. This result is shown in the screenshot below.

&#x20;

![mceclip8.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079643011/mceclip8.png)

Notable parts of this response include the message topic (shown in the red box below) stating the telegram type as well as which EnOcean connector received the telegram and on which Mobius hub the telegram was received (HubID/ServiceID/TelegramType). Furthermore, the actual data contained with the telegram is shown in the green box in the screenshot below.

&#x20;

![mceclip12.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079489792/mceclip12.png)

### Telegram Response Profiles <a href="#telegram_response_profiles" id="telegram_response_profiles"></a>

It's worth noting that other telegram types (e.g. ERP1 or MSC) have different response profiles to the RMC profile exemplified in the previous section. All profiles are documented in the table below.

| **Telegram Type** | **Example Response Profile**                                                                        |
| ----------------- | --------------------------------------------------------------------------------------------------- |
| ERP1              | ![mceclip2.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079720891/mceclip2.png) |
| ERP1 VLD          | ![mceclip3.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079721151/mceclip3.png) |
| MSC               | ![mceclip4.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079566252/mceclip4.png) |
| RMC               | ![mceclip8.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079643011/mceclip8.png) |

## Sending <a href="#sending" id="sending"></a>

### Overview <a href="#sending" id="sending"></a>

EnOcean telegrams can be sent from the flows using the Send Broadcast Command node, labeled 'send bcmd'. This node is shown below. &#x20;

![mceclip0.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079560652/mceclip0.png)

On opening the node's configuration, a Command ID is required to specify the function of the node. To allow the node to send EnOcean telegrams, the Command ID should read 'ENOCEAN\_RADIO\_TX'. This is shown in the configuration window below.

![mceclip14.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079644691/mceclip14.png)

The node accepts and forwards data contained within the payloads of incoming messages. The appropriate incoming message structure is shown below.

```
msg.payload = {
 sid: (EnOcean Connector Service ID),
 rawData: (Command Data)
}
```

sid: The Service ID of the EnOcean connector that will be used to transmit the EnOcean telegram. This takes the form of a 3 digit hex string.

rawData: An array of single-byte numbers containing the transmission data. The length of this array will depend on the telegram type.

### Checksums and Sync Byte <a href="#h_01esk467vt0fpwxys3kzrvjb7r" id="h_01esk467vt0fpwxys3kzrvjb7r"></a>

All EnOcean telegram types feature a sync byte and some checksum bytes to ensure message integrity. These features, outlined in red, are shown within an RMC telegram profile below.

![mceclip8.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079724451/mceclip8.png)

When forming a telegram, the user **does not need to include the sync byte or checksum bytes**, as these are automatically added by **Mobius**Flow. In the example above, the RMC (Remote Management Command) type is described. This telegram type will be further used in the later [example in this article](https://support.iaconnects.co.uk/hc/en-gb/articles/360054113731-Receiving-and-Sending-EnOcean-Telegrams#h\_01ESKCME42TGYDZXH3XRV50K5J).

### Telegram Types <a href="#telegram_types" id="telegram_types"></a>

The type of telegram being sent is specified within the 'Packet Type' field in the rawData of the outgoing telegram. This is shown in the context of an RMC telegram (Packet Type 7) in the red box below.

![mceclip7.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079724351/mceclip7.png)

Note, the type of telegram specified vastly affects the remaining profile of the telegram so the correct telegram profile must be used with the specified type. The following table shows which packet type values correspond to which telegram types.

| **Type(s)**               | **Value**  |
| ------------------------- | ---------- |
| ERP1, ERP1 VLD            | 1          |
| Generic Response          | 2          |
| Radio Sub Tel             | 3          |
| Event                     | 4          |
| Common Command            | 5          |
| Smart Acknowledge Command | 6          |
| RMC                       | 7          |
| Radio Message             | 9          |
| ERP2                      | 10         |
| Command Accepted          | 12         |
| Radio 802\_15\_4 Raw      | 16         |
| Command 2.4GHz            | 17         |
| MSC                       | 128 to 255 |

### Example <a href="#h_01eskcme42tgydzxh3xrv50k5j" id="h_01eskcme42tgydzxh3xrv50k5j"></a>

In this example, the send bcmd node is used to send an RMC EnOcean telegram. An inject node, labeled Trigger, is used to initially trigger the flow. This is wired to a function node, labeled Form Telegram, which is used to transmute the incoming trigger message into the outgoing EnOcean telegram. Finally, the function node is wired to the send bcmd node which is used to send the newly formed EnOcean telegram. This entire flow is shown below.

![mceclip1.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079562872/mceclip1.png)

The function node has been configured to contain the following setup. This sets the Service ID (sid) and rawData properties of the message payload.

&#x20;

![mceclip5.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079568812/mceclip5.png)

In the above screenshot, the rawData has been divided to illustrate the distinct header, data, and optional data segments. The colours used to show these segments match the colours used to describe the RMC telegram structure in the following table.

![mceclip13.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079644551/mceclip13.png)

Also note, within the function node, the sid property has been set to the hex string 'F01', to match the service ID of the connector that will be used to send the message. In this case, the connector being used has sid F01 and this is shown in red in the diagnostics window below.

&#x20;

![mceclip21.png](https://support.iaconnects.co.uk/hc/article\_attachments/360079651171/mceclip21.png)

The code contained within the function node is shown in code form below.

```
msg.payload = {
sid: 'F01', // Connector Service ID
rawData: [
 0x00,
 0x04 + 2, // Data Length
 0x0A,     // Optional Data Length
 0x07,     // Remote Man Type
 0x04,     // Function Number
 0x51,     // Function Number
 0x00,     // Manufacturer ID
 0x47,     // Manufacturer ID
 100,      // data byte 0
 200,      // data byte 1
 0x00,     // Destination ID
 0x00,     // Destination ID
 0x00,     // Destination ID
 0x00,     // Destination ID
 0x00,     // Source ID
 0x00,     // Source ID
 0x00,     // Source ID
 0x00,     // Source ID
 0xFF,     // dBm
 0x00      // Send With Delay
]};
return msg;
```

When the flow is triggered, the function node generates the EnOcean telegram and this is sent using the send bcmd node.\
