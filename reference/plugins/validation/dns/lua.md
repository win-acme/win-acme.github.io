---
sidebar: reference
---

# LuaDNS 
Create the record in LuaDNS

{% include plugin-seperate.md %}

## Setup
This assumes you already have your DNS managed in LuaDNS; if not, you'll need to set that up first. If you are 
using the LuaDNS option for validation, you'll need to obtain a user name and API key.

## Unattended 
`--validationmode dns-01 --validation luadns --luadnsusername *** --luadnsapikey ***`