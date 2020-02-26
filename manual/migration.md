---
sidebar: manual
---

# Migration
To migrate to another machine, first make sure to [decrypt](/manual/advanced-use/encryption) 
the configuration files. They are stored in the `ConfigPath` which typically means 
`%ProgramData%\win-acme\acme-v02.api.letsencrypt.org`, though that can be changed in 
[settings.json](/reference/settings). Move these files to the other machine and then 
(optionally) turn encryption back on.

## Checklist after migrating
- Review the renewal manager to see if all expected renewals are present
- Run all renewals to check for potential [validation problems](/manual/validation-problems) on the new machine
- Test your email notification settings (if any) from the main menu