---
description: MobiusFlow® balenaCloud Device Variable
---

# Device Variables

balenaCloud devices are configured using Device Variables. When deploying **Mobius**Flow® to a balenaCloud fleet a number of Device Variables are created with default values. These are defined at the fleet level but can be overridden at the device level. More information about working with balenaCloud Device Variables can be found [here](https://docs.balena.io/learn/manage/variables/#device-variables).

## MobiusFlow Device Variables

The image below shows the Device Variables created when **Mobius**Flow® is deployed to balenaCloud.

<figure><img src="../../.gitbook/assets/Balena Variables.png" alt=""><figcaption></figcaption></figure>

Expand the items below for detailed information on each Device Variable

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

* **local** _- Use the local user database_

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

* **000001** _- Can be any six digit hex number_

</details>

<details>

<summary>MOBIUS_HUB_RESET_PSKS</summary>

Reset all **Mobius**Flow® Service pre-shared keys on startup

**Possible Values:** (default shown in bold)

* **true** _- reset the pre-shared keys on startup_
* false _- do not reset the pre-shared keys on startup_

</details>

<details>

<summary>MOBIUS_LICENCE</summary>

The **Mobius**Flow® licence code for this device

**Possible Values:** _a valid licence code_

</details>

<details>

<summary>MOBIUS_LICENCE_RENEW</summary>

Change the **Mobius**Flow® licence code. Set this to **true** when replacing an licence code

**Possible Values:** (default shown in bold)

* true _- Change the licence code_
* **false** _- Use existing licence code_

</details>

<details>

<summary>MOBIUS_LOCAL_TIMEOUT</summary>

The maximum time in milliseconds that any **Mobius**Flow® Service will wait for a response to a **Mobius**Flow® message

**Possible Values:** (default shown in bold)

* **10000** _- any number greater than 1000_

</details>

<details>

<summary>MOBIUS_LOG_SERVICE_STATUS</summary>

Log changes of MobiusFlow® Services status to the standard logs

**Possible Values:** (default shown in bold)

* true _- log the service status changes to the standard logs_
* **false** _- do not log the service statis changes to the standard logs_

</details>
