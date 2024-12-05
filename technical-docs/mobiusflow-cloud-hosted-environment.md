---
description: >-
  Reference material for the environment in which MobiusFlow Cloud Instances
  exist
---

# MobiusFlow Cloud Hosted Environment

## MobiusFlow with LoRaWAN Stack

It is optional to include the LoRaWAN Stack when specifying the hosting type on instance creation. This Stack will grant the ability to use the [MobiusFlow LoRaWAN LNS](mobiusflow-services/lorawan-local-network-server.md).

If included, an instance of [Chirpstack](https://www.chirpstack.io/) and it associated infrastructure will be hosted in the background. Accessing this is not necessary to use the LNS, however it is accessible if required. Full details can be found within the [LNS Service documentation](mobiusflow-services/lorawan-local-network-server.md#lns-backend-chirpstack).

## Port Mappings (Simple)

The table below shows a simple overview illustrating how the ports are mapped. This is a simple overview suitable for most users.

<table><thead><tr><th width="168">Exposed Port</th><th width="170">Internal</th><th width="189">Usage</th><th>Version</th></tr></thead><tbody><tr><td>8443</td><td>8443</td><td>Mobius Engine API</td><td>All</td></tr><tr><td>8080</td><td>8080</td><td>MobiusFlow UI (Toolbox)</td><td>All</td></tr><tr><td>1880</td><td>1880</td><td>Flows access</td><td>All</td></tr><tr><td>8883</td><td>1883</td><td>Suggested use for MQTT Broker. If the port is set to 1883 within the service, it will be accessible in the outside via 8883.</td><td>All</td></tr><tr><td>30815</td><td>30815</td><td>Free</td><td>All</td></tr><tr><td>30817</td><td>30817</td><td>Free</td><td>All</td></tr><tr><td>8081</td><td>8082</td><td>Chirpstack UI</td><td>MobiusFlow with LoRaWAN Stack</td></tr><tr><td>1700</td><td>1700</td><td>EU868 Chirpstack LoRaWAN Gateway Bridge</td><td>MobiusFlow with LoRaWAN Stack</td></tr><tr><td>1701</td><td>1700</td><td>US915_0 Chirpstack LoRaWAN Gateway Bridge</td><td>MobiusFlow with LoRaWAN Stack</td></tr><tr><td>1702</td><td>1700</td><td>US915_1 Chirpstack LoRaWAN Gateway Bridge</td><td>MobiusFlow with LoRaWAN Stack</td></tr></tbody></table>

## Port Mappings (Advance)

### Docker & Docker Routing

Different parts of the MobiusFlow solution run in different docker containers. These communicate via docker routing. Docker routing allows container names to be resolved in the Host OS, for example, to refer to the Mobius Engine API from the Host OS or a container that is not the _mobius_ container, one could use _mobius:8442_ (container name followed by Host OS Port).

This means that, if communication between containers is required, the Host OS port and container is required. As such, these are included in the advanced port mappings table below.

### Full Mappings

The table below gives a full description of the port mappings a MobiusFlow Cloud hosted environment is subject to.

<table><thead><tr><th width="137">Exposed Port</th><th width="127">Host OS Port</th><th width="111">Container Name</th><th width="96">Internal</th><th width="173">Usage</th><th>Version</th></tr></thead><tbody><tr><td>8443</td><td>8442</td><td>mobius</td><td>8443</td><td>Mobius Engine API</td><td>All</td></tr><tr><td>8080</td><td>8080</td><td>toolbox</td><td>8080</td><td>MobiusFlow UI (Toolbox)</td><td>All</td></tr><tr><td>1880</td><td>1879</td><td>mobius</td><td>1880</td><td>Flows access</td><td>All</td></tr><tr><td>8883</td><td>1883</td><td>mobius</td><td>1883</td><td>Free - Normally MF MQTT Broker</td><td>All</td></tr><tr><td>30815</td><td>30814</td><td>mobius</td><td>30815</td><td>Free</td><td>All</td></tr><tr><td>30817</td><td>30816</td><td>mobius</td><td>30817</td><td>Free</td><td>All</td></tr><tr><td>8081</td><td>8082</td><td>chirpstack</td><td>8082</td><td>Chirpstack UI</td><td>MobiusFlow with LoRaWAN Stack Only</td></tr><tr><td>/</td><td>1884</td><td>mosquitto</td><td>1884</td><td>Chirpstack MQTT broker</td><td>MobiusFlow with LoRaWAN Stack Only</td></tr><tr><td>/</td><td>8090</td><td>chirpstack-rest-api</td><td>8090</td><td>Chripstack Rest API</td><td>MobiusFlow with LoRaWAN Stack Only</td></tr><tr><td>1700</td><td>1700</td><td>chirpstack-gateway-bridge-eu868</td><td>1700</td><td>EU868 Chirpstack LoRaWAN Gateway Bridge</td><td>MobiusFlow with LoRaWAN Stack Only</td></tr><tr><td>1701</td><td>1701</td><td>chirpstack-gateway-bridge-us915_0</td><td>1700</td><td>US915_0 Chirpstack LoRaWAN Gateway Bridge</td><td>MobiusFlow with LoRaWAN Stack Only</td></tr><tr><td>1702</td><td>1702</td><td>chirpstack-gateway-bridge-us915_1</td><td>1700</td><td>US915_1 Chirpstack LoRaWAN Gateway Bridge</td><td>MobiusFlow with LoRaWAN Stack Only</td></tr></tbody></table>

