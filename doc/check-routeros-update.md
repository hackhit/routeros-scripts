Notify on RouterOS update
=========================

[◀ Go back to main README](../README.md)

> ℹ️ **Info**: This script can not be used on its own but requires the base
> installation. See [main README](../README.md) for details.

Description
-----------

The primary use of this script is to notify about RouterOS updates.

Run from a terminal you can start the update process or schedule it.

Centrally managing update process of several devices is possibly by
specifying versions safe to be updated on a web server. Versions seen
in neighbor discovery can be specified to be safe as well.

Also installing patch updates (where just last digit is increased)
automatically is supported.

> ⚠️ **Warning**: Installing updates is important from a security point
> of view. At the same time it can be source of serve breakage. So test
> versions in lab and read
> [changelog](https://mikrotik.com/download/changelogs/) and
> [forum](https://forum.mikrotik.com/viewforum.php?f=21) before deploying
> to your production environment! Automatic updates should be handled
> with care!

### Sample notification

![check-routeros-update notification](check-routeros-update.d/notification.svg)

Requirements and installation
-----------------------------

Just install the script:

    $ScriptInstallUpdate check-routeros-update;

And add a scheduler for automatic update notification:

    /system/scheduler/add interval=1d name=check-routeros-update on-event="/system/script/run check-routeros-update;" start-time=startup;

Configuration
-------------

Configuration is required only if you want to control update process with
safe versions from a web server. The configuration goes to
`global-config-overlay`, this is the parameter:

* `SafeUpdateNeighbor`: install updates automatically if seen in neighbor list
* `SafeUpdateOnCap`: check for updates even if device is managed by CAPsMAN
* `SafeUpdatePatch`: install patch updates automatically
* `SafeUpdateUrl`: url to check for safe update, the channel (`long-term`,
`stable` or `testing`) is appended

Also notification settings are required for e-mail,
[matrix](mod/notification-matrix.md) and/or
[telegram](mod/notification-telegram.md).

Usage and invocation
--------------------

Be notified when run from scheduler or run it manually:

    /system/script/run check-routeros-update;

If an update is found you can install it right away.

Installing script [packages-update](packages-update.md) gives extra options.

See also
--------

* [Automatically upgrade firmware and reboot](firmware-upgrade-reboot.md)
* [Manage system update](packages-update.md)

---
[◀ Go back to main README](../README.md)  
[▲ Go back to top](#top)
