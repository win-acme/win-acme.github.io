---
sidebar: manual
---

# Secrets

Some plugins require authentication information such as a password or API key
to be able to work, e.g. to login to an FTP server or to update a DNS record.
These secrets are historically saved in [encrypted](/manual/advanced-use/encryption) 
form in the [.renewal.json](/manual/advanced-use/renewal-management) files in the 
configuration folder.

There are also some global secrets, like the proxy server password and the smpt 
server password, that are stored in [settings.json](/reference/settings).

## Central Management

Version 2.1.17 introduced the secret manager to make it easier to re-use and manage
secrets for renewals. Also it makes it possible to protect those aformentioned global 
secrets. The secret manager can be accessed from the main menu by going to 
`More options...` > `Manage secrets`. There you will be presented with a list of currently 
known secrets (if any) to update/delete them, and an option to add a new one. Each secret 
has a unique URI like `vault://json/mysecret` which you can use in various places like 
configuration files, command line arguments or script installation parameters.

## Multiple backends

Currently there is only a single backend for the secret manager, which is a `.json` file 
in the configuration folder. The location of that file may be modified through
[settings.json](/reference/settings), for example if you want to share it between different
ACME endpoints. In the future the idea is to support more backends like Azure KeyVault.