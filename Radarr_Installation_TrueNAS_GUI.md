# Installation overview using TrueNAS GUI
## Overview
Radarr's dotNET version currently does not use the plugin system that TrueNAS uses so this will require more interaction from the user than what normally would be expected.

If you are not comfortable setting up a jail or using the shell please wait until someone adds it to the community plugin libary.

If you are installing from base FreeBSD there is a different guide for that or you can adopt this as an general overview.

This guide will use `Radarrv3-devel` until there is a `master` release for it. `Radarrv3` and `Radarrv3-devel` packages are not compatible with eachother by design.

Going foward, `Radarrv3` will track `master` and `Radarr-devel` will track `develop` to be more consistent with FreeBSD port naming. As of writing THIS IS NOT THE CASE.

## Jail Setup
1. From the main screen select Jails

2. Click ADD

3. Click Advanced Jail Creation

4. Name (any name will work): Radarr

5. Jail Type: Default (Clone Jail)

6. Release: 12.2-Release (or newer)

7. Configure Basic Properties to your liking

8. Configure Jail Properties to your liking but add
- [x] allow_raw_sockets
- [x] allow_mlock

9. Configure Network Properties to your liking

10. Configure Custom Properties to your liking

11. Click Save

## Radarr Installation

Back on the jails list find your newly created jail for `radarr` and click "Shell"

Download the version you want you can find the releases of Radarr here: https://github.com/Thefrank/freebsd-port-sooners/releases

You can just copy and paste the full download URL and `fetch` will be able to download it. Here is an example:

`fetch https://github.com/Thefrank/freebsd-port-sooners/releases/download/20210420/Radarrv3-devel-3.1.0.4893.txz`

Now we install it:

`pkg install Radarrv3-devel-3.1.0.4893.txz`

Don't close the shell out yet we still have a few more things!

## Configuring Radarr

Now that we have it installed a few more steps are required.

### Service Setup

Time to enable the service but before we do a note:

The service file uses `chown` to make sure radarr can update itself. This can break things like `pkg check -s` and `pkg remove` for radarr when the built-in updater replaces files.

To enable the service:

`sysrc radarr_enable=TRUE`

If you do not want to use user/group `radarr` you will need to tell the service file what user/group it should be running under

`sysrc radarr_user="USER_YOU_WANT"`

`sysrc radarr_group="GROUP_YOU_WANT"`

Almost done, let's start the service:

`service radarr start`

If everything went according to plan then radarr should be up and running on the IP of the jail!

(You can now safely close the shell)
