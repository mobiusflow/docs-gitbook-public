---
description: For MobiusFlow 1.x.x only
---

# Service and Object Configuration

The configuration page is used to create and configure the MobiusFlow configuration for a Mobius node (see [MobiusFlow Architecture](../mobiusflow/mobiusflow-architecture.md)). The page is split into five main sections:

1. **The main menu**
2. **The services palette**
3. **The objects palette**
4. **The configuration tree**
5. **The service and object configuration section**

### The main menu <a href="#nodeserviceandobjectconfiguration-themainmenu" id="nodeserviceandobjectconfiguration-themainmenu"></a>

The main menu is displayed on all pages. It allows switching between Configuration, Diagnostics, Node-RED Flows and Administration. The Administration option is only shown for users who have admin privileges.

### The services palette <a href="#nodeserviceandobjectconfiguration-theservicespalette" id="nodeserviceandobjectconfiguration-theservicespalette"></a>

The services palette shows the list of Mobius services that can be added to the configuration. To add a service to your configuration drag it from the services palette and drop it on to the configuration tree.

### The objects palette <a href="#nodeserviceandobjectconfiguration-theobjectspalette" id="nodeserviceandobjectconfiguration-theobjectspalette"></a>

The objects palette shows the list of Mobius objects that can be added to the configuration. To add an object to your configuration drag it from the objects palette and drop it on to a service in the configuration tree.

### The configuration tree <a href="#nodeserviceandobjectconfiguration-theconfigurationtree" id="nodeserviceandobjectconfiguration-theconfigurationtree"></a>

The configuration tree shows the services and objects currently added to the configuration. Clicking on the triangles on the left of the tree either expands or contracts a branch of the tree. The currently selected item is shown as highlighted in orange.

To delete a service or object, hover over the item and click on the dustbin icon which appears to the right of the item.

Deleting a service deletes all associated objects

### The service and object configuration section <a href="#nodeserviceandobjectconfiguration-theserviceandobjectconfigurationsection" id="nodeserviceandobjectconfiguration-theserviceandobjectconfigurationsection"></a>

This section is dynamic and updates depending on which item has been selected in the configuration tree. If a service has been selected the service's configuration properties are displayed. Similarly, selecting an object or object resource shows the relevant configuration options.

Always click the Save Changes button to persist changes to a service, object or resource configuration. Any changes to a service, object or resource only become active **after** the service has been restarted on the diagnostics page.
