# swupdate
by Morgan Aldridge <morgant@makkintosshu.com>

## OVERVIEW

A simple utility to roll the various software update related utilities in [OpenBSD](https://www.openbsd.org/) into a single command, a la macOS's (nee Mac OS X's) [`softwareupdate`](https://ss64.com/osx/softwareupdate.html), including:

* [fw_update(8)](https://man.openbsd.org/fw_update)
* [syspatch(8)](https://man.openbsd.org/syspatch)
* [pkg_add(1)](https://man.openbsd.org/pkg_add)
* [pkg_delete(1)](https://man.openbsd.org/pkg_delete)
* [checkrestart](https://github.com/semarie/checkrestart) (if installed)

## FEATURES

* List, download, or install pending updates for firmware, system patches, and packages
* Works on -release, -stable, or -current
* Upon installation:
  * Checks for any running processes that might have had their binaries updated, if `checkrestart` is installed
  * Prompt to reboot if kernel was updated by `syspatch`
  * Checks for further system patches when `syspatch` has updated itself
  * Deletes any unused package dependencies

## USAGE

To check for software updates:

    doas swupdate -l

To download, but not install software updates:

    doas swupdate -d

To install all software updates, including system patches and firmware:

    doas swupdate -i

## LICENSE

Released under the [MIT license](LICENSE).
