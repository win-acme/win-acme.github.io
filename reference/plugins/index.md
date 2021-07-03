---
sidebar: reference
---

# Plugins

Conceptually win-acme works by chaining together five components also known as plugins, which can be 
mixed and matched to support many use cases. Using the "default settings" mode of the UI, the default 
for each plugin will be chosen for you. These defaults can be changed in [settings.json](/reference/settings). 

In "full options" mode, you will be asked to pick each of these plugins. 

From the command line you can also rely on the configured defaults or explicitly provide which 
one(s) you want. Check the [command line reference](/reference/cli) to see how.

- A [source plugin](/reference/plugins/source/) determines which domains to include in the renewal.
- An [order plugin](/reference/plugins/order/) divides these domains over one or more certificates to be ordered.
- A [validation plugin](/reference/plugins/validation/) provides the ACME server with proof that you own the domain(s).
- A [CSR plugin](/reference/plugins/csr/) determines the (type of) private key and extensions to use for the certificate(s).
- One or more [store plugins](/reference/plugins/store/) place the certificate(s) in a specific location and format.
- One or more [installation plugins](/reference/plugins/installation/) make changes to your application(s) configuration.

## Pluggable vs. Trimmed releases

A lot of plugins are built-in, but some plugins are distributed as optional extra downloads. 
When using one of the extra downloads, it's required to use the "pluggable" releases of the 
main program. Otherwise you may use the "trimmed" releases to save space.