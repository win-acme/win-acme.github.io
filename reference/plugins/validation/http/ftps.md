---
sidebar: reference
---

# FTP(S)
This plugin uploads the validation challenge to a (secure) FTP server.

{% include validation-http-common.md %}

## Microsoft TLS vs. GnuTLS
If you experience connection issues with Unix FTPS servers, using the GnuTLS library
instead of Microsofts native TLS might solve the problem. [This page](https://github.com/robinrodricks/FluentFTP/wiki/FTPS-Connection-using-GnuTLS) 
by the FluentFTP project explains the reasons behind and limitations of this method.

Using this requires:
   - A change in `settings.config`: `Validation.Ftp.UseGnuTls = true`
   - The pluggable **x64** release of win-acme (it is not available for x86 or ARM due to limitiations of the upstream package, and also doesn't work on the trimmed build) 
   - Download and extract the additonal artifact `gnutls.v{build}.x64.zip`

## Unattended 
`--validation ftp --webroot ftps://x/ --username admin --password ******`