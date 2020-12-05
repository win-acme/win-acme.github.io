---
sidebar: reference
---

# TransIP 
Create the record at TransIP. Note that this provider is not very fast updating its records after 
their API has accepted the changes, so it's highly recommended to roughly double either 
`PreValidateDnsRetryCount` and/or `PreValidateDnsRetryInterval` in `settings.json` when using 
DNS validation through them.

{% include plugin-seperate.md %}

## Setup
This requires you to activate the API in the "my account" section of the control panel and to create
a key pair for win-acme.

## Unattended 
Unattended use of this plugin is currently not supported because it uses a certificate provided in PEM 
(multi-line) format for authentication which is not easily translate to a single command line. If it 
turns out there is demand for this feature we might come up with a solution for that problem.