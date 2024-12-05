---
description: For MobiusFlow 1.x.x only
---

# Diagnostics and Service Control

## Service diagnostics and control <a href="#nodediagnosticsandservicecontrol-servicediagnosticsandcontrol" id="nodediagnosticsandservicecontrol-servicediagnosticsandcontrol"></a>

The service diagnostics and control page shows all of the configured services, their current status and controls to start and stop services.

### Run state column <a href="#nodediagnosticsandservicecontrol-runstatecolumn" id="nodediagnosticsandservicecontrol-runstatecolumn"></a>

The Run State column (2) shows the current run state of the services in a traffic light. The colours are defined as follows:

* **Grey** - Not running, never started
* **Red** - Not running, manually stopped
* **Amber** - Starting or attempting to start
* **Green** - Running

### Actions column <a href="#nodediagnosticsandservicecontrol-actionscolumn" id="nodediagnosticsandservicecontrol-actionscolumn"></a>

The Actions column (3) has start / stop buttons for each service. Services can be manually started or stopped by clicking on the action buttons.

These action buttons do not modify the value of the **Run on Start** checkbox on the [services configuration](https://support.iaconnects.co.uk/hc/en-gb/articles/360025433491-Service-and-Object-Configuration) page.

### Service status column <a href="#nodediagnosticsandservicecontrol-servicestatuscolumn" id="nodediagnosticsandservicecontrol-servicestatuscolumn"></a>

The service status column (4) shows the current status of all running services. In addition to a text message, the statuses are colour coded as follows:

* Amber - starting or status unknown
* Red - service is running but in fault (see text message for details)
* Green - service is running and not in fault

The values shown in the Service Status column are tied to the service status object associated with the service. These status objects are automatically created and updated by the services as object profile ID 0001 with instance 0001. You can read the status of these objects but should not write to them.

### View objects column <a href="#nodediagnosticsandservicecontrol-viewobjectscolumn" id="nodediagnosticsandservicecontrol-viewobjectscolumn"></a>

The View Objects column (5) are hot-links to the Objects Diagnostics page, but filtered to only show objects belonging the the relevant service.

## Object and resource diagnostics <a href="#nodediagnosticsandservicecontrol-objectandresourcediagnostics" id="nodediagnosticsandservicecontrol-objectandresourcediagnostics"></a>

The Objects diagnostics page can be shown by clicking on the Objects button on the left of the screen (section 1 in image below) or by clicking on the View Objects hot-link described above. To view all objects belonging to all services use the Objects button (section 1 in image below).

Clicking on the plus sign (3) next to an object expands it to show all of its resources and their current values (2).

### Modifying a resource value <a href="#nodediagnosticsandservicecontrol-modifyingaresourcevalue" id="nodediagnosticsandservicecontrol-modifyingaresourcevalue"></a>

It is possible to manually modify a resource's value by writing to, or clearing a value in its priority array (see [MobiusFlow Architecture](../../technical-docs/mobiusflow-basics/mobiusflow-architecture.md)). Click on a resource to display its full priority array. Click on a priority to modify its value or clear it.

Resource value modifications are temporary and could be overwritten by a service or Node-RED flow, and do not persist between service restarts or node reboots.
