---
sidebar: reference
---

# Command line arguments
Here are all the command line arguments the program accepts.

#### Notes
- Make sure that you are familiar with the basics of [renewal management](/manual/renewal-management) 
  before proceeding with unattended use.
- Arguments documented as such: `--foo [--bar baz|qux]` mean that `--foo` is only 
applicable when `--bar` is set to `baz` or `qux`.

## Main
```
   --baseuri
     Address of the ACMEv2 server to use. The default endpoint
     can be modified in settings.json.

   --import
     Import scheduled renewals from version 1.9.x in unattended
     mode.

   --importbaseuri
     [--import] When importing scheduled renewals from version
     1.9.x, this argument can change the address of the ACMEv1
     server to import from. The default endpoint to import from
     can be modified in settings.json.

   --test
     Enables testing behaviours in the program which may help
     with troubleshooting. By default this also switches the
     --baseuri to the ACME test endpoint. The default endpoint
     for test mode can be modified in settings.json.

   --verbose
     Print additional log messages to console for
     troubleshooting and bug reports.

   --help
     Show information about all available command line options.

   --version
     Show version information.

   --renew
     Renew any certificates that are due. This argument is used
     by the scheduled task. Note that it's not possible to
     change certificate properties and renew at the same time.

   --force
     [--renew] Always execute the renewal, disregarding the 
     validity of the current certificates and the prefered schedule.

   --nocache
     Bypass the cache on certificate requests. Applies to both 
     new requests and renewals.

   --cancel
     Cancel renewal specified by the --friendlyname or --id
     arguments.

   --revoke
     Revoke the most recently issued certificate for the
     renewal specified by the --friendlyname or --id arguments.

   --list
     List all created renewals in unattended mode.

   --encrypt
     Rewrites all renewal information using current
     EncryptConfig setting

   --id
     [--source|--cancel|--renew|--revoke] Id of a new or
     existing renewal, can be used to override the default when
     creating a new renewal or to specify a specific renewal
     for other commands.

   --friendlyname
     [--source|--cancel|--renew|--revoke] Friendly name of a
     new or existing renewal, can be used to override the
     default when creating a new renewal or to specify a
     specific renewal for other commands. In the latter case a
     pattern might be used. You may use a `*` for a range of
     any characters and a `?` for any single character. For
     example: the pattern `example.*` will match `example.net`
     and `example.com` (but not `my.example.com`) and the
     pattern `?.example.com` will match `a.example.com` and
     `b.example.com` (but not `www.example.com`). Note that
     multiple patterns can be combined by comma seperating
     them.

   --source
     Specify which source plugin to run, bypassing the main
     menu and triggering unattended mode.

   --validation
     Specify which validation plugin to run. If none is
     specified, SelfHosting validation will be chosen as the
     default.

   --validationmode
     Specify which validation mode to use. HTTP-01 is the
     default.

   --order
     Specify which order plugin to use. Single is the default.

   --csr
     Specify which CSR plugin to use. RSA is the default.

   --store
     Specify which store plugin to use. CertificateStore is the
     default. This may be a comma-separated list.

   --installation
     Specify which installation plugins to use (if any). This
     may be a comma-separated list.

   --closeonfinish
     [--test] Close the application when complete, which
     usually does not happen when test mode is active. Useful
     to test unattended operation.

   --hidehttps
     Hide sites that have existing https bindings from
     interactive mode.

   --notaskscheduler
     Do not create (or offer to update) the scheduled task.

   --setuptaskscheduler
     Create or update the scheduled task according to the
     current settings.

```
## Account
```
   --accepttos
     Accept the ACME terms of service.

   --emailaddress
     Email address to link to your ACME account.

   --account
     Name for your ACME account. A separate registration and
     signer will be generated for each unique value that you
     provide.

   --eab-key-identifier
     Key identifier to use for external account binding.

   --eab-key
     Key to use for external account binding. Must be base64url
     encoded.

   --eab-algorithm
     Algorithm to use for external account binding. Valid
     values are HS256 (default), HS384, and HS512.

```
# CSR

## Common
```
   --ocsp-must-staple
     Enable OCSP Must Staple extension on certificate.

   --reuse-privatekey
     Reuse the same private key for each renewal.

```
# Installation

## IIS plugin
``` [--installation iis] ```
```
   --installationsiteid
     Specify site to install new bindings to. Defaults to the
     source if that is an IIS site.

   --sslport
     Port number to use for newly created HTTPS bindings.
     Defaults to 443.

   --sslipaddress
     IP address to use for newly created HTTPS bindings.
     Defaults to *.

```
## Script plugin
``` [--installation script] ```
```
   --script
     Path to script file to run after retrieving the
     certificate. This may be any executable file or a
     Powershell (.ps1) script.

   --scriptparameters
     Parameters for the script to run after retrieving the
     certificate. Refer to
     https://win-acme.com/reference/plugins/installation/script
     for further instructions.

```
# Source

## CSR plugin
``` [--source csr] ```
```
   --csrfile
     Specify the location of a CSR file to make a certificate
     for

   --pkfile
     Specify the location of the private key corresponding to
     the CSR

```
## IIS plugin
``` [--source iis] ```
```
   --siteid
     Identifiers of one or more sites to include. This may be a
     comma-separated list.

   --host
     Host name to filter. This parameter may be used to target
     specific bindings. This may be a comma-separated list.

   --host-pattern
     Pattern filter for host names. Can be used to dynamically
     include bindings based on their match with the pattern.You
     may use a `*` for a range of any characters and a `?` for
     any single character. For example: the pattern `example.*`
     will match `example.net` and `example.com` (but not
     `my.example.com`) and the pattern `?.example.com` will
     match `a.example.com` and `b.example.com` (but not
     `www.example.com`). Note that multiple patterns can be
     combined by comma seperating them.

   --host-regex
     Regex pattern filter for host names. Some people, when
     confronted with a problem, think "I know, I'll use regular
     expressions." Now they have two problems.

   --commonname
     Specify the common name of the certificate that should be
     requested for the source. By default this will be the
     first binding that is enumerated.

   --excludebindings
     Exclude host names from the certificate. This may be a
     comma-separated list.

   --host-type
     Specify which types of bindings to consider. May be set to
     http, ftp or both (comma separated)

```
## Manual plugin
``` [--source manual] ```
```
   --commonname
     Specify the common name of the certificate. If not
     provided the first host name will be used.

   --host
     A host name to get a certificate for. This may be a
     comma-separated list.

```
# Store

## Certificate Store plugin
``` [--store certificatestore] ``` (default)
```
   --certificatestore
     This setting can be used to save the certificate in a
     specific store. By default it will go to 'WebHosting'
     store on modern versions of Windows.

   --keepexisting
     While renewing, do not remove the previous certificate.

   --acl-fullcontrol
     List of additional principals (besides the owners of the
     store) that should get full control permissions on the
     private key of the certificate.

```
## Central Certificate Store plugin
``` [--store centralssl] ```
```
   --centralsslstore
     Location of the IIS Central Certificate Store.

   --pfxpassword
     Password to set for .pfx files exported to the IIS Central
     Certificate Store.

```
## PEM files plugin
``` [--store pemfiles] ```
```
   --pemfilespath
     .pem files are exported to this folder.

   --pemfilesname
     Prefix to use for the .pem files, defaults to the common
     name.

   --pempassword
     Password to set for the private key .pem file.

```
## PFX file plugin
``` [--store pfxfile] ```
```
   --pfxfilepath
     Path to write the .pfx file to.

   --pfxfilename
     Prefix to use for the .pfx file, defaults to the common
     name.

   --pfxpassword
     Password to set for .pfx file exported to the folder.

```
## Azure KeyVault
``` [--store keyvault] ```
```
   --vaultname
     The name of the vault

   --certificatename
     The name of the certificate

   --azureenvironment
     This can be used to specify a specific Azure endpoint.
     Valid inputs are AzureCloud (default), AzureChinaCloud,
     AzureGermanCloud, AzureUSGovernment or a specific URI for
     an Azure Stack implementation.

   --azureusemsi
     Use Managed Service Identity for authentication.

   --azuretenantid
     Directory/tenant identifier. Found in Azure AD >
     Properties.

   --azureclientid
     Application/client identifier. Found/created in Azure AD >
     App registrations.

   --azuresecret
     Client secret. Found/created under Azure AD > App
     registrations.

```
## User Store plugin
``` [--store userstore] ```
```
   --keepexisting
     While renewing, do not remove the previous certificate.

```
# Validation

## Credentials
``` [--validation ftp|sftp|webdav] ```
```
   --username
     Username for remote server

   --password
     Password for remote server

```
## Common HTTP validation options
``` [--validation filesystem|ftp|sftp|webdav] ```
```
   --webroot
     Root path of the site that will serve the HTTP validation
     requests.

   --manualtargetisiis
     Copy default web.config to the .well-known directory.

```
## AcmeDns
``` [--validation acme-dns] ```
```
   --acmednsserver
     Root URI of the acme-dns service

```
## Script
``` [--validation script] ```
```
   --dnsscript
     Path to script that creates and deletes validation
     records, depending on its parameters. If this parameter is
     provided then --dnscreatescript and --dnsdeletescript are
     ignored.

   --dnscreatescript
     Path to script that creates the validation TXT record.

   --dnscreatescriptarguments
     Default parameters passed to the script are "create
     {Identifier} {RecordName} {Token}", but that can be
     customized using this argument.

   --dnsdeletescript
     Path to script to remove TXT record.

   --dnsdeletescriptarguments
     Default parameters passed to the script are "delete
     {Identifier} {RecordName} {Token}", but that can be
     customized using this argument.

   --dnsscriptparallelism
     Configure parallelism mode. 0 is fully serial (default), 1
     allows multiple records to be created simultaneously, 2
     allows multiple records to be validated simultaneously and
     3 is a combination of both forms of parallelism.

```
## FileSystem plugin
``` [--validation filesystem] ```
```
   --validationsiteid
     Specify IIS site to use for handling validation requests.
     This will be used to choose the web root path.

```
## SelfHosting plugin
``` [--validation selfhosting] ``` (default)
```
   --validationport
     Port to use for listening to validation requests. Note
     that the ACME server will always send requests to port 80.
     This option is only useful in combination with a port
     forwarding.

   --validationprotocol
     Protocol to use to handle validation requests. Defaults to
     http but may be set to https if you have automatic
     redirects setup in your infrastructure before requests hit
     the web server.

```
## SelfHosting plugin
``` [--validationmode tls-alpn-01 --validation selfhosting] ``` (default)
```
   --validationport
     Port to use for listening to validation requests. Note
     that the ACME server will always send requests to port
     443. This option is only useful in combination with a port
     forwarding.

```
## Azure
``` [--validation azure] ```
```
   --azuresubscriptionid
     Subscription ID to login into Microsoft Azure DNS.

   --azureresourcegroupname
     The name of the resource group within Microsoft Azure DNS.

   --azurehostedzone
     Hosted zone (blank to find best match)

   --azureenvironment
     This can be used to specify a specific Azure endpoint.
     Valid inputs are AzureCloud (default), AzureChinaCloud,
     AzureGermanCloud, AzureUSGovernment or a specific URI for
     an Azure Stack implementation.

   --azureusemsi
     Use Managed Service Identity for authentication.

   --azuretenantid
     Directory/tenant identifier. Found in Azure AD >
     Properties.

   --azureclientid
     Application/client identifier. Found/created in Azure AD >
     App registrations.

   --azuresecret
     Client secret. Found/created under Azure AD > App
     registrations.

```
## Cloudflare
``` [--validation cloudflare] ```
```
   --cloudflareapitoken
     API Token for Cloudflare.

```
## DigitalOcean
``` [--validation digitalocean] ```
```
   --digitaloceanapitoken
     The API token to authenticate against the DigitalOcean
     API.

```
## DnsMadeEasy
``` [--validation dnsmadeeasy] ```
```
   --apikey
     DnsMadeEasy API key.

   --apisecret
     DnsMadeEasy API secret.

```
## Domeneshop
``` [--validation domeneshop] ```
```
   --clientid
     Domeneshop ClientID (token)

   --clientsecret
     Domeneshop Client Secret

```
## Dreamhost
``` [--validation dreamhost] ```
```
   --apikey
     Dreamhost API key.

```
## GoDaddy
``` [--validation godaddy] ```
```
   --apikey
     GoDaddy API key.

   --apisecret
     GoDaddy API secret.

```
## Google Cloud DNS
``` [--validation gcpdns] ```
```
   --serviceaccountkey
     Service Account Key to authenticate with GCP

   --projectid
     Project ID that is hosting Cloud DNS.

```
## Infomaniak
``` [--validation infomaniak] ```
```
   --apitoken
     Infomaniak API token

```
## Linode
``` [--validation linode] ```
```
   --apitoken
     Linode Personal Access Token

```
## LuaDns
``` [--validation luadns] ```
```
   --luadnsusername
     LuaDNS account username (email address).

   --luadnsapikey
     LuaDNS API key.

```
## NS1
``` [--validation ns1] ```
```
   --apikey
     NS1 API key.

```
## Rest plugin
``` [--validation rest] ```
```
   --rest-securitytoken
     The bearer token needed to authenticate with the REST API
     on the server for PUT / DELETE requests.

   --rest-usehttps
     If HTTPS should be used instead of HTTP. Must be true if
     the server has HTTP to HTTPS redirection configured, as
     the redirected request always uses the GET method.

```
## Rfc2136
``` [--validation rfc2136] ```
```
   --serverhost
     DNS server host/ip

   --serverport
     DNS server port

   --tsigkeyname
     TSIG key name

   --tsigkeysecret
     TSIG key secret (Base64 encoded)

   --tsigkeyalgorithm
     TSIG key algorithm

```
## Route53
``` [--validation route53] ```
```
   --route53iamrole
     AWS IAM role for the current EC2 instance to login into
     Amazon Route 53.

   --route53accesskeyid
     Access key ID to login into Amazon Route 53.

   --route53secretaccesskey
     Secret access key to login into Amazon Route 53.

```
## Simply
``` [--validation simply] ```
```
   --account
     Simply Account.

   --apikey
     Simply API key.

```
## TransIp
``` [--validation transip] ```
```
   --transip-login
     Login name at TransIp.

   --transip-privatekey
     Private key generated in the control panel (replace enters
     by spaces and use quotes).

   --transip-privatekeyfile
     Private key generated in the control panel (saved to a
     file on disk).

```