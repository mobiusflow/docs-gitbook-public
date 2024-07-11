---
description: >-
  This page covers how to use the ADFWeb HD67941-B2 DALI/MQTT converter with
  MobiusFlow. The article covers control, querying and configuration for both
  standard luminaires and emergency lights.
---

# DALI via AFDWeb MQTT

## rchitecture Overview

The ADFWeb HD67941-B2 DALI/MQTT bridge acts as a converter between MQTT and DALI protocols. The bridge connects to an MQTT broker via either ethernet or WiFi. The bridge acts as a DALI master and therefore the pair of DALI lines is run directly into it. This completes the DALI/MQTT connection.

MobiusFlow can be connected to the same MQTT broker as DALI/MQTT bridge, allowing the two the communicate via MQTT. This allows MobiusFlow achieve to two-way communication with a given DALI circuit, hence allowing control, querying and configuration to be achieved.

The overall architecture is shown in the diagram below.

<figure><img src="../../../.gitbook/assets/image (21).png" alt="" width="302"><figcaption><p>High-Level System Architecture Diagram</p></figcaption></figure>

### Service - adfweb dali mqtt

A MobiusFlow service called '_adfweb dali mqtt_' has been made to specifically to allow control, querying and configuration to be performed simply and easily from MobiusFlow. Each adfweb dali mqtt service connects to a single HD67941-B2, so if your application uses mutliple HD67941-B2 then multiple _adfweb dali mqtt_ services should be used.

For some use cases that will be covered later in this article, MobiusFlow direct commands (DCMDs) can be used to control some functions of service. These DCMDs are sent via the MobiusFlow engine API most commonly from the Flows, however direct HTTP requests can also be used.

As such, a lower-level system architecture diagram looks as follows:

<figure><img src="../../../.gitbook/assets/image (23).png" alt="" width="489"><figcaption><p>Lower-level system architecture diagram</p></figcaption></figure>

### MQTT Broker

The MQTT broker can be run anywhere which is accessible over a network to both the HD67941-B2 and MobiusFlow. For ease, in most cases the MQTT broker is run within MobiusFlow itself. As such, the architecture diagram becomes the following:

<figure><img src="../../../.gitbook/assets/image (24).png" alt="" width="488"><figcaption><p>Lower-level system architecture diagram with the MQTT broker running within MobiusFlow</p></figcaption></figure>

## HD67941-B2 Configuration

To configure the HD67941-B2, ADFWeb's documentation on HD67941-B should be followed [here](http://www.adfweb.com/download/filefold/MN67941\_ENG.pdf). Use the instructions to get the HD67941-B2 to connect to your MQTT broker. To work with MobiusFlow correctly, specific MQTT settings must be set using the [SW67941](http://www.adfweb.com/download/filefold/SW67941.zip) configurator tool.

Navigate to the the MQTT Set Topic menu:

<figure><img src="../../../.gitbook/assets/image (25).png" alt="" width="516"><figcaption><p>The main menu of the SW67941 configurator tool with the MQTT Set Topic button highlighted</p></figcaption></figure>

### MQTT Publish

Once on the MQTT Set Topic menu, navigate to the MQTT publish tab. Create a single entry the following settings:

#### **Topic**

```
mobiusDALIquery/{MACID}
```

Note that {MACID} should be replaced with the MAC ID of the HD67941-B2 you're using. For example:

```
mobiusDALIquery/1064E209AD03
```

**Template**

The template should be set to the following JSON string:

```json
{
    "channel": $CHANNEL$, 
    "adv": $ADV$, 
    "grp1": $GRP1$, 
    "grp2": $GRP2$, 
    "ans": $ANSWER$, 
    "status": $STATUS$, 
    "type": $TYPE$, 
    "min": $MIN$, 
    "max": $MAX$  
}
```

All remaining fields should be populated as shown in the screenshot below:

<figure><img src="../../../.gitbook/assets/image (27).png" alt=""><figcaption><p>Correctly populated MQTT Publish tab</p></figcaption></figure>

### MQTT Subscribe

Navigate to the MQTT Subscribe tab.

#### **Topic**

The topic should be set as follows

```
mobiusDALIwrite/{MACID}
```

As before, {MACID} should be replaced with the MAC ID of the HD67941-B2 you're using. For example:

```
mobiusDALIwrite/1064E209AD03
```

The remainder of the row should be populated as shown in the screenshot below:

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption><p>Correctly populated MQTT Subscribe tab</p></figcaption></figure>

This completes the configuration required for MobiusFlow. Ensure all MQTT changes are saved before flashing the new configuration to the HD67941-B2.

## Luminaires and Groups

### Overview

Within MobiusFlow, a given DALI luminaire or DALI group is represented by an equivalent luminaire and group object. Both object types are designed to reside on the adfweb dali mqtt. This service is shown configured and running in the screenshot below.

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption><p>An adweb dali mqtt service and mqtt broker service running within MobiusFlow</p></figcaption></figure>

The two object types are tabulated below.

<table><thead><tr><th width="156">Object</th><th width="145">Profile ID (PID)</th><th width="201">Name in MobiusFlow</th><th>Parent Service</th></tr></thead><tbody><tr><td>DALI Luminaire</td><td>027A</td><td>dali_Luminiaire_v2</td><td><em>adfweb dali mqtt</em></td></tr><tr><td>DALI Group</td><td>027B</td><td>dali_group</td><td><em>adfweb dali mqtt</em></td></tr></tbody></table>

A single instance of both of these objects is shown live on an _adfweb dali mqtt_ service in the screenshot below. The screenshot also shows the configuration page for the luminaire object. A DALI short address should be entered to match that of a real-world DALI luminaire.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Configuration page for a DALI luminaire MobiusFlow object</p></figcaption></figure>

The configuration window of a group object is shown in the screenshot below. Similarly to a luminaire, a group address should be added to represent the group number of the DALI group this object will represent.

<figure><img src="../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>The configuration of page of a DALI group MobiusFlow object</p></figcaption></figure>

### Control

#### Overview

Both Luminaire objects and Group objects feature a setPoint resource (rid: 41). To change the lighting level, this resource should be simply be set in the same manner as any other MobiusFlow resource.

In the case of the Luminaire object, a knowLevel resource is also present. This populated as a result of the the current level being queried. It exists because sometimes due to issues with the system, there may be a discrepancy between the demanded level and actual level.

Within a luminaire, a resource exists for each group, allowing you to choose which groups the luminaire is a member of.

The screenshot below partially shows the resource list for the luminaire object.

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>Resource list of the DALI luminaire oject</p></figcaption></figure>

{% hint style="info" %}
Note that, the group membership of all luminaires should be set via changing the default value of any group membership resource prior to starting the _adfweb dali mqtt_ service. **Do not make the mistake of changing the live value** of these resources after the service has started. Although this will work, if the service is restarted, this group membership information **will not be saved**.
{% endhint %}

The group object is simpler. As querying the level of a whole group is not possible in DALI, no known level resource exists. As with the luminaire, the lighting level of the DALI group can be changed by setting the setPoint resource.

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Resource list for DALI group object</p></figcaption></figure>

#### Flows Examples

Below is an example of a simple flow with two inject buttons, one to set the level to 95% and the other to 5%. The inject nodes are linked to a setResource node which setup to set the setPoint resource of a live DALI luminaire (resource 000001/020/027A/41).

<figure><img src="../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

A very similar flow is shown to change the level of a group between 80% and 10%. In this case the setResource has been set to set the setPoint resource of the DALI group (resource 000001/020/027B/0001/41.

<figure><img src="../../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

A more typical use case may be to have the lights automatically controlled. As well as this, it may be required that groups and single luminaires may need to be controlled as one. In the below flow, an EnOcean PIR is linked to a 'local control' zone node, which is then linked both a setResource node linking to a single DALI luminaire, and a DALI group.

<figure><img src="../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

The local control node us used in this case to set time periods of when the lights should be at given levels. The config window for this node is shown below

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Note that is node is included within the _node-red-contrib-mobius-flow-lighting_ package and may not be included within your Flows palette by default. If this is the case, it can be instantly added using the palette manager.

### Querying

#### Overview

The system has been setup to automatically query several key properties of all luminaires. These are as follows:

* Group Membership (returned as raw 2 byte, bit-array)
* Ballast Status
* Lamp failure status
* Lamp arc power status
* Power failure status
* Raw status (all status information returned as 1 byte, bit-array)
* Device Type
* Max lighting level
* Min lighting level

Each luminaire object has resources to store this data. These resources are populated automatically when information is received from the HD67941-B2 DALI/MQTT bridge.

The system also allows the user to perform some additional queries manually. The queries can be sent by sending the _adfweb dali mqtt_ service a recognised MobiusFlow direct command (DCMD). These DCMDs can be sent directly using the MobiusFlow engine API or by using the DCMD node within the Flows. Ensure the DCMD is setup with a timeout time of at least 10,000ms. All queries use the DCMD command name:

```
GENERIC_DCMD
```

Supported queries and their associated DCMD data are tabulated below:

<table><thead><tr><th width="371">Query Type</th><th>Example DCMD Data</th></tr></thead><tbody><tr><td>Query power up level</td><td><pre class="language-json"><code class="lang-json">{
    command: 'queryPowerUpLevel',
    payload: {
        address: 0
    }
}
</code></pre></td></tr><tr><td>Query system failure level</td><td><pre class="language-json"><code class="lang-json">{
    command: 'queryPowerUpLevel',
    payload: {
        address: 0
    }
}
</code></pre></td></tr><tr><td>Query fade time / rate</td><td><pre class="language-json"><code class="lang-json">{
    command: 'queryPowerUpLevel',
    payload: {
        address: 0
    }
}
</code></pre></td></tr><tr><td>Query power failure</td><td><pre class="language-json"><code class="lang-json">{
    command: 'queryPowerUpLevel',
    payload: {
        address: 0
    }
}
</code></pre></td></tr><tr><td>Query dtr content</td><td><pre class="language-json"><code class="lang-json">{
    command: 'queryPowerUpLevel',
    payload: {
        address: 0
    }
}
</code></pre></td></tr></tbody></table>

In the above table, all payloads were shown for a target DALI luminaire with a DALI short address of 0, however this should be replaced with the DALI short address of whichever luminaire is the target of the query (0-63).

After sending the DCMD, if correct, you should receive a response. This response will be in the form of a raw byte. The DALI documentation should be used to interpret this data.

#### Flows Examples

Data that is automatically queried from all luminaires can be found in that luminaire's resource list.

<figure><img src="../../../.gitbook/assets/image (9) (1).png" alt=""><figcaption><p>Populated DALI luminaire resource list as a result of auto-querying</p></figcaption></figure>

In the example flow below, a resource COV node has been used to respond to the change of value of the lamp failure status (resource 54). This may be useful if actions need to be taken in such an event, e.g. notifying maintenance. A similar flow could be made to respond to the data from any of the resources.

<figure><img src="../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

In the case of special queries (queries which are not automatically run), as explained before, DCMDs should be sent. The flow below shows how this could be set up.

<figure><img src="../../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

The function node labelled function 1, is used to set the correct DCMD data for the query. The configuration is shown below:

<figure><img src="../../../.gitbook/assets/image (17).png" alt=""><figcaption><p>Function 1 node configuration</p></figcaption></figure>

The DCMD node is setup as follows:

<figure><img src="../../../.gitbook/assets/image (18).png" alt=""><figcaption><p>DCMD node configuration</p></figcaption></figure>

Note that the URI property should be set to target the _adfweb dali mqtt_ service. In this case, the service id of the _adfweb dali mqtt_ service is 020 and the hub id the MobiusFlow instance that service is running on is 000001, hence the target URI of 000001/020.

### Configuration

#### Overview

Configuration is performed in the same manner as manual querying, using DCMDs to directly interface with _adfweb dali mqtt_ service, sent either directly to the MobiusFlow engine API or using the Flows.

Ensure the DCMD is setup with a timeout time of at least 10,000ms. All queries use the DCMD command name:

```
GENERIC_DCMD
```

Supported queries and their associated DCMD data are tabulated below:

<table><thead><tr><th width="371">Query Type</th><th>Example DCMD Data</th></tr></thead><tbody><tr><td>Set maximum allowed lighting level</td><td><pre class="language-json"><code class="lang-json">{
    command: 'setMaxLevel',
    payload: {
        address: 0,
        level: 80,
        group: false
    }
}
</code></pre></td></tr><tr><td>Set minimum allowed lighting level</td><td><pre class="language-json"><code class="lang-json">{
    command: 'setMinLevel',
    payload: {
        address: 0,
        level: 10,
        group: false
    }
}
</code></pre></td></tr><tr><td>Set power up lighting level</td><td><pre class="language-json"><code class="lang-json">{
    command: 'setPowerUpLevel',
    payload: {
        address: 0,
        level: 80,
        group: false
    }
}
</code></pre></td></tr><tr><td>Set system failure level</td><td><pre class="language-json"><code class="lang-json">{
    command: 'setSysFailureLevel',
    payload: {
        address: 0,
        level: 50,
        group: false
    }
}
</code></pre></td></tr><tr><td>Set fade time</td><td><pre class="language-json"><code class="lang-json">{
    command: 'setFadeTime',
    payload: {
        address: 0,
        level: 5,
        group: false
    }
}
</code></pre></td></tr><tr><td>Set fade rate</td><td><pre class="language-json"><code class="lang-json">{
    command: 'setFadeRate',
    payload: {
        address: 0,
        level: 5,
        group: false
    }
}
</code></pre></td></tr><tr><td>Store current lighting level in dtr</td><td><pre class="language-json"><code class="lang-json">{
    command: 'setMaxLevel',
    payload: {
        address: 0,
        group: false
    }
}
</code></pre></td></tr></tbody></table>

In the above table, all data packets were shown for a target DALI luminaire with a DALI short address of 0, however this should be replaced with the DALI short address of whichever luminaire is the target of the query (0-63).&#x20;

The level parameter should be varied to set the desired quantity accordingly.&#x20;

The group property can be set to true if an entire DALI group is being configured at once. Note, in this case, the address property will represent the group number (0-15) instead of a DALI short address.

#### Flows Examples

The flow below shows how a DCMD node could be used to send configuration commands, in this case setting the maximum lighting level:

<figure><img src="../../../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

The node function node labelled function 4 is used to set the DCMD data. The configuration for this node is as follows:

<figure><img src="../../../.gitbook/assets/image (19).png" alt=""><figcaption><p>Function 4 configuration window</p></figcaption></figure>

The DCMD node is setup as follows:

<figure><img src="../../../.gitbook/assets/image (18).png" alt=""><figcaption><p>DCMD node configuration window</p></figcaption></figure>

Note that the URI property should be set to target the _adfweb dali mqtt_ service. In this case, the service id of the _adfweb dali mqtt_ service is 020 and the hub id the MobiusFlow instance that service is running on is 000001, hence the target URI of 000001/020.

## Emergency Lights

### Overview

A MobiusFlow object type has been created to represent DALI emergency lights. This object type contains resources to capture information regarding the status of the emergency light as well as test results. As with all other DALI object types, the DALI emergency light is designed to be a child of the _adfweb dali mqtt_ service. It's details are tabulated below.

<table><thead><tr><th width="156">Object</th><th width="145">Profile ID (PID)</th><th width="201">Name in MobiusFlow</th><th>Parent Service</th></tr></thead><tbody><tr><td>DALI Emergency Light</td><td>0259</td><td>dali_emergency</td><td>adfweb dali mqtt</td></tr></tbody></table>

The screenshot below shows a DALI emergency light object within an _adfweb dali mqtt_.

<figure><img src="../../../.gitbook/assets/image (29).png" alt=""><figcaption><p>DALI emergency light MobiusFlow object on an adfweb dali mqtt service</p></figcaption></figure>

Like all DALI objects, the DALI emergency object requires a DALI short address to be assigned to it:

<figure><img src="../../../.gitbook/assets/image (30).png" alt=""><figcaption><p>Configuration screen for a DALI emergency MobiusFlow object</p></figcaption></figure>

### Control & Querying

No automatic control or querying of DALI emergency lights is performed. As such, all interfacing is performed using MobiusFlow direct commands (DCMDs) sent to the _adfweb dali mqtt_ service, either via the MobiusFlow engine API or using the Flows.

In case of queries, data received as a result of the query automatically populates the corresponding MobiusFlow object. The data is also returned to the user via the DCMD response as normal.

Ensure the DCMD is setup with a timeout time of at least 10,000ms. All queries use the DCMD command name:

```
GENERIC_DCMD
```

Supported actions and their associated DCMD data are tabulated below:



<table><thead><tr><th width="194.5">Action</th><th>Example DCMD data</th></tr></thead><tbody><tr><td>Rest</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emRest',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Inhibit</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emInhibit',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>ReLight Inhibit</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emReLightInhibit',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Start function test</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emStartFunctionTest',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Start duration test</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emStartDurationTest',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Stop test</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emStopTest',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Reset function test done flag</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emResetFunctionTestDoneFlag',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Reset duration test done flag</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emResetDurationTestDoneFlag',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Reset lamp time</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emRestetLampTime',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Store DTR as emergency level</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emStoreDTRAsEmergencyLevel',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Store test delay time high byte</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emStoreTestDelayTimeHightByte',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Store test dalay time low byte</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emStoreTestDelayTimeLowByte',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Store function test interval</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emStoreFunctionTestInterval',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Store duration test interval</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emStoreDurationTestInterval',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Store test execuation timeout</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emStoreTestExecuationTimeout',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Store prolong time</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emStoreProlongTime',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Start indentification</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emStartIdentification',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Query battery charge</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emQueryBatteryCharge',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Query duration test result</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emQueryDurationTestResult',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Query lamp operational time</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emQueryLampOperationTime',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Query emergency mode</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emQueryEmergencyMode',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Query failure mode</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emQueryFailureMode',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr><tr><td>Query emergency status</td><td><pre class="language-json"><code class="lang-json">{
    command: 'emQueryEmergencyStatus',
    payload: {
        address: 0,
    }
}
</code></pre></td></tr></tbody></table>

In the above table, all data packets were shown for a target DALI emergency light with a DALI short address of 0, however this should be replaced with the DALI short address of whichever emergency light is the target of the action (0-63).

### Flows Examples

The flows can be used to easily send DCMDs to the _adfweb dali mqtt_ service to complete any desired actions. The flow below has been set to automatically query the potential failure mode on interval.

<figure><img src="../../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

The function node labelled function 8 is used to set the DCMD data prior to the request. The configuration for the node is as follows:

<figure><img src="../../../.gitbook/assets/image (31).png" alt=""><figcaption><p>Functon 8 node configuration</p></figcaption></figure>

The DCMD node is setup as follows:

<figure><img src="../../../.gitbook/assets/image (18).png" alt=""><figcaption><p>DCMD node configuration</p></figcaption></figure>

Note that the URI property should be set to target the _adfweb dali mqtt_ service. In this case, the service id of the _adfweb dali mqtt_ service is 020 and the hub id the MobiusFlow instance that service is running on is 000001, hence the target URI of 000001/020.

Note that, no debug node is used here to display query results. This is because, in the case of DALI emergency lights, the data is auto-populated into the corresponding DALI emergency light object.
