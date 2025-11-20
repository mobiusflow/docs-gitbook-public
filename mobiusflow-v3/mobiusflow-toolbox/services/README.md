---
description: Managing MobiusFlow Services
---

# Services

MobiusFlow Services are the starting point for any configuration. They are typically device drivers for a specific protocol or provide protocol interfaces such as an MQTT broker.

The main services page shows an overview and status of each service that has been added to the configuration. You can interact with services in a number of ways, including configuring a service, starting and stopping a service, or adding and configuring objects belonging to a service.

{% hint style="info" %}
MobiusFlow includes a number of pre-configured [system services](system-services.md) that you may or may not be able to interact with in the normal way. These include the Engine API and Historian services
{% endhint %}

<figure><img src="../../../.gitbook/assets/Service page overview.png" alt=""><figcaption></figcaption></figure>

The main Services page shows an overview of all services that have been added to an instance. Each service is represented by a card which provides status information and allows you to interact with the service.

As new services are added cards will appear on this this page. The service list is also visible in the main menu below the Services menu item.

## Service Cards

<figure><img src="../../../.gitbook/assets/Service card (1).png" alt=""><figcaption></figcaption></figure>

Service cards shown a lot of information about a service and allow you to interact with a service.

### Service ID (SID)

The service ID is a three digit hexadecimal number and is shown in the middle of the coloured service status circle in the top left corner of the card.

### Service Name

The service name is shown at the top of the main body of the card. The name can be set in the service settings and defaults to the service type.

### Service Status

The service status is shown in two places on the card.&#x20;

#### Quick Status Indicator

The coloured circle in the top left corner gives a quick indication of the health of a service. The indicator colours are as follows:

<table><thead><tr><th width="149.2578125">Colour</th><th>Meaning</th></tr></thead><tbody><tr><td><strong>Grey</strong></td><td>Service is disabled and cannot be started</td></tr><tr><td><mark style="color:red;"><strong>Red</strong></mark></td><td>Service is enabled but not started</td></tr><tr><td><mark style="color:orange;"><strong>Amber</strong></mark></td><td>Service is running but has an error</td></tr><tr><td><mark style="color:green;"><strong>Green</strong></mark></td><td>Service is running an OK</td></tr><tr><td><mark style="color:blue;"><strong>Blue</strong></mark></td><td>Service is starting</td></tr></tbody></table>

#### Detailed Status Information

In addition to the quick status indicator, detailed status information is shown in the main body of the card beneath the service name. If a service is in error, the error is shown here.

#### Last Seen

At the bottom left of the main body of the card is a timestamp showing the last time a service interacted with the MobiusFlow instance.

### Service Type

The service type is shown in the top right corner of the main body of the card.&#x20;

In addition the internal Service Profile ID (SPID) which also indicates the service type is shown in the bottom right of the main body of the card&#x20;

### Service Toolbar

With the exception of system services, each service card has a toolbar in the top right. Hovering over the card will highlight the toolbar. The six buttons from left to right are:

<table><thead><tr><th width="163.046875">Button</th><th>Action</th></tr></thead><tbody><tr><td><strong>Start service</strong></td><td>Start a service that is enabled but stopped</td></tr><tr><td><strong>Stop service</strong></td><td>Stop a service that is running</td></tr><tr><td><strong>Hot reload service</strong></td><td>Update a service's objects after a change without stopping the service</td></tr><tr><td><strong>Service settings</strong></td><td>Access the service settings dialog</td></tr><tr><td><strong>Clone service</strong></td><td>Make a copy of a service including all of its objects and settings</td></tr><tr><td><strong>Delete service</strong></td><td>Delete a service and all of its objects</td></tr></tbody></table>

