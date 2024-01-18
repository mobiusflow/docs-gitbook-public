# Node-RED Flows

All MobiusFlow devices come with the open source [Node-RED](https://node-red.org/) flow-based programming software installed. For full Node-RED user documentation please refer to the [Node-RED documentation](https://nodered.org/docs/).

Node-RED is a programming tool for wiring together hardware devices, APIs and online services in new and interesting ways. It provides a browser-based editor that makes it easy to wire together flows using the wide range of nodes in the palette that can be deployed to its runtime in a single-click. A selection of nodes to communicate and interact with Mobius objects have been created. In addition to these MobiusFlow specific Node-RED nodes, the Node-RED community have published 100's of useful nodes that you can use in your projects. For more details on the full list of Node-RED nodes and examples, please have a look [here](https://flows.nodered.org/).

## Using Node-RED with MobiusFlow <a href="#node-redflows-usingnode-redwithmobiusflow" id="node-redflows-usingnode-redwithmobiusflow"></a>

In order for **Mobius**Flow to communicate with Node-RED, a connection needs to be setup between them. This connection requires some configuration both in Mobius and Node-RED. To make this easier, a Node-RED Mobius connector service has been created as well as acompanying Node-RED connection configuration node.

### Setting up the Mobius Node-RED connector service <a href="#node-redflows-settingupthemobiusnode-redconnectorservice" id="node-redflows-settingupthemobiusnode-redconnectorservice"></a>

1. Add the Node-RED connector service to your Mobius configuration (see [Configuring Services](https://support.iaconnects.co.uk/hc/en-gb/articles/360025140772))
2. Configure the Node-RED connector service (see [Node-RED Connector Service Settings](https://support.iaconnects.co.uk/hc/en-gb/articles/360025434631)). When using the built-in Node-RED instance use the following settings:
   1. **Host**: localhost
   2. **Port**: 1890
   3. **PSK**: a secret phrase such as _my-super-secret-secret_
3. Start the Node-RED connector service running (see [Node Diagnostics and Service Control](https://support.iaconnects.co.uk/hc/en-gb/articles/360025139552))
4. The service status will show as In Fault, with the message "Waiting for Node-RED to connect"

![](https://support.iaconnects.co.uk/hc/article\_attachments/360023998512/node-red\_connector\_setup.png)

### Setting up Node-RED <a href="#node-redflows-settingupnode-red" id="node-redflows-settingupnode-red"></a>

![](https://support.iaconnects.co.uk/hc/article\_attachments/360023998652/add\_object\_cov\_node.png)

* Open the Node-RED flows page
* Scroll down the Node-RED palette and find a Mobius **Object COV** node and drag it onto the flow
* Double click on the new Node-RED node to open the node's config page
* Click on the **Pencil** icon to add a new Mobius connection

![](https://support.iaconnects.co.uk/hc/article\_attachments/360023998632/configure\_node-red\_config\_node.png)

* Enter the same details that you entered into the Node-RED connector service and click **Done**

You only need to create the Mobius connection in Node-RED once. When adding additional Mobius enabled nodes they will share the same connection to Mobius

![](https://support.iaconnects.co.uk/hc/article\_attachments/360024022331/configure\_object\_cov\_uri.png)

* Enter a [Mobius URI](../mobiusflow/mobiusflow-uniform-resource-identifiers.md) to subscribe to for change of value notifications (to subscribe to all objects just enter a # wildcard) and click **Done**
* Click on the **Deploy** button to deploy the flow

![](https://support.iaconnects.co.uk/hc/article\_attachments/360024022351/node\_connected.png)

* The Node-RED node should have a green status indicator and the Node-RED connector service status should turn green and update its status text to connected
