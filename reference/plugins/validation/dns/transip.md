---
sidebar: reference
---

# TransIP 
Create the record at [TransIP](https://www.transip.nl/). Note that this provider is not very fast updating its records after 
their API has accepted the changes, so it's highly recommended to roughly double either 
`PreValidateDnsRetryCount` and/or `PreValidateDnsRetryInterval` in `settings.json` when using 
DNS validation through them.

{% include plugin-seperate.md %}

## Setup
This requires you to activate the API in the "my account" section of the control panel and to create
a key pair for win-acme.

## Unattended 
- Key inline
`--validation transip --transip-login xx --transip-privatekey `"---- PRIVATE KEY --- ...`"`
- Key in file:
`--validation transip --transip-login xx --transip-privatekey C:\transip.key`