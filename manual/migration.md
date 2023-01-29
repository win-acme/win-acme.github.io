---
sidebar: manual
---

# Migrating without downtime
To migrate to another machine without downtime, you may follow these steps.
If you're willing to incur some downtime none of this is required, you can
simply install win-acme on the new machine and re-request all certificates
after the DNS has been switched over.

## Pre-migration checklist
- [Decrypt](/manual/advanced-use/encryption) the configuration files. 
- Review [settings.json](/reference/settings) to check if all paths and services 
configured there are available on/from the new machine.
- Review firewalls and other security settings to make sure than win-acme will be able 
to access all the resources it might need for validation (e.g. FTP services, 
Azure Managed Resource Identity, etc.).

## Move program files
The files in the directory that contains `wacs.exe` can be copied to the new machine. 
Alternatively you can download the latest release, but in that case make sure to 
check the [upgrade instructions](/manual/upgrading/) for possible breaking changes to
take into account.

## Move configuration 
Move the configuration files to the new machine. They are stored in the `ConfigPath` 
(typically `%ProgramData%\win-acme\acme-v02.api.letsencrypt.org`, though 
that can be customized in [settings.json](/reference/settings)). Move these files 
to new other machine. 

## Pre-seed certificates
If you're using HTTP validation directly from the old machine (which is most common 
scenario), you will have to update your DNS records* before you can validate host names
on the new machine 

*) Don't forget the AAAA/IPv6 records when doing so!

That means that in theory you won't be able to get certificates before you go "live" 
on the new machine, which is a problem for services that require continuous 
availability. To work around this you can:

- Force renew all certificates on the old machine, 
so that your account will have valid authorizations cached for all domains. Then
on the new machine you will be able to (also) renew and order new certificates 
based on the cached validation results.
- Move the "old" certificates to the new machine, which is easy to accomplish using
the [PemFiles](/reference/plugins/store/pemfiles), 
[PfxFile](/reference/plugins/store/pfxfile) or 
[CentralSsl](/reference/plugins/store/centralssl) store plugins because they allow
you to easily copy over the files. If you're using the default [CertificateStore](/reference/plugins/store/certificatestore)
the process is a bit more difficult though, because you will need to get access to 
the [private keys](/manual/advanced-use/private-key-management).

## Post-migration checklist
- Review the renewal manager to see if all expected renewals are present
- Turn encryption back on (optional, but recommended in most scenarios)
- Run all renewals to check for potential [validation problems](/manual/validation-problems) on the new machine.
- If you are using email notifications, test if settings work from the new server using `More options...` > `Test email notification`