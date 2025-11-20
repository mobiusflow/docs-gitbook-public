---
description: Manage users and roles
---

# User Management

All access to MobiusFlow Toolbox and the MobiusFlow Engine API requires a valid username and password. Adding, deleting, and modifying users is done on the User Management tab on the Settings page.

{% hint style="warning" %}
Make sure to change your default admin user password or create a new account and delete the default admin account as soon as possible!
{% endhint %}

<figure><img src="../../.gitbook/assets/User management page.png" alt=""><figcaption></figcaption></figure>

The User Management page shows a list of all users with their roles, whether they are active or not, and an Actions button for additional user management.

{% hint style="danger" %}
As MobiusFlow is designed to run both online and offline it is not currently possible to retrieve a forgotten password. Make sure you keep your administrator password in a safe location!
{% endhint %}

## User Roles

There are three user roles, Viewer, Editor, and Administrator.&#x20;

#### Viewers

* View services, objects and live data
* View flows

#### Editors

* Add, edit, and delete services, objects and live data&#x20;
* Start and stop services
* Add, edit and delete flows
* Add edit and delete object profiles
* Import and export configuration

#### &#x20;Administrators

* Add, edit, and delete services, objects and live data&#x20;
* Start and stop services
* Add, edit and delete flows
* Add edit and delete object profiles
* Import and export configuration
* View and manage users
* Modify system settings

## Adding Users

Click on the **Add User** button to view the Add User dialog

Enter a Username, select a role, and enter the user's initial password. Users can change their own password later

The new user will appear in the users list

## Managing Users

Click on the **Action** button (three vertical dots) next to a user to open the user management menu

<figure><img src="../../.gitbook/assets/User action menu.png" alt=""><figcaption></figcaption></figure>

### Change Password

Change the password of an existing user. This is useful if a user forgets their password or you want to change the password of a [service account](user-management.md#service-accounts)

### Change Role

Change the role of an existing user

### Active / Deactive User

Users are active by default but can be activated or deactivated. Deactivated users will no longer be able to log in.&#x20;

### Delete User

Permanently delete an existing user. You will need to confirm your action before the user is deleted.

## Service Accounts

Access to the [MobiusFlow Engine API](../mobiusflow-engine-api-v3/) requires a valid user with the correct role.&#x20;

We recommend creating service account users with the Editor or Viewer role for API access. You should consider a separate account for each service that requires access as revoking access to a specific service can be as simple as deactivating that service account.

{% hint style="info" %}
Flows use the MobiusFlow Engine API to interact with services and objects. You should create a service account to use with Flows
{% endhint %}
