---
description: >-
  This page explains how to use the MobiusFlow specific Node-RED nodes to pull
  data from the MobiusFlow Engine into the flows, as well as how to move data
  from the flows back into the MobiusFlow Engine.
---

# Data Transfer between Flows and MobiusFlow Engine

All Node-RED nodes that facilitate the data transfer between the MobiusFlow Engine and the Flows are contained in the [node-red-contrib-mobius-flow-base](https://flows.nodered.org/node/node-red-contrib-mobius-flow-base) package. Ensure you add this package to your palette to continue. Also ensure you have setup a connection between the MobiusFlow engine and the Flows by following this [guide](connecting-to-flows-to-mobiusflow-engine.md).

All specific information on how to use each node can also be found within that nodes help pane within Node-RED. As well as this guide, we recommend using the help panes as a close reference when first learning how these nodes are used.

## Moving data into Flows

Pulling data into a given flow can be triggered in two ways. Firstly, a message within the flows can cause a 'Get', where data is pulled from the MobiusFlow Engine on demand. Alternatively, flows can be setup to respond to a change of value (COV) of a given MobiusFlow resource or object within the MobiusFlow Engine.

### Basic Get

The simplest 'Get' nodes come in the form of getResource and getObject nodes, which get the current value of a specified MobiusFlow resource or object respectively. An example flow using the getResource node is shown below.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption><p>Example of how to use a getResource node</p></figcaption></figure>

Both the getResource and getObject nodes require a MobiusFlow URI to be specified to control which data they fetch. This is set within the node configuration.

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Configuration window of the getResource node</p></figcaption></figure>

In the above example, the URI has been set to the resource 000001/027/0201/0001/40. Upon clicking done, the node label reflects this specification.

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>Node label of the getResource node reflecting the specified resource URI</p></figcaption></figure>

When the getResource or getObject nodes receive an input message, the 'Get' will be performed and the results will be sent out of the node's outputs. In the above case, clicking the inject button will trigger the flow causing the 'Get' to occur, and the output of this will be detected and displayed by the debug node.

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption><p>Debug window showing the result of the triggered flow. In this case the current value of specified resource was 0</p></figcaption></figure>

The getObject node works in an identical way however an object URI is specified instead of a resource URI.

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption><p>Result of equivalent flow when using getObject node</p></figcaption></figure>

Note that the output from a getObject node is more complex due to the data from a whole MobiusFlow object (including all resources) being pulled rather than just a specified resource.

### Basic COV

Basic COV nodes include the resourceCov and objectCov nodes. These directly reflect how the getResource and getObject nodes work respectively however respond to a change of value within the MobiusFlow Engine, rather than a trigger message.

The nodes are configured in the same way, by specifying either a resource URI or object URI.

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption><p>Example flow of a resourceCov node</p></figcaption></figure>

In the above example, the resourceCov node has responded the resource of URI 000001/027/0201/0001/40 changing to value of 1. This is reflected in the debug window.

The equivalent flow can also be constructed for the objectCov node. This flow will a respond to a change of any of the resources contained within the specified object.

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption><p>Example flow of the objectCov node</p></figcaption></figure>

Notice, in the case of the objectCov node, in the debug window only changed resource are shown (in this case the objectLastUpated time and the value). It can be changed in the nodes configuration so all resources are contained in the output message if this is required.

{% hint style="info" %}
The getResource, getObject, resourceCov and objectCov nodes can also make use or [URI wildcarding](../../user-guides/mobiusflow/mobiusflow-uniform-resource-identifiers.md#mobiusflowuniformresourceidentifiers-mobiusuriwildcards), allowing for a group of objects or resources to be selected instead of a just one.


{% endhint %}

### Additional Outputs

You may have noticed that in the case of the some nodes, an extra output is present. This output provides a response with an increased level of information if this is required in your flow.

<figure><img src="../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption><p>Example usage of second output</p></figcaption></figure>

Notice in the above debug window, the resultant response contains both the name of the resource as well as its new value, instead of just the value itself.

Increasing the level of detail of the output response can be further expanded for almost all MobiusFlow nodes by enabling the 'Use detailed outputs' option in the node configuration.

<figure><img src="../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption><p>ResourceCov node with 'Use detailed outputs' enabled</p></figcaption></figure>

Notice now in the flow below that the node now has four outputs. Each output has an ever increasing level of detail and this is shown in the four responses in the debug window.

<figure><img src="../../.gitbook/assets/image (10) (1) (1).png" alt=""><figcaption><p>Example of usage of all detailed outputs</p></figcaption></figure>

### Further Get and COV nodes

There is an array of other node types which allow data fetching from the MobiusFlow Engine in a variety of specific ways. These will not be explained in full but will be summarised here.

<table><thead><tr><th width="166.33333333333331">Node Type</th><th width="96">Type</th><th>Explanation</th></tr></thead><tbody><tr><td>Mobius Flow Inject</td><td>COV</td><td>Allows the definition of a set included or exluded URIs (including <a href="../../user-guides/mobiusflow/mobiusflow-uniform-resource-identifiers.md#mobiusflowuniformresourceidentifiers-mobiusuriwildcards">wildcards</a>). The node will act similar to an objectCov node for all of these included (but not excluded) URIs and output their data into your flow in the MobiusFlow Inject standard format. Nodei s very useful when linked with a Cloud Format node to allow data to be send to cloud application.</td></tr><tr><td>Get Multi-Object</td><td>Get</td><td>Get several objects in a single message when triggered based on a pre-specified set of URIs (including <a href="../../user-guides/mobiusflow/mobiusflow-uniform-resource-identifiers.md#mobiusflowuniformresourceidentifiers-mobiusuriwildcards">wildcards</a>).</td></tr><tr><td>Filter by Rid Value</td><td>Get</td><td>Allows a set of objects to be specified as well as a single resource. When triggered, the node will test the specified resource of all objects against a user defined filtration function and will output a list of all objects which passed the filter.</td></tr><tr><td>Discover</td><td>Get</td><td>Allows a the discovery of MobiusFlow entities based on a URI specified within the input topic. The discovery will work on any level (service / profile / object / etc. ) based on how specified the input URI is.</td></tr><tr><td>Discover Object List</td><td>Get</td><td>Works the same as the discover node however allows a set of URIs to specified (including <a href="../../user-guides/mobiusflow/mobiusflow-uniform-resource-identifiers.md#mobiusflowuniformresourceidentifiers-mobiusuriwildcards">wildcards</a>). Node outputs all discovered MobiusFlow entities as either individual messages or a single array packaged message.</td></tr></tbody></table>

## Moving data from Flows to MobiusFlow Engine

Often useful data will be in your flows from an external sources or maybe simply the result of a calculation based on several other pieces of data. Either way, it is often useful to put this data back into a MobiusFlow resource so it can be used in the same way as any other data within MobiusFlow.

A 'Set' can be performed as a single resource or a group of multiple resource at once using the setResource and setMultiResource nodes respectively.

### Set Resource

The setResource node allows the user to specify a target resource URI, and if valid, will set that resource to whatever the payload of the input message is.

<figure><img src="../../.gitbook/assets/image (11) (1) (1).png" alt=""><figcaption><p>Example flow using setResource node to set resource with URI 000001/027/0201/0001/40</p></figcaption></figure>

In the above case, the inject node has been set up to inject a message with a payload of 10, causing the setResource node to set the MobiusFlow resource of URI 000001/027/0201/0001/40 to a value of 10.

You may notice the setResource node also contains outputs of its own. These allow the message to continue to trigger further actions if required.

### Set Multi-Resource

The setMultiResource requires specification of a target object URI. It expects the input payload to contain an array of JSON objects each containing a resource / priority / value (RPV) triplet. More information can be found in the nodes help pane. An example payload to set resource 40 to a value of 1 and a resource 41 to a value of True may look like the following.

```

[
    { "r": 40, p: 15, v: 1},
    { "r": 41, p: 15, v: true }
]

```

## Input Topic

It is very important to note that most of the node's functionality depend on input topic. If any of  the nodes detect that the input topic is the form of a MobiusFlow URI, this **input topic will override the URI specified within the nodes own configuration**. This can often cause problem if you're stringing multiple MobiusFlow nodes together which relate to different URIs. These issues can be circumvented by using a change node to delete or change message topics where necessary.

The behaviour can also be very useful. This is because you can leave a given MobiusFlow node's URI field unspecific an rely solely on input topic to control its function. This means that the function of a single node can be dynamically change based on the state of other parts of your flows, avoiding the need for long lists of of the same type of node and complex switching logic.
