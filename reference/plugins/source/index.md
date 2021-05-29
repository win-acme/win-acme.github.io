---
sidebar: reference
---

# Source plugins

A source plugin is responsible for providing information about a (potential) certificate to the rest of the program. 
Its primary purpose is to determine which host names should be included in the SAN list, but can also provide extra 
information such as the preferred common name or bindings to exclude.

## Default

There is no default source plugin, it always has to be chosen by the user, either using the `--source` 
parameter that triggers unattended mode, or using the "Create renewal" menu. The default plugin 
suggested by the UI can be changed in [settings.json](/reference/settings).