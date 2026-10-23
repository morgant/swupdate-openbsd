# swupdate
by Morgan Aldridge <morgant@makkintosshu.com>

[![swupdate-openbsd on OpenHub](https://openhub.net/p/swupdate-openbsd/widgets/project_thin_badge.gif)](https://openhub.net/p/swupdate-openbsd)

## OVERVIEW

A simple utility to roll the various software update related utilities in
[OpenBSD](https://www.openbsd.org/) into a single command, a la macOS's (nee
Mac OS X's) [`softwareupdate`](https://ss64.com/osx/softwareupdate.html),
including:

* [dbupdate(8)](https://man.openbsd.org/dbupdate)
* [fw_update(8)](https://man.openbsd.org/fw_update)
* [syspatch(8)](https://man.openbsd.org/syspatch)
* [pkg_add(1)](https://man.openbsd.org/pkg_add)
* [pkg_delete(1)](https://man.openbsd.org/pkg_delete)
* [sysupgrade(8)](https://man.openbsd.org/sysupgrade)
* [checkrestart](https://github.com/semarie/checkrestart) (if installed)

## Update-verse

```
One script for base developers providing system binary patches,
One for non-free driver firmware available from the Internet,
Three for third-party binary packages built via ports infrastructure,
One for upgrading to the next major OpenBSD release or snapshot,
One for the system administrator in their dark terminal
On the OpenBSD operating system where software needs an update.
  One script to run them all, One script to find them,
  One script to download them all, and from the shell install them
On the OpenBSD operating system where software needs an update.
```

(My apologies for the blasphemous merging of Tolkien's ring verse
with OpenBSD's manual pages for the various software updare scripts.)

## FEATURES

* List, download, or install pending updates for system databases, firmware,
    system patches, packages, and new major releases
* Works on -release, -stable, or -current
* Automatically uses snapshots when running a post-beta/pre-release kernel
* Upon installation:
  * Installs additional system patches when `syspatch` has updated itself
  * Uninstalls any unused package dependencies
  * Checks for any running processes which might have had their binaries
    updated (if `checkrestart` is installed)
  * Prompts to reboot if kernel was updated by `syspatch`
  * Prompts to install next major release upgrade via `sysupgrade`, if
    available

## SECURITY PRECAUTIONS

* Prevents `PATH` poisoning/hijacking
* Drops root user privileges before fetching data via [ftp(1)](https://man.openbsd.org/ftp)
    (syspatch(8) and sysupgrade(8) also do the same)
* Deliberate order of operations, especially:
    * dbupdate(8) is **always** run first, if available, to ensure that system
        certificate authority databases and such are up-to-date
    * fw_update(8) and syspatch(8) updates are prioritized above package
        updates

## USAGE

To check for and list pending software updates:

    doas swupdate -l

To download, but not install, pending software updates:

    doas swupdate -d

To install all pending software updates, including system databases, patches,
and firmware:

    doas swupdate -i

## LICENSE

Released under the [MIT License](LICENSE).
