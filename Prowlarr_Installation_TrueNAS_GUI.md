# Installation overview using TrueNAS GUI
## Overview
Prowlarr's dotNET version currently does not use the plugin system that TrueNAS uses so this will require more interaction from the user than what normally would be expected.

If you are not comfortable setting up a jail or using the shell please wait until someone adds it to the community plugin libary.

If you are installing from base FreeBSD you can adopt this guide as an general overview. TrueNAS uses `iocage` as jail manager so jail properties listed here will use its variable naming.


## Jail Setup
1. From the main screen select Jails

2. Click ADD

3. Click Advanced Jail Creation

4. Name (any name will work): Prowlarr

5. Jail Type: Default (Clone Jail)

6. Release: 12.2-Release (or newer)

7. Configure Basic Properties to your liking

8. Configure Jail Properties to your liking but add
- [x] allow_raw_sockets
- [x] allow_mlock

9. Configure Network Properties to your liking

10. Configure Custom Properties to your liking

11. Click Save

## Prowlarr Installation

Back on the jails list find your newly created jail for `prowlarr` and click "Shell"

As FreeBSD lacks an official reserved UID/GID for Prowlarr we will need to create our own user and group for it

`pw user add prowlarr -c prowlarr -u 349 -d /nonexistent -s /usr/bin/nologin`

Download the version you want. You can find the releases of Prowlarr here: https://github.com/Thefrank/freebsd-port-sooners/releases

You can just copy and paste the full download URL and `fetch` will be able to download it. Here is an example:

`fetch https://github.com/Thefrank/freebsd-port-sooners/releases/download/20210821/prowlarr-0.1.1.842.txz`

Now we install it:

`pkg install prowlarr-0.1.1.842.txz`

Don't close the shell out yet we still have a few more things!

## Configuring Prowlarr

Now that we have it installed a few more steps are required.

### Service Setup

Time to enable the service but before we do, a note:

The service file uses `chown` to make sure prowlarr can update itself. This can break things like `pkg check -s` and `pkg remove` for prowlarr when the built-in updater replaces files.

To enable the service:

`sysrc prowlarr_enable=TRUE`

If you do not want to use user/group `prowlarr` you will need to tell the service file what user/group it should be running under

`sysrc prowlarr_user="USER_YOU_WANT"`

`sysrc prowlarr_group="GROUP_YOU_WANT"`

Almost done, let's start the service:

`service prowlarr start`

If everything went according to plan then prowlarr should be up and running on the IP of the jail (port 9696)!

(You can now safely close the shell)


## Troubleshooting
 - `System.Net.Sockets.SocketException (43): Protocol not supported`
   - Make sure you have `VNET` turned on for your jail.
