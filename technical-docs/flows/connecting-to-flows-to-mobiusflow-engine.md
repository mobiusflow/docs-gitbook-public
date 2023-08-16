---
description: >-
  Description of how to setup connection between Node-RED Flows and MobiusFlow
  Engine
---

# Connecting to Flows to MobiusFlow Engine

The flows are powered by Node-RED. Use the link below to learn more about Node-RED specifically.

{% embed url="https://nodered.org/" %}

Node-RED can be used independently of MobiusFlow, however if you want move data between the MobiusFlow Engine and the Node-RED flows, you will need to link the two.

## MobiusFlow Specific Nodes

A set of MobiusFlow specific nodes have been created to facilitate data transmission between the Flows and the MobiusFlow Engine. The nodes are found in the Node-RED package [node-red-contrib-mobius-flow-base](https://flows.nodered.org/node/node-red-contrib-mobius-flow-base). If you're using Node-RED pre-packaged with MobiusFlow, this package will be installed by default however if you're using Node-RED running elsewhere, you will need to add this to your palette using the Node-RED palette manager.

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption><p>The correct package shown in the Node-RED palette manager search results</p></figcaption></figure>

## Setting up MobiusFlow Connection

A MobiusFlow connection is defined within a Node-RED configuration node. Once defined, all MobiusFlow specific nodes in your flows can use this connection to interface with the MobiusFlow Engine.

To create a new connection, open the config window of any MobiusFlow node. If no connection has yet been defined, the node will prompt you to add a new one.

<figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption><p>Prompt to add a new connection shown here within a getResource node configuration window</p></figcaption></figure>

Clicking the pencil icon will open the new connection's configuration window.

<figure><img src="../../.gitbook/assets/image (10) (1).png" alt=""><figcaption><p>The configuration window of the new connection</p></figcaption></figure>

### Authorisation

All connections require a valid API username and password to ensure this instance of Node-RED is authorised to connect to MobiusFlow.

The default cradentials are:

Username: **admin**

Password: **adm123**

{% hint style="warning" %}
We **heavily** recommend you change the default admin password. If your MobiusFlow instance is not brand new it's very likely this will have been changed already.
{% endhint %}

### Using Node-RED pre-packaged with MobiusFlow

If you're using the instance of Node-RED that has come pre-packaged with MobiusFlow, that means Node-RED and the MobiusFlow Engine and running locally to one another in parallel docker containers . As such, the following settings must be used:

#### Host

`mobius:8443`

#### Use SSL/TLS

This controls if the connection uses HTTP or HTTPS. As Node-RED is running locally relative to the MobiusFlow Engine, this should be left unchecked to ensure the connection uses HTTP.

### **Using external Node-RED**

When running Node-RED remotely relative to the MobiusFlow Engine, we recommend SSL/TLS is enabled so the connection is secure. Also ensure the port is appended to the hostname if required.

## Checking the Connection

Once set up, you should check that the flows are successfully connected to the MobiusFlow Engine.

On any MobiusFlow node, select the newly added connection. If this is the only connection you have set up, it will be selected by default.

<figure><img src="../../.gitbook/assets/image (11) (1).png" alt=""><figcaption><p>The configuration window of a getResource node showing the selected connection labelled <strong>mobius:8443</strong></p></figcaption></figure>

Upon clicking done and deploying your flows, all MobiusFlow nodes using this connection should show the status 'Connected' if the connection to the MobiusFlow Engine has been made.

<figure><img src="../../.gitbook/assets/image (12) (1).png" alt=""><figcaption><p>GetResource node showing 'Connected' status</p></figcaption></figure>

If you the connection has not successfully been made, the status of all nodes using that connection will reflect this.

<figure><img src="../../.gitbook/assets/image (13) (1).png" alt=""><figcaption><p>GetResource node showing 'Disconnected' status</p></figcaption></figure>
