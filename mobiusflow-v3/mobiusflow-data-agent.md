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

In the near future it will also allow:

* Generation of alerts
* Generation of graphs / cards to supplement data reports

The Data Agent can accessed via MobiusFlow View. The agent invokes the tools provided by the [Historian MCP Sever](mobiusflow-historian-data-api-v3/mcp-server.md), whilst being powered by an OpenAI LLM.

## Limitations

The Data Agent only knows about the data within MobiusFlow Historian. It does not know anything about the underlying MobiusFlow Engine or its configuration (i.e. the plumbing behind the data). As such, it cannot do the following:

* Reporting of current MobiusFlow Engine configuration
* Reporting of service statuses
* Reporting / advising why a specific device / service is not connecting / not functioning as expected
* Making engine configuration changes such as populating a service or updating an object

Most of the above tasks can achieved via using the [MobiusFlow Engine Agent](mobiusflow-engine-agent.md) instead.

## Requirements for Usage

The agent uses an OpenAI LLM backend. MobiusFlow does not currently manage token usage of this LLM and as such, it is left to customers to manage this themselves.

This means an account on the [OpenAI Platform](https://platform.openai.com/login) is required. Once created, ensure some credit is added to the account so tokens can be consumed by the agent.

The MobiusFlow Data Agent is linked to your OpenAI Platform account via and OpenAI API token. This token can be created on the OpenAI Platform website [here](https://platform.openai.com/settings/organization/api-keys). Once created, this key must be copied and pasted into the Data Agent when prompted:

<figure><img src="../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

If a key is already set but needs to be updated, the key button next to the chat bar should be used:

<figure><img src="../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>
