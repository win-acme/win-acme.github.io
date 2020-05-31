---
sidebar: reference
---

# Host
Generates an order/certificate for each registerable domain found in the target. 
For example when there are five hosts in the target:

- sub.example.com
- another.sub.example.com
- sub.contoso.net
- *.contoso.net
- *.contoso.co.uk

Three certificates will be generated: one for `example.com`, one for `contoso.net` and one for `contoso.co.uk`.

Not compatible with custom CSR targets.

## Unattended
`--order domain`