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

* **true** - Enable the configuration user interface
* false - Disable the configuration user interface

</details>

<details>

<summary>MOBIUS_ENGINE_API_AUTH_PROVIDER</summary>

Select which authentication provider to use for the Engine Rest API.

**Possible Values:** (default shown in bold)

* **local** - Use the local user database

</details>
