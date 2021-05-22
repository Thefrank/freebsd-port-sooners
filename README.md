# freebsd-port-sooners
FreeBSD ports-built binary packages
# Notice
Please avoid mixing and matching these, ports, and main pkg installs. You will have a bad time.

Jails are easy and quick to make. How about one service per jail? It will help prevent the bad time.

## What is here currently:
- ~~sabnzbdplus 3.2.1 (works around tbb no longer building, feedburner issues)~~ 
  - REMOVED. PORT UPDATED.

- radarr 3.2.0.5048 (dotnet5 variant) (this can be updated via built-in updater)
  - This now tracks "master"! Older versions tracked "nightly"!
  - package named `radarrv3` as a way to deconflict with existing mono-based `radarr`
 
- radarr-devel 3.1.0.4893 (dotnet5 variant) (this can be updated via built-in updater)
  - This currently tracks "develop" to better match FreeBSD port naming

- sonarr 3.0.6.1196 (mono) (`mono6.8>0:lang/mono6.8` instead of `USES=MONO`)
  - This gets rid of the message about using an ancient version of mono. 
  - I will bump this to mono6.12 when it comes to ports, if not handled by maintainer before that.
  - mono < 6.12 contains a security issue on all non-windows platforms.

- Ombi v4 (dotnet5 variant, experimental, binary only NO PKG OR SERVICE)

- jackettdotnet 0.18.98 (dotnet5 variant, experimental, installable txz + service file)
  - different portname! Please `pkg remove jackett` before installing!
  - different service name! Please use `jackettdotnet` for your `sysrc` settings (e.g., `sysrc jackettdotnet_enable=YES`)
  - uses `chown` in service file to set correct user assuming you installed the package as root
  - no way to update: dev currently does not build for FreeBSD so update check will always fail
  
- tautulli 2.7.2 (version bump from 2.5.5, bump python to `USES=python:3.6+`)
  - built under FreeBSD 12.2.
  - bytecompiled python code
  
## Updates
Open a ticket if I fall behind on something. 

Open a ticket if the port has caught up so I can remove the now-duplicated package.

## One more thing
Microsoft does not currently official support dotNET5 on FreeBSD so "dotnet5 variant" packages and binaries might have limited support across FreeBSD versions.
