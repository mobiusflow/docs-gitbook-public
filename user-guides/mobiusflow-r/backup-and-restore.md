# Backup and Restore

You can use the backup and restore feature to backup the full configuration of a MobiusFlow instance, and to restore the configuration of a MobiusFlow instance to a previously saved backup.

## Overview

In summary, all configuration data of a MobiusFlow instance can be **stored within** a single **.zip file**. This means the current configuration of any MobiusFlow instance can be **backed up by** simply **downloading** this backup file and saving it in a safe location of your choice. Similarly, the configuration of any MobiusFlow instance can **restored by uploading** one of your previously saved backup files.

All backup and restore functionality is accessed through the '**Backup/Restore' menu** located on the '**Administration' Tab**.

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption><p>Backup/Restore Menu</p></figcaption></figure>

## Backup

On the '**Backup/Restore' menu**, you can create a backup by clicking '**Backup'**.

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption><p>Backup button</p></figcaption></figure>

{% hint style="info" %}
Giving the backup an appropriate name is recommended. In the above example, the name 'example-backup' has been set. The system will **automatically append date/time** information to the file name.
{% endhint %}

Once the backup file has been created, click '**Download Zip**' to download it.

<figure><img src="../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption><p>Location of backup file download button</p></figcaption></figure>

Alternatively, the you can click '**Request new backup**' to return to the previous menu and generate an updated backup file.

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption><p>Downloaded backup file</p></figcaption></figure>

Be sure to save your backup file in a safe location! There is nothing worse than not being able to find a much needed backup file.

## Restore

The restore feature is particularly useful if you want to copy a MobiusFlow configuration onto to other MobiusFlow instances, however it also useful if you've managed to break everything.

The **'Backup/Restore' menu** is also used for restoring. You can restore by first clicking '**Upload Zip**' and then **browsing to the .zip** backup file you previously saved in a safe place.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption><p>Upload Zip button</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Browsing to backup file</p></figcaption></figure>

Once uploaded, the menu will **show the backup information** as well as allowing you to click '**Restore**'.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption><p>Uploaded backup file information and restore button</p></figcaption></figure>

Accept the a confirmation dialog to proceed.

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption><p>Confirmation Dialog</p></figcaption></figure>

You will be notified that the restoration process has started and then MobiusFlow will then **reboot**, completing the restore process.

Congratulations for completing your restore!
