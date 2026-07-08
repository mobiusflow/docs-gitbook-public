---
description: This page explains the MobiusFlow Data Agent found in MobiusFlow View
---

# MobiusFlow Data Agent

## Overview

The Data Agent introduces an agentic / chat style interface to interact with your MobiusFlow data. The enables tasks such as:

* Reporting what data exists
* Summarising data, both present and historical
* Making data comparisons between multiple data sets
* Drawing conclusions about the nature of data
* Making suggestions about changes which could be made to improve real-world systems
* Generation of graphs supplement data reports

In the near future it will also allow:

* Generation of alerts
* Populating dashboards with formatted cards

The Data Agent can accessed via MobiusFlow View. The agent invokes the tools provided by the [Historian MCP Sever](mobiusflow-historian-data-api-v3/mcp-server.md), whilst being powered by a OpenAI / Anthropic / Google Gemini LLM.

## Limitations

The Data Agent only knows about the data within MobiusFlow Historian. It does not know anything about the underlying MobiusFlow Engine or its configuration (i.e. the plumbing behind the data). As such, it cannot do the following:

* Reporting of current MobiusFlow Engine configuration
* Reporting of service statuses
* Reporting / advising why a specific device / service is not connecting / not functioning as expected
* Making engine configuration changes such as populating a service or updating an object

Most of the above tasks can achieved via using the [MobiusFlow Engine Agent](mobiusflow-engine-agent.md) instead.

## Requirements for Usage

The agent uses an a commercial LLM backend provided by one of the following provider:

* Open AI
* Anthropic
* Google Gemini

MobiusFlow does not currently manage token usage of these LLMs and as such, this is left to customers to manage this themselves. This means an account with one of the 3 providers is required. Once created, ensure some credit is added to the account so tokens can be consumed by the agent.

The MobiusFlow Data Agent is linked to your LLM provider via an API token. This token can be created on your chosen provider's respective platform. Once created, this API key must be copied and pasted into the Data Agent's settings page:

<figure><img src="../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

On the settings page you'll be asked to pick a provider / LLM model and set the API Key:

<figure><img src="../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

Ensure a valid API key is set for the chosen provider otherwise the agent will not function.

{% hint style="info" %}
Note: Updating the chat settings will cause the page to reload. Your ongoing chat will not be lost.
{% endhint %}
