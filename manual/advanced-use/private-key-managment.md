---
sidebar: manual
---

# Private keys

ACME is all about automation and certificates are typically considered to 
be disposable and easily replacable. There are scenarios though where you
want to manually handle a certificate and its private key.

## Always-accessible private keys
The best way to access the private keys is to configure your renewals to 
save the certificate in an easily transferrable way, e.g. by using the 
[PfxFile](/reference/plugins/store/pfxfile) store plugin. 

If you're using 
the default [CertificateStore](/reference/plugins/store/certificatestore)
plugin you can set `PrivateKeyExportable` to `true` in 
[settings.json](/reference/settings) to enable these certificates to be exported. 


## Migration / disaster recovery
The `PrivateKeyExportable` setting only works for future certificates, 
so if you're in a hurry you can force the renewals using `--renew --force` 
or from the interactive menu to get new certificates with exportable keys.

When renewal is not an option and you need to get the current certificate,
you can find a `.pfx` file in the CertificatePath (which defaults to 
`%programdata%\win-acme\$baseuri$\certificates`). You can access the passwords for 
these cache files from the main menu (`Manage Renewals` > `Show details`) or you 
can decrypt the configuration files (`More options` > `Decrypt`) and 
subsequently find the passwords in the corresponding `.renewal.json` files.

## Reuse private keys
If you don't want your private key to change, you can use the option 
`--reuse-privatekey` when setting up the renewal.