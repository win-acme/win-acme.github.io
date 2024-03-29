﻿## Separate download

This plugin is offered as a separate download, which can be downloaded from the 
[releases](https://github.com/win-acme/win-acme/releases/) page on GitHub has to 
be unpacked into the folder where you also unpacked `wacs.exe` to able to use them. 
If you are using win-acme as a dotnet tool, you will have to unpack to 
`%userprofile%\.dotnet\tools\.store\win-acme\{version}\win-acme\{version}\tools\net5.0\any`

Note that after unpacking you may have to unblock all new .dll files before .NET 
will trust them. You can do that from the Windows File Explorer by using the right 
mouse button and then checking the `Unblock` box on the General tab.

![image](/assets/unblock-dll.png)

## Using a downloaded plugin

To verify that the plugin is properly installed you can start the main executable 
with `--verbose` and it will print information about found and loaded plugins at 
start up. When the plugin is loaded, it manifests itself as extra menu choices and
command line parameters being made availalbe.

## Requires pluggable release

This plugin requires to you use the `pluggable` release of the main executable. It
will not work on the smaller `trimmed` releases.
