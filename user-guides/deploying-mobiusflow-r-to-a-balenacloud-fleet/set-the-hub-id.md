---
description: MobiusFlow® balenaCloud Device Variable
---

# Device Variables

balenaCloud devices are configured using Device Variables. When deploying **Mobius**Flow® to a balenaCloud fleet a number of Device Variables are created with default values. These are defined at the fleet level but can be overridden at the device level. More information about working with balenaCloud Device Variables can be found [here](https://docs.balena.io/learn/manage/variables/#device-variables).

## MobiusFlow Device Variables

The image below shows the Device Variables created when **Mobius**Flow® is deployed to balenaCloud.

<figure><img src="../../.gitbook/assets/Balena Variables.png" alt=""><figcaption></figcaption></figure>

<details>

<summary>MOBIUS_ENABLE_CONFIG_UI</summary>

Enable or disable the MobiusFlow® configuration user interface

**Possible Values:** (default shown in bold)

* **true** _- Enable the configuration user interface_
* false _- Disable the configuration user interface_

</details>

<details>

<summary>MOBIUS_ENGINE_API_AUTH_PROVIDER</summary>

Select which authentication provider to use for the Engine Rest API.

**Possible Values:** (default shown in bold)

* **local** - Use the local user database

</details>

<details>

<summary>MOBIUS_ENGINE_API_PORT</summary>

The Engine Rest API port

**Possible Values:** (default shown in bold)

* **8443**

</details>

<details>

<summary>MOBIUS_HUB_ID</summary>

The HUB ID used by this **Mobius**Flow® instance

**Possible Values:** (default shown in bold)

* **000001** - Can be any six digit hex number

</details>

<details>

<summary>MOBIUS_HUB_RESET_PSKS</summary>

Reset all **Mobius**Flow® Service pre-shared keys on startup

**Possible Values:** (default shown in bold)

* **true** - reset the pre-shared keys on startup
* false - do not reset the pre-shared keys on startup

</details>

<details>

<summary>MOBIUS_LICENCE</summary>

The **Mobius**Flow® licence code for this device

**Possible Values:** a valid licence code

</details>

<details>

<summary>MOBIUS_LICENCE_RENEW</summary>

Change the **Mobius**Flow® licence code. Set this to **true** when replacing an licence code

**Possible Values:** (default shown in bold)

* true - Change the licence code
* **false** - Use existing licence code

</details>

