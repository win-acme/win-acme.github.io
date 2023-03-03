---
sidebar: reference
---

# PfxFile
Exports a `.pfx` archive including the certificate, its private key and the chain, 
and places it in the path provided by the `--pfxfilepath` parameter, or the 
`Store.PfxFile.DefaultPath` setting in [settings.json](/reference/settings). 

By default the file name will be the common name of the certificate (i.e. 
the primary host name), but this may be overruled with the `--pfxfilename` parameter.

## Unattended
`--store pfxfile [--pfxpassword *****] [--pfxfilepath C:\Certificates\] [--pfxfilename mycert]`
