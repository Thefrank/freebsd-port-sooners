# freebsd-port-sooners
FreeBSD ports-built binary packages
# Notice
Please avoid mixing and matching these, ports, and main pkg installs. You will have a bad time.

Jails are easy and quick to make. How about one service per jail? It will help prevent the bad time.

# INCOMING CHANGES
Ports built after September 29th 2021 are built with `pkg` >= 1.17.0. 

They will use `pkg` as the file extension and require `pkg` >= 1.17.0.

These port will also more accurately use the canonical default install locations. These changes will be noted for each port.

## What is here currently:
- mono 6.13.0.1212 (tarball Tue Dec 21 19:40:42 UTC 2021)
  - Made from a NIGHTLY tarball. mono 6.12 still does not build cleanly under FreeBSD
  - PROOF OF CONCEPT. FREEBSD 12.2 AMD64 ONLY!
  - If you are a/the port maintainer and would like to adopt this, please contact me for `Makefile`, `pkg-plist`, and `/files`
  - fixed cert install location (/usr/share -> /usr/local), fix build w/o NLS option
  - OPTIONS = BIGARRAY, MONOLITE, NLS, ODBC, SPECTRE, X11
- MSBuild (for Mono!) 16.10.1.52401 (Tarball only, too lazy to update the mess that is the port)
  - from in mono/msbuild 63458bd6cb3a98b5a062bb18bd51ffdea4aa3001
  - no tests done. too lazy. `mono MSBuild.dll` work tho. glhf
- Ombi v4.25.0 (dotnet6 variant, experimental)
  - Now with PKG and Service!
  - Now also only for FreeBSD 13.1 (also works under TrueNAS CORE 13.1)
- jackett 0.20.596 (dotnet6 variant, experimental, installable pkg + service file)
  - different portname! Please `pkg remove jackett` before installing!
  - different service name! Please use `jackettdotnet` for your `sysrc` settings (e.g., `sysrc jackettdotnet_enable=YES`)
  - uses `chown` in service file to set correct user assuming you installed the package as root
  - no way to update: dev currently does not build for FreeBSD so update check will always fail
  - THIS USES THE NEW PKG FORMAT
  - This will see updates far less frequently than jackett actually updates
## What is no longer here:
- ~~sabnzbdplus 3.4.2~~
  - Removed: Ports updated
- ~~radarr v4 (dotnet6 variant)~~
  - @mvanbaak is now the port maintainer and has brought it up to v4! TYVM!
  - This is now in ports as a dotnet binary and can be built from there. Otherwise you can check: https://www.freshports.org/net-p2p/radarr/ to see what it lands on the pkg mirrors
  
- ~~radarr-devel 3.1.0.4893 (dotnet5 variant) (this can be updated via built-in updater)~~
  - Old. Removed.

- ~~sonarr 3.0.6.1335 (mono) (`mono6.8>0:lang/mono6.8` instead of `USES=MONO`)~~
  - PORT NOW USES MONO6.8. REMOVED.
  
- ~~tautulli 2.7.2 (version bump from 2.5.5, bump python to `USES=python:3.6+`)~~
  - REMOVED. PORT UPDATED.

- ~~prowlarr 0.1.1 (dotnet6 variant) (this can be updated via built-in updater)~~
  - REMOVED. Now in ports! TYVM @mvanbaak
  - https://www.freshports.org/net-p2p/prowlarr/

## Where is...?:
- Jellyfin. Please use the repo here: https://github.com/Thefrank/jellyfin-server-freebsd

## Updates
Open a ticket if I fall behind on something. 

Open a ticket if the port has caught up so I can remove the now-duplicated package.

## One more thing
Microsoft does not currently official support dotNET5+ on FreeBSD so "dotnet# variant" packages and binaries might have limited support across FreeBSD versions.
If you would like to help out please drop over to https://github.com/dotnet/runtime/issues/14537 and see if you can.
