# Getting Data out from MobiusFlow

This section covers different methods on moving your data from MobiusFlow to somewhere else. These methods include via MQTT, via REST and via WebScocket. Pick whichever method best suits your application / integration.

## Engine vs Historian

If using REST or WebSockets for data extraction, both Engine and Historian are suitable. Here is a comparison so you know which one to use in any given situation.

### Engine API / Engine WebSocket

* Contains telemetry as well as detailed information about MobiusFlow objects relating to MobiusFlow Engine.
* Historical data not available, only current data / live updates.
* Deeper granular control of which updates to subscribe to when using WebSocket

{% hint style="info" %}
Note: The Engine API is used for an overall much wider set of applications than just data extraction. It can be used to control everything within the MobiusFlow Engine (backend) including its configuration. See the [main article](../../mobiusflow-v3/mobiusflow-engine-api-v3/) on this for a full deep dive on this.
{% endhint %}

### Historian API / Historian WebSocket

* Data is telemetry / MobiusFlow resource value updates only. No extra engine data.
* Full historical data available.
* WebSocket allows subscription to all updates only, no granular control
