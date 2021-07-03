---
sidebar: reference
---

# Order plugins

Order plugins are responsible for conversion of your source into one or more actual 
certificate orders. The default behaviour is that each renewal generated a single 
certificate. But in some cases, e.g. when you are close to the 100 domain limit, or you 
don't want visitors of one site to be able to see other host names, you may want to split 
things up. 

Of course this is also possible by setting up multiple renewals, but with proper use of 
source and order plugins the burden of managing certificates for different sites and 
domains can be greatly eased. 

## Default

The default is [single](/reference/plugins/order/single). This can be changed in [settings.json](/reference/settings). 