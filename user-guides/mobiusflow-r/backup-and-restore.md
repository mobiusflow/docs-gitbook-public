# Backup and Restore

The backup and restore feature is used to backup the full configuration of a **Mobius**Flow® instance, as well as to restore the configuration of a **Mobius**Flow® instance to a previously saved backup.

## Overview

In summary, all configuration data of a given **Mobius**Flow® instance can be **stored within** a single **.zip file**. As such, the current configuration of any **Mobius**Flow® instance can be **backed up by** simply **downloading** this file. Similarly, the configuration of any **Mobius**Flow® instance can **restored by uploading** a previously saved backup file.

All backup and restore functionality is accessed by navigating to to the '**Backup/Restore' menu** located on the '**Administration' Tab**.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption><p>Backup/Restore Menu</p></figcaption></figure>

## Backup

Once navigated to the 'Backup/Restore' menu, a backup can be created by simply clicking the '**Backup' button**.

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption><p>Backup button</p></figcaption></figure>

{% hint style="info" %}
Giving the backup an appropriate name is recommended. In the above screenshot, the name 'example-backup' has been set. Note that, the system will **automatically append date/time** information to the file name.
{% endhint %}

Once the backup file has been created, the option to '**Download Zip**' is shown.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Location of backup file download button</p></figcaption></figure>

Alternatively, the user can click 'Request new backup' to return to the previous menu and generate an updated backup file.

Once the 'Download Zip' button is clicked, the **backup file is downloaded** by the browser.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Downloaded backup file</p></figcaption></figure>

## Restore

As with backup, restore functionality is also accessed via the **'Backup/Restore' menu**. Restoration is performed by clicking '**Upload Zip**' and then **browsing to the .zip** backup file.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Upload Zip button</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Browsing to backup file</p></figcaption></figure>

Once the backup file has been uploaded, the menu **** will **show the backup information** as well as giving the the option the user to '**Restore**'.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Uploaded backup file information and restore button</p></figcaption></figure>

Restoration is performed by clicking the **'Restore' button**. The user is promoted with a **confirmation dialog** which must be **confirmed to trigger the restore** process.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Confirmation Dialog</p></figcaption></figure>

Finally, a dialog confirming the restore has been triggered is presented. The **Mobius**Flow® instance **will** then **reboot**, completing the restore process.
