---
description: What are the mobius, manage, and mongodb microservices
---

# Installed Services

balenaCloud devices can run multiple microservices in separate Docker containers. Deploying **Mobius**Flow® to your device will create three microservices. You can start, stop and view logs for each service on the **balenaCloud device summary** page.

<figure><img src="../../.gitbook/assets/Balena Microservices.png" alt=""><figcaption><p>MobiusFlow® Microservices</p></figcaption></figure>

## mobius

This microservice runs the **Mobius**Flow® application.&#x20;

## manage

Manages network interfaces. See [Configure Networks](configure-networks.md) for more information

## mongodb

A full version of MongoDB which you can use to store / retrieve data in flows.

The default settings are

<table><thead><tr><th>Setting</th><th>Default Value</th><th data-hidden></th></tr></thead><tbody><tr><td>Database</td><td>mobius</td><td></td></tr><tr><td>Username</td><td>mobius</td><td></td></tr><tr><td>Password</td><td>RmzsXQYReLHaCS5wWGjAPjtJ7VnTw4qL</td><td></td></tr></tbody></table>
