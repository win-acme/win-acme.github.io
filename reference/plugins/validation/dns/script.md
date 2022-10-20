---
sidebar: reference
---

# Script
Run an external script or program to create or update the validation records.

## Create
A script to create the DNS record must be provided. The arguments passed to the 
script will be `create {Identifier} {RecordName} {Token}` by default, where the
following replacements are made by win-acme:

| Value          |  Replaced with |
|----------------|----------------|
| `{Identifier}` | host name that's being validated, e.g. `sub.example.com`										|
| `{RecordName}` | full name of the TXT record that is being expected, e.g. `_acme-challenge.sub.example.com`	|
| `{ZoneName}`   | registerable domain, e.g. `example.com`														|
| `{NodeName}`   | registerable domain, e.g. `_acme-challenge.sub`												|
| `{Token}`      | content of the TXT record, e.g. `DGyRejmCefe7v4NfDGDKfA`										|     
| `{vault://json/mysecret}`        |  Secret from the [vault](https://www.win-acme.com/manual/advanced-use/secret-management)|

The order and format of arguments may be customized by providing a diffent argument string. 
For example if your script needs arguments like:

`--host _acme-challenge.example.com --token DGyRejmCefe7v4NfDGDKfA`

...your argument string should like like this: 

`--host {RecordName} --token {Token}`

## Delete
Optionally, another script may be provided to delete the record after validation. The arguments passed to the 
script will be `delete {Identifier} {RecordName} {Token}` by default. The order and format of arguments may be 
customized by providing a diffent argument string, just like for the create script. You can also choose to use 
the same script for create and delete, with each their own argument string.

## Parallelism
You can use `--dnsscriptparallelism` to specify if your script supports parallelism. This only has any 
effect when `DisableParallelism` is set to `false` in `settings.config`. You may use the following values:

| Value          |  Meaning |
|----------------|----------------|
| 0 | Serial, default serial behaviour	|
| 1 | Allow multiple new records to created as the same time. Only do this when you are sure that a "create" request will not interfere with others running at the same time |
| 2 | Allow multiple validations to run at the same time. This is possible in theory with any DNS provider, but you must be sure that your script is non-destructive, e.g. it should not overwrite pre-existing TXT records, nor delete more than the one specifically asked for |
| 3 | Combination of 1 and 2 |


## Resources
A lot of good reference scripts are available from the 
[POSH-ACME](https://github.com/rmbolger/Posh-ACME/tree/master/Posh-ACME/DnsPlugins)
project. Note that these scripts are **not compatible** with win-acme. You will have
to make changes (e.g. in terms of accepted parameter and such) in order to use them.

## Unattended
- ##### Create script only
`-validationmode dns-01 --validation script --dnscreatescript c:\create.ps1 [--dnscreatescriptarguments {args}]`
- ##### Create and delete scripts seperate
`-validationmode dns-01 --validation script --dnscreatescript c:\create.ps1 --dnsdeletescript c:\delete.ps1 [--dnscreatescriptarguments {args}] [--dnsdeletescriptarguments {args}]`
- ##### Create-delete script (integrated)
`-validationmode dns-01 --validation script --dnsscript c:\create-and-delete.ps1 [--dnscreatescriptarguments {args}] [--dnsdeletescriptarguments {args}]`