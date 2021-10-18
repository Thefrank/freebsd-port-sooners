# freebsd-port-sooners
FreeBSD ports-built binary packages
# Notice
Please avoid mixing and matching these, ports, and main pkg installs. You will have a bad time.

Jails are easy and quick to make. How about one service per jail? It will help prevent the bad time.

# INCOMING CHANGES
Ports built after September 29th 2021 are built with `pkg` >= 1.17.0. 

They will use `pkg` as the file extension and require `pkg` >= 1.17.0.

These port will also more accurately use the canonical default install locations. These changes will be noted for each port.

ALSO: Radarr and Prowlarr might be getting added to the official ports tree! See https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=259194 and https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=259196

## What is here currently:
- mono 6.13.0.1201 (tarball Mon Oct 18 00:41:00 UTC 2021)
  - Made from a NIGHTLY tarball. mono 6.12 still does not build cleanly under FreeBSD
  - PROOF OF CONCEPT. FREEBSD 12.2 AMD64 ONLY!
  - If you are a/the port maintainer and would like to adopt this, please contact me for `Makefile` and `pkg-plist`
- sabnzbdplus 3.4.1
  - Version bump. 
  - THIS USES THE NEW PKG FORMAT
  - NOTE: This needs TWO python3 packages from pip that are not in ports: `puremagic` and `guessit`. You will need to `pkg install py38-pip` if you do not have it either
   - `python3.8 -m pip install puremagic` && `python3.8 -m pip install guessit`. If you just want to copy/paste.

- radarr 3.2.2.5080 (dotnet5 variant) (this can be updated via built-in updater)
  - This now tracks "master"! Older versions tracked "nightly"!
  - package named `radarrv3` as a way to deconflict with existing mono-based `radarr`
   - still uses same name for service file to stop people from trying to install one over the other
  - now actually complies with `portfmt` and `portlint`
 
- radarr-devel 3.1.0.4893 (dotnet5 variant) (this can be updated via built-in updater)
  - This currently tracks "develop" to better match FreeBSD port naming

- ~~sonarr 3.0.6.1335 (mono) (`mono6.8>0:lang/mono6.8` instead of `USES=MONO`)~~
  - PORT NOW USES MONO6.8. REMOVED.

- Ombi v4 (dotnet5 variant, experimental, binary only NO PKG OR SERVICE)

- jackett 0.18.475 (dotnet5 variant, experimental, installable txz + service file)
  - different portname! Please `pkg remove jackett` before installing!
  - different service name! Please use `jackettdotnet` for your `sysrc` settings (e.g., `sysrc jackettdotnet_enable=YES`)
  - uses `chown` in service file to set correct user assuming you installed the package as root
  - no way to update: dev currently does not build for FreeBSD so update check will always fail
  - This will see updates far less frequently that jackett actually updates
  
- ~~tautulli 2.7.2 (version bump from 2.5.5, bump python to `USES=python:3.6+`)~~
  - REMOVED. PORT UPDATED.

- prowlarr 0.1.1.978 (dotnet5 variant) (this can be updated via built-in updater)
  - If you are using a package of prowlarr from BEFORE 2021-09-16 then I suggest a fresh install. 
   - I changed where `prowlarr` stores its data. It can now be updated without giving warnings. CHECK THE RC FILE FOR THE NEW DEFAULTS!
   - It now uses `prowlarrdotnet` for service/pkg name.
  - This currently tracks "develop" as there is no stable release for this yet
  - Now actually complies with `portfmt` and `portlint`
  - More info: https://github.com/Prowlarr/Prowlarr

## What is NOT here:
- Jellyfin. Please use the repo here: https://github.com/Thefrank/jellyfin-server-freebsd

## Updates
Open a ticket if I fall behind on something. 

Open a ticket if the port has caught up so I can remove the now-duplicated package.

## One more thing
Microsoft does not currently official support dotNET5+ on FreeBSD so "dotnet# variant" packages and binaries might have limited support across FreeBSD versions.
If you would like to help out please drop over to https://github.com/dotnet/runtime/issues/14537 and see if you can.
