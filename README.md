# freebsd-port-sooners
FreeBSD ports-built binary packages
# Notice
Please avoid mixing and matching these, ports, and main pkg installs. You will have a bad time.

Jails are easy and quick to make. How about one service per jail? It will help prevent the bad time.

## What is here currently:
- sabnzbdplus 3.2.0 (works around tbb no longer building)

- radarr 3.1.0.4625 (dotnet5 variant) (this can be updated via built-in updater)
  - This currently tracks "nightly" but May/June 2021 will track "master" to match FreeBSD port naming better. Avoid using this package until then unless absolutely necessary!
 
- radarr-devel 3.1.0.4893 (dotnet5 variant) (this can be updated via built-in updater)
  - This currently tracks "develop" to better match FreeBSD port naming

- Ombi v4 (dotnet5 variant, experimental, binary only NO PKG OR SERVICE)


## Updates
Open a ticket if I fall behind on something. 

Open a ticket if the port has caught up so I can remove the now-duplicated package.

## One more thing
Microsoft does not currently official support dotNET5 on FreeBSD so "dotnet5 variant" packages and binaries might have limited support across FreeBSD versions.
