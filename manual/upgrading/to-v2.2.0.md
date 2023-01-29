---
sidebar: manual
---

# Migration from v1.9.x to v2.2.x
You can follow the same instructions as listed for [v1.9.x to v2.1.x](/manual/upgrading/to-v2.1.0).

# Migration from v2.x.x to v2.2.0
Version 2.2.0 is an xcopy update for users of any 2.x.x version.

Custom plugins will have to be modified to conform to the new interfaces of this version of win-acme. 
Also they will have to be targeted to build for .NET7. Note that this does not affect installation or
DNS scripts, only additional `.dll`s.