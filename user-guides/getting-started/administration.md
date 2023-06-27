# Administration

The administration pages cover user administration, backup and restore, network settings, security and setting the Hub ID. Select the required administration function from the menu on the left of the page.

## User administration <a href="#nodeadministration-useradministration" id="nodeadministration-useradministration"></a>

Users can be added, modified and deleted from within the User Administration pages.

Select **Add New User** or **Edit/Delete User** to administer users.

![](https://support.iaconnects.co.uk/hc/article\_attachments/360023994752/add\_user.png)

## Network Settings <a href="#nodeadministration-networksettings" id="nodeadministration-networksettings"></a>

This is not currently enabled and all network settings should be done using the USB stick method described [here](https://support.iaconnects.co.uk/hc/en-gb/articles/360020899932-Changing-Mobius-Device-Network-Settings).

## Backup/Restore <a href="#nodeadministration-backup-restore" id="nodeadministration-backup-restore"></a>

A Mobius node can be backed up or restored by downloading or uploading a configuration zip file. All settings including user details, Node-RED flows and Mobius node configurations are included in a back up.

![](https://support.iaconnects.co.uk/hc/article\_attachments/360024018891/backup\_and\_restore.png)

To perform a backup, set a name (the default is mobius-backup with the date and time automatically added) and click the **Backup** button. This will download a zip file containing your backup.

To perform a restore, click the **Upload Zip** button and select a Mobius backup file. Once the file has uploaded click the **Restore** button. If the node does not restart after a minute, manually reboot the node by removing power.

A full article covering backup and restore can be found [here](../mobiusflow-r/backup-and-restore.md).

## Setting the Hub ID <a href="#nodeadministration-settingthehubid" id="nodeadministration-settingthehubid"></a>

All Mobius nodes are identified by their hub ID. This is a six character hexadecimal number and should be unique within any group of Mobius nodes. See [MobiusFlow Architecture](../mobiusflow-r/mobiusflow-architecture.md) and [MobiusFlow Uniform Resource Identifiers](../mobiusflow-r/mobiusflow-uniform-resource-identifiers.md) for more information about Hub IDs.
