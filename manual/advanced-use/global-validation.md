---
sidebar: manual
---

# Global validation settings
Starting from version 2.2.0, you can configure validation settings to apply for all 
host names across all managed renewals (within the scope of a single ACME service, so 
your `--test` endpoint will still have different settings than the regular one). 

## Motivation
If you want to have a certificate with hosts from domains, with the DNS for each of 
them hosted at a different provider. It's not possible to configure that using the 
regular renewal configuration process, but by setting global validation options for at
least of the hosts, it becomes possible.

Another scenario is when you managed multiple renewals with complicated validation
settings. While the [secret manager](/manual/advanced-use/secret-management) already
provides a good way to rotate secret credentials like API keys, in some cases it's 
also convenient to be able to quickly update non-secret information like paths, user 
names, subscription identifiers etc. in multiple renewals. Or at least to not have to 
input all of that information every time.

## Usage
You can find the validation options in the main menu under `More options...`. From the menu
you can add, edit or remove settings. The settings consist of the regular settings that also
apply to a single renewal, plus:
- A pattern that determines wether or not the settings will apply to a specific host name.
You may use a `*` for a range of any characters and a `?` for any single character. For
example: the pattern `example.*` will match `example.net` and `example.com` (but not 
`my.example.com`) and the pattern `?.example.com` will match `a.example.com` and
`b.example.com` (but not `www.example.com`). Note that multiple patterns can be combined
by comma seperating them.
- A number incidating priority. Settings with a lower value for the priority will be 
processed first, e.g. priority 1 will take preference over priority 2. This is only 
relevant when a hostname matches with multiple patterns.

## Storage
The global validation settings are stored in a file called `validation.json`. Sensitive 
information is encrypted just like in regular `.renewal.json` files.