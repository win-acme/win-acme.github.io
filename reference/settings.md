---
sidebar: reference
---

# Settings.json
Some of the applications' settings can be modified in a file called `settings.json`. 
If this file is not present when the program starts it will be automatically 
created on first run, copied from `settings_default.json`. This allows you to
xcopy new releases without worrying about overwriting your previously customized 
settings.

## Client

### `ClientName`
Default: `"win-acme"`

The name of the client, which comes back in the scheduled task and the 
`ConfigurationPath`.

### `ConfigurationPath`
Default: `null`

Change the location where the program stores its (temporary) files. If not specified 
this resolves to `%programdata%\{ClientName}\{BaseUri}`. Values should be JSON-encoded, 
e.g. `"C:\\"` (note the double backslash).

### `LogPath`
Default: `null`

The path where log files for the past 31 days are stored. If not 
specified or invalid, this defaults to `{ConfigurationPath}\Log`. 
Values should be JSON-encoded, e.g. `"C:\\"` (note the double backslash).

### `VersionCheck`
Default: `false`

Automatically check for new versions at startup.

## UI

### `DateFormat` 
Default: `"yyyy/M/d H:mm:ss"`

A string that is used to format the date of the certificates friendly 
name. [Documentation](https://msdn.microsoft.com/en-us/library/8kb3ddd4(v=vs.110).aspx) 
for possibilities is available from Microsoft.

### `PageSize`
Default: `50`

The number of items to display per page in list views.

### `TextEncoding`
Default: `"utf-8"`

Encoding to use for the console output. A list of possible values can be
found [here](https://docs.microsoft.com/en-us/dotnet/api/system.text.encoding?view=netcore-3.0).
For certain languages `"unicode"` might give better results displaying the characters,
but note that this reduces compatibility with other programs processing the output.

## ACME

### `DefaultBaseUri`
Default: `"https://acme-v02.api.letsencrypt.org/"`

Default ACMEv2 endpoint to use when none is specified with 
the command line.

### `DefaultBaseUriTest`
Default: `"https://acme-staging-v02.api.letsencrypt.org/"`

Default ACMEv2 endpoint to use when none is specified with
the command line and the `--test` switch is activated.

### `DefaultBaseUriImport`
Default: `"https://acme-v01.api.letsencrypt.org/"`

Default ACMEv1 endpoint to import renewal settings from.

### `PostAsGet`
Default: `true`

Use [POST-as-GET] mode as defined in 
[RFC8555](https://tools.ietf.org/html/rfc8555#section-6.3), 
as required by Let's Encrypt since November 2020.

### `ValidateServerCertificate`
Default: `true`

Set this to `false` to disable certificate validation of the 
ACME endpoint. Note that this is a security risk, it's only
intended to connect to internal/private ACME servers with 
self-signed certificates.

### `RetryCount`
Default: `15`

Maximum numbers of times to refresh validation and order status, while
waiting for the ACME server to complete its tasks.

### `RetryInterval`
Default: `5`

Amount of time in seconds to wait for each retry.

### `PreferredIssuer`
Default: `null`

In some exceptional cases an ACME service will offer multiple certificates
signed by different root authorities. This setting can be used to give a 
preference. I.e. `"ISRG Root X1"` can be used to prefer Let's Encrypt 
self-signed chain over the backwards compatible `"DST Root CA X3"`. Note
that this only really works for Apache and other software that uses .pem
files to store certificates. Windows has its own opinions about how 
chains should be built that are difficult to influence. For maximum
compatibility with legacy clients we recommend using an alternative provider
like [ZeroSSL](https://zerossl.com/).

## Execution

### `DefaultPreExecutionScript`

Path to a script that is executed before renewing a certificate. This may
be useful to temporarely relax security measures, e.g. opening port 80
on the firewall.

### `DefaultPostExecutionScript`

Path to a script that is called after renewing a certificate, this may
be useful to undo any actions taken by the script configured as the 
`DefaultPreExecutionScript`. Not to be confused with the 
[script installation](/reference/plugins/installation/script) plugin.
The difference is that the installation plugin can be configured 
separately for each renewal and has access to a lot more context about 
the new and previous certificates. Also when the installation script fails,
the renewal will be retried later. That is not the case for the pre/post 
execution scripts. Any errors there are logged but otherwise ignored.

## Proxy

### `Url`
Default: `"[System]"`

Configures a proxy server to use for communication with the ACME server and
other HTTP requests done by the program. The default setting (which is equivalent 
to `[wininet]`) uses the proxy as defined by the legacy Windows Internet API. 
You can also `[winhttp]` to use the more modern Windows HTTP API. 
Honestly `[winhttp]` **should** be the default, but isn't because of backwards 
compatiblity. Leaving the value empty/null tries to bypass any proxy. You 
can also configure a specific proxy URL.

### `Username`
Default: `null`

Username used to access the proxy server.

### `Password`
Default: `null`

Password used to access the proxy server. This may be a reference to the
[secret vault](/manual/advanced-use/secret-management).

## Cache

### `Path`
Default: `null`

The path where certificates and request files are cached. If not specified or invalid,
this defaults to `{ConfigurationPath}\Certificates`. If you are using 
[CentralSsl](/reference/plugins/store/centralssl), this can **not** 
be set to the same path. Values should be JSON-encoded, e.g. `"C:\\"`
(note the double backslash).

### `ReuseDays`
Default: `1`

When renewing or re-creating a previously requested certificate that 
has the exact same set of domain names, the program will used a cached 
version for this many days, to prevent users from running into 
[rate limits](https://letsencrypt.org/docs/rate-limits/) while experimenting. 
Set this to a high value if you regularly re-request the same certificates, 
e.g. for a Continuous Deployment scenario.

Setting this to `0` will not entirely disabled the cache (the program also
needs the files for different reasons), but it will prevent the files from being
used for renewals and will also ensure that no private key material is stored in 
the cache, unless specifically requested by parameters like `--reuse-privatekey`.

### `DeleteStaleFiles`
Default: `false`

Automatically delete files older than `{DeleteStaleFileDays}` days from 
the `{CertificatePath}` folder. Running with default settings, these should 
only be long-expired certificates, generated for abandoned renewals. 

### `DeleteStaleFileDays`
Default: `120`

This value should be increased if you are working with long-lived 
certificates.

## Scheduled task

### `RenewalDays`
Default: `55`

The number of days to renew a certificate after. Let's Encrypt certificates are 
currently for a max of 90 days so it is advised to not increase the days much. 
If you increase the days, please note that you will have less time to fix any 
issues if the certificate doesn't renew correctly.

### `RenewalDaysRange`
Default: `0`

To spread service load, program run time and/or to minimize downtime, those 
managing a large amount of renewals may want to spread them out of the course 
of multiple days/weeks. The number of days specified here will be substracted 
from `RenewalDays` to create a range in which the renewal will e processed. 
E.g. if `RenewalDays` is 55 and `RenewalDaysRange` is 10, the renewal will be 
processed between 45 and 55 days after issuing. 

If you use an order plugin to split your renewal into multiple orders, orders 
may run on different days.

### `RenewalDisableServerSchedule`
Default: `false`

By default, servers implementing ARI may suggest that renewals should happen 
earlier than the regularly scheduled moment. When set to `true`, ARI suggestions
will be ignored.

### `RenewalMinimumValidDays `
Default: `null` (which is interpreted as 7 days)

The minimum number of days a certificate should still be valid. If the certificate
is valid for a smaller number of days, it will be renewed regardless of the 
`RenewalDays` setting.

### `StartBoundary`
Default: `"09:00:00"` (9:00 am)

Configures start time for the scheduled task.

### `ExecutionTimeLimit`
Default: `"02:00:00"` (2 hours)

Configures time after which the scheduled task will be 
terminated if it hangs for whatever reason.

### `RandomDelay`
Default: `"04:00:00"` (4 hours)

Configures random time to wait for starting the scheduled task.
This spreads the load on the servers and thus prevents users
from getting `TooManyRequests` errors.

## Notifications

### `SmtpServer`
Default: `null`

SMTP server to use for sending email notifications. 
Required to receive renewal failure notifications.

### `SmtpPort`
Default: `25`

SMTP server port number.

### `SmtpUser`
Default: `null`

User name for the SMTP server, in case of authenticated SMTP.

### `SmtpPassword`
Default: `null`

Password for the SMTP server, in case of authenticated SMTP. 
This may be a reference to the [secret vault](/manual/advanced-use/secret-management).

### `SmtpSecure`
Default: `false`

Change to `true` to enable secure SMTP.

### `SmtpSecureMode`
Default: `1`

| Value          |  Meaning |
|----------------|----------------|
| 1			     | Automatic (based on port number)
| 2			     | Implicit TLS
| 3			     | Explicit TLS (required)
| 4			     | Explicit TLS (when available)

### `SmtpSenderName`
Default: `null`

Display name to use as the sender of notification emails.
Defaults to the `ClientName` setting when empty.

### `SenderAddress`
Default: `null`

Email address to use as the sender of notification emails. 
Required to receive renewal failure notifications.

### `ReceiverAddresses`
Default: `[]`

Email address to receive notification emails. Required to 
receive renewal failure notifications. The correct format 
for the receiver is `["example@example.com"]` for a single 
address and `["example1@example.com", "example2@example.com"]` 
for multiple addresses.

### `EmailOnSuccess`
Default: `false`

Send an email notification when a certificate has been successfully created 
or renewed, as opposed to the default behavior that only send failure 
notifications. Only works if at least `SmtpServer`, `SmtpSenderAddress`
and `SmtpReceiverAddress` have been configured.

### `ComputerName`
Default: `null`

This value replaces the Windows machine name reported in emails.

## Security

### `EncryptConfig`
Default: `true`

Uses Microsoft Data Protection API to encrypt sensitive parts of 
the configuration, e.g. passwords. This may be disabled to share 
the configuration across a cluster of machines.

### `FriendlyNameDateTimeStamp`
Default: `true`

Add the issue date and time to the friendly name of requested certificates. 
If you require full control over the final certificate friendly name this 
feature should be disabled.

## Script

### `Timeout`
Default: `600`

Time in seconds to allow installation and DNS scripts to run before
terminating them forcefully.

### `PowershellExecutablePath`
Default: `powershell.exe`

Customize this value to use a different version of Powershell to
execute `.ps1` scripts. E.g. `C:\\Program Files\\PowerShell\\6.0.0\\pwsh.exe` 
for Powershell Core 6. Values should be JSON-encoded (note the double 
backslashes in the example).

## Source

### `DefaultSource`
Default: `null`

Default source plugin. This only affects the menu in the UI. `null` 
equivalent to `"iis"` with `"manual"` as backup for non-administrators 
or systems without IIS.

## Validation

### `DefaultValidation`
Default: `null`

Default validation plugin, `null` currently equivalent to `"selfhosting"` 
with `"filesystem"` as backup for non-administrators.

### `DefaultValidationMode`
Default: `null`

Default validation method, `null` currently equivalent to `"http-01"`.

### `DisableMultiThreading`
Default: `true`

Disable multithreading features for validation. Inceases runtime but may
help to fix bugs caused by race conditions.

### `CleanupFolders`
Default: `true`

If set to `true`, it will cleanup the folder structure and files it creates 
under the site for authorization.

### `PreValidateDns`
Default: `true`

If set to `true`, it will wait until it can verify that the validation record
has been created and is available before beginning DNS validation.

### `PreValidateDnsRetryCount`
Default: `5`

Maximum numbers of times to retry DNS pre-validation, while
waiting for the name servers to start providing the expected answer.

### `PreValidateDnsRetryInterval`
Default: `30`

Amount of time in seconds to wait between each retry.

### `AllowDnsSubstitution`
Default: `true`

If your goal is to get a certificate for `example.com` using DNS validation, 
but the DNS provider for that domain does not support automation and/or your 
security policy doesn't allow third party tools like win-acme to access the 
DNS configuration, then you can set up a CNAME from `_acme-challenge.example.com` 
to another (sub)domain under your control that doesn't have these limitations. 
[acme-dns](/reference/plugins/validation/dns/acme-dns) is based on this principle, 
but the same trick can be applied to any of the 
[DNS plugins](/reference/plugins/validation/dns/). Set this value to `false` 
to disable the feature.

### `Ftp.UseGnuTls`
Default: `false`

If you experience connection issues with Unix FTPS servers, using the GnuTLS library
instead of Microsofts native TLS might solve the problem. [This page](https://github.com/robinrodricks/FluentFTP/wiki/FTPS-Connection-using-GnuTLS) 
by the FluentFTP project explains the reasons behind and limitations of this method.
Note that it's not enough to merely change this setting, check the documentation of the
[FTP plugin](/reference/plugins/validation/http/ftps) for more details.

### `DnsServers`
Default: `[ "[System]" ]`

A list of servers to query during DNS prevalidation checks to verify whether 
or not the validation record has been properly created and is visible for the 
world. These servers will be used to located the actual authoritative name
servers for the domain. You can use the string `[System]` to have the 
program query your servers default, but note that this can lead to 
prevalidation failures when your Active Directory is hosting a private 
version of the DNS zone for internal use. 

## Order 

### `DefaultOrder`
Default: `null`

Default order plugin, `null` currently equivalent to `"single"`

### `DefaultValidDays`
Default: `null` (server default)

Number of days requested certificates should remain valid. Note that 
not all servers support this property. Specifically Let's Encrypt throws
an error when using this at the time of writing.

## Csr 

### `DefaultCsr`
Default: `null`

Default order plugin, `null` currently equivalent to `"rsa"`

### `Rsa.KeyBits`
Default: `3072`

The number of bits to use for RSA private keys. Minimum is 2048.

### `Rsa.SignatureAlgorithm`
Default: `"SHA512withRSA"`

Algorithm to use to sign CSR with RSA private keys. Full list of possible options available [here](https://github.com/bcgit/bc-csharp/blob/master/crypto/src/cms/CMSSignedGenerator.cs). Note that not all servers will support all types of signatures.

### `Ec.CurveName`
Default: `"secp384r1"`

The curve to use for EC private keys.

### `Ec.SignatureAlgorithm`
Default: `"SHA512withECDSA"`

Algorithm to use to sign CSR with EC private key. Full list of possible options available [here](https://github.com/bcgit/bc-csharp/blob/master/crypto/src/cms/CMSSignedGenerator.cs). Note that not all servers will support all types of signatures.

## Store

### `DefaultStore`
Default: `null`

Default store plugin(s), `null` currently equivalent to `"certificatestore"`. 
This may be a comma separated value for multiple default store plugins.

### `CertificateStore.DefaultStore`
Default: `null`

The certificate store to save the certificates in. If left empty, 
certificates will be installed either in the `WebHosting` store, or 
if that is not available, the `My` store (better known in the
Microsoft Management Console as as `Personal`).

### `CertificateStore.PrivateKeyExportable`
Default: `false`

If set to `true`, certificates stored in the Windows Certificate Store
will be marked as exportable, allowing you to transfer them to other 
computers. Note that this setting doesn't apply retroactively but only
to certificates issued from the moment that setting has changed.
For tips about migration please refer to [this page](/manual/migration).

### `CertificateStore.UseNextGenerationCryptoApi`
Default: `false`

If set to `true`, the program will use the [Cryptography API: Next Generation](https://learn.microsoft.com/en-us/windows/win32/seccng/about-cng) (CNG)
to handle private keys, instead of the legacy CryptoAPI. Note that enabling 
this option may make the certificates unusable or behave differently in subtle 
ways for software that only supports or assumes the key to exist in CryptoAPI. 
For example it will not work for older versions of Microsoft Exchange and it 
won't be exportable from IIS, even if the `PrivateKeyExportable` setting is true.

### `CentralSsl.DefaultPath`
Default: `null`

When using `--store centralssl` this path is used by default, saving you the 
effort from providing it manually. Filling this out makes the `--centralsslstore`
parameter unnecessary in most cases. Renewals created with the default path will 
automatically change to any future default value, meaning this is also a good 
practice for maintainability. Values should be JSON-encoded, e.g. `"C:\\"`
(note the double backslash).

### `CentralSsl.DefaultPassword`
Default: `null`

When using `--store centralssl` this password is used by default for the pfx 
files, saving you the effort from providing it manually. Filling this out makes
the `--pfxpassword` parameter unnecessary in most cases. Renewals created with
the default password will automatically change to any future default value, 
meaning this is also a good practice for maintainability. This may be a reference 
to the [secret vault](/manual/advanced-use/secret-management).

### `PemFiles.DefaultPath`
Default: `null`

When using `--store pemfiles` this path is used by default, saving you the effort 
from providing it manually. Filling this out makes the `--pemfilespath` parameter
unnecessary in most cases. Renewals created with the default path will automatically
change to any future default value, meaning this is also a good practice for
maintainability. Values should be JSON-encoded, e.g. `"C:\\"`
(note the double backslash).

### `PemFiles.DefaultPassword`
Default: `null`

When using `--store pemfiles` this password is used by default for the pfx 
files, saving you the effort from providing it manually. Filling this out makes
the `--pempassword` parameter unnecessary in most cases. Renewals created with
the default password will automatically change to any future default value, 
meaning this is also a good practice for maintainability. This may be a reference 
to the [secret vault](/manual/advanced-use/secret-management).

### `PfxFile.DefaultPath`
Default: `null`

When using `--store pfxfile` this path is used by default, saving you the 
effort from providing it manually. Filling this out makes the `--pfxfilepath`
parameter unnecessary in most cases. Renewals created with the default path will 
automatically change to any future default value, meaning this is also a good 
practice for maintainability. Values should be JSON-encoded, e.g. `"C:\\"`
(note the double backslash).

### `PfxFile.DefaultPassword`
Default: `null`

When using `--store pfxfile` this password is used by default for the pfx 
files, saving you the effort from providing it manually. Filling this out makes
the `--pfxpassword` parameter unnecessary in most cases. Renewals created with
the default password will automatically change to any future default value, 
meaning this is also a good practice for maintainability. This may be a reference 
to the [secret vault](/manual/advanced-use/secret-management).

## Installation

### `DefaultInstallation`
Default: `null`

Default installation plugin(s), `null` currently equivalent to `"none"` for 
unattended usage and `"iis"` for interactive mode. This may be a comma 
separated value for multiple default installation plugins.

# Secrets

## Json

### FilePath

Default: `null`

Location of the file store secrets. If undefined, defaults to 
`{ConfigurationPath}\secrets.json`
