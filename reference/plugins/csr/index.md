---
sidebar: reference
---

# CSR plugins

CSR plugins are responsible for providing certificate requests that the ACME server can sign. 
They determine key properties such as the private key, applications and extensions. When 
a CSR is used as [target](/reference/plugins/target/csr), no CSR plugin can be chosen
and the third party application is expected to take care of the private key and extensions instead.

## Default

The default is an [RSA](/reference/plugins/csr/rsa) private key.
