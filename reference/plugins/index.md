---
sidebar: reference
---

# Plugins

Conceptually win-acme works by chaining together five components also known as plugins, which can be mixed and matched to support many use cases.

- A [target plugin](/reference/plugins/target/) provides information about (potential) certificates to create.
- A [validation plugin](/reference/plugins/validation/) provides the ACME server with proof that you own the domain(s).
- A [CSR plugin](/reference/plugins/csr/) determines the (type of) private key and extensions to use for the certificate.
- One or more [store plugins](/reference/plugins/store/) place the certificate in a specific location and format.
- One or more [installation plugins](/reference/plugins/installation/) make changes to your application(s) configuration.
