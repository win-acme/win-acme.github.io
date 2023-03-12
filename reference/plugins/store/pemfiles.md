---
sidebar: reference
---

# PemFiles
Designed for [Apache](/manual/advanced-use/examples/apache), nginx and other web servers. 
Exports a `.pem` file for the certificate and private key and places them in 
the path provided by the `--pemfilespath` parameter, or the `Store.PemFiles.DefaultPath` 
setting in [settings.json](/reference/settings). 

Files created are:
- `{name}-crt.pem` (certificate)
- `{name}-key.pem` (private key)
- `{name}-chain.pem` (certificate plus chain)
- `{name}-chain-only.pem` (chain without certificate)

By default `{name}` will be the common name of the certificate (i.e. the primary host 
name), but this may be overruled with the `--pemfilesname` parameter.

You can also optionally have the `-key.pem` file password protected, though you should
make sure that the software you intend to consume the key with supports this as well.

## Unattended
`--store pemfiles [--pemfilespath C:\Certificates\] [--pempassword ******] [--pemfilesname mycert]`