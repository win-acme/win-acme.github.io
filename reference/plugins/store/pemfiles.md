---
sidebar: reference
---

# PemFiles
Designed for [Apache](/manual/advanced-use/examples/apache), nginx and other web servers. 
Exports a `.pem` file for the certificate and private key and places them in 
the path provided by the `--pemfilespath` parameter, or the `Store.PemFiles.DefaultPath` 
setting in [settings.json](/reference/settings). 

Files created are:
- `{CommonName}-crt.pem` (certificate)
- `{CommonName}-key.pem` (private key)
- `{CommonName}-chain.pem` (certificate plus chain)
- `{CommonName}-chain-only.pem` (chain without certificate)

You can optionally have the `-key.pem` file password protected.

## Unattended
`--store pemfiles [--pemfilespath C:\Certificates\] [--pempassword ******]`