---
sidebar: reference
---

# PemFiles
Designed for [Apache](/manual/advanced-use/examples/apache), nginx and other web servers. 
Exports a `.pem` file for the certificate and private key and places them in 
the path provided by the `--pemfilespath` parameter, or the `Store.PemFiles.DefaultPath` 
setting in [settings.json](/reference/settings). 

## Unattended
`--store pemfiles [--pemfilespath C:\Certificates\]`