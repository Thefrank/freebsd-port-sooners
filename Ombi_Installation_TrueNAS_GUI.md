# Installation overview using TrueNAS GUI
## Overview
Ombi currently does not use the plugin system that TrueNAS uses so this will require more interaction from the user than what normally would be expected.

If you are not comfortable setting up a jail or using the shell please wait until someone adds it to the community plugin libary.

If you are installing from base FreeBSD you can adopt this guide as an general overview. TrueNAS uses `iocage` as jail manager so jail properties listed here will use its variable naming.

dotNET binaries should work in jails on FreeBSD kernel 11.3+. FreeNAS/TrueNAS users should use 12.2+ as the previous statement does not apply to you!

Ombi requires `e_sqlite3` which is not buildable for FreeBSD. However, the `sqlite3` package contains something that is "close enough". The installer will create a symlink `/usr/local/lib/libe_sqlite3.so` to help resolve this.

Finally, a UID/GID for Ombi is created by the installer. The UID/GID used is CURRENTLY marked as "free" so it should not cause conflicts.

## Jail Setup
1. From the main screen select Jails

2. Click ADD

3. Click Advanced Jail Creation

4. Name (any name will work): Ombi

5. Jail Type: Default (Clone Jail)

6. Release: 12.2-Release (or newer)

7. Configure Basic Properties to your liking add but add

- [x] VNET

  - (While this is not a hard requirement, you may encouter networking issues. See: troubleshooting )

8. Configure Jail Properties to your liking but add
- [x] allow_raw_sockets

  - (Highly suggested for easier troubleshooting)
  
- [x] allow_mlock

  - (This is REQUIRED)
  
9. Configure Network Properties to your liking

10. Configure Custom Properties to your liking

11. Click Save

## Ombi Installation

Back on the jails list find your newly created jail for `Ombi` and click "Shell"

Download the version you want. You can find the releases of Ombi here: https://github.com/Thefrank/freebsd-port-sooners/releases

You can just copy and paste the full download URL and `fetch` will be able to download it. Here is an example:

`fetch https://github.com/Thefrank/freebsd-port-sooners/releases/download/20211221/ombi-4.7.11.pkg`

Now we install it:

`pkg install ombi-4.7.11.pkg`

Don't close the shell out yet we still have a few more things!

## Configuring Ombi

Now that we have it installed a few more steps are required.

### Service Setup

Time to enable the service but before we do, a note:

The service file uses `chown` to make sure Ombi can update itself. This can break things like `pkg check -s` and `pkg remove` for Ombi when the built-in updater replaces files.

To enable the service:

`sysrc ombi_enable=TRUE`

If you do not want to use user/group `Ombi` you will need to tell the service file what user/group it should be running under

`sysrc ombi_user="USER_YOU_WANT"`

`sysrc ombi_group="GROUP_YOU_WANT"`

`Ombi` stores its data, config, logs, and PID files in `/var/db/ombi` by default. The service file will create this and take ownership of it IF AND ONLY IF IT DOES NOT EXIST. If you want to store these files in a different place (e.g., a dataset mounted into the jail for easier snapshots) then you will need to change it using `sysrc`

`sysrc ombi_data_dir="DIR_YOU_WANT"`

Reminder: If you are using an existing location then you will manually need to either: change the ownership to the UID/GID `Ombi` uses AND/OR add `Ombi` to a GID that has write access.

Almost done, let's start the service:

`service ombi start`

If everything went according to plan then Ombi should be up and running on the IP of the jail (port 5000)!

(You can now safely close the shell)


## Troubleshooting
 - `System.Net.Sockets.SocketException (43): Protocol not supported`
   - Make sure you have `VNET` turned on for your jail.
   - If you do not use `VNET` then setting `ip6=inherit` for the jail should also fix this.
 - `libe_sqlite3` errors
   - In rare cases, the installer might fail to make the symbolic link needed to run Ombi. Try `ln -s /usr/local/lib/libsqlite3.so /usr/local/lib/libe_sqlite3.so`
