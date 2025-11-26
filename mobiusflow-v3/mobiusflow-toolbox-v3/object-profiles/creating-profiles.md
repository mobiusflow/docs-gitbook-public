---
description: Learn how to create new object profiles
---

# Creating Profiles

To create a new profile open the Object Profiles page, make sure that the sidebar is closed, and click on the **Create** button. This will open the Create Object Profile wizard.

{% hint style="info" %}
To close a sidebar click on the **X** button in the sidebar toolbar
{% endhint %}

<figure><img src="../../../.gitbook/assets/Profiles wizard 1.png" alt=""><figcaption></figcaption></figure>

The wizard will have three starting point options. Selecting one of the options will change the steps required to complete the wizard.

<table><thead><tr><th width="163.4921875"></th><th></th></tr></thead><tbody><tr><td><strong>A Blank Profile</strong></td><td>Start from scratch</td></tr><tr><td><strong>Profile Template</strong></td><td>Use an existing profile template as the starting point</td></tr><tr><td><strong>Existing Profile</strong></td><td>Use an existing profile as the starting point</td></tr></tbody></table>

## Start From a Blank Profile

If you choose to start with a blank profile and click **Next**, you will jump to the last step which is Finalise Settings

## Start From Profile Template or Existing Profile

Choosing to start from a template or existing profile and clicking **Next** will require you to select either a template or existing profile. These are shown in a table, which can be filtered. Select one of the rows before clicking on **Next** to view the last Finalise Settings step.

{% hint style="success" %}
The Codec, preprocessor, UI layout, and all resources defined in the template or existing profile, along with their settings will also be added to the profile when it is created
{% endhint %}

## Finalising Settings

Depending on your starting point, the Finalise Settings form will be blank or have some fields pre-populated by the template or existing profile.

<figure><img src="../../../.gitbook/assets/Profile finalise settings.png" alt=""><figcaption></figcaption></figure>

Fill in all required fields and optionally add a description and [tags](../tags.md) before clicking on **Create Profile.**

### PID

A unique profile ID as a four digit hexadecimal number from 0200 to FFFF.

### Group

The group is used by MobiusFlow toolbox to aid in filtering the object profiles. You can select from an existing group or type in a new group name.

### Profile Name and User Interface Name

The profile name is used to help identify this profile. It normally starts with a lower case letter and does not contain spaces, but can containg underscores and dashes.

The user interface name is a human readable name normally used by MobiusFlow View to make selecting profiles easier for non-technical users.

## 💥 Interactive Demo

{% embed url="https://demo.mobiusflow.com/demo/cmig4glb7cub6b7b4t4oifwdo?utm_source=link" %}
