# CHANGELOG

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

* `swupdate`:
    * List (`-l`), download (`-d`), and install (`-i`) options now all execute
        the new [dbupdate(8)](https://man.openbsd.org/dbupdate) **first**, if
        it is available. This helps ensure that the certificate authority
        database is up-to-date before fetching or installing further updates.
* `CHANGELOG.md`:
    * Added this CHANGELOG file with detailed documentation for all prior
        releases

### Changed

* `swupdate`:
    * `PATH` environment variable is now reset and re-exported to prevent
        poisoning/hijacking. Additionally, the `PATH` is only temporarily
        expanded to include the package localbase paths (e.g. `/usr/local/bin`
        and `/usr/local/sbin`) when working with optional binaries installed
        via pkg_add(1), for example: checkrestart(8).
* `README.md`:
    * Updated to note new support for dbupdate(8)
    * Added new 'Security Precautions' section noting dbupdate(8), `PATH`
        poisoning/hijacking prevention, privilege drop, etc.

## [0.7.1] - 2023-07-06

### Fixed

* When installing updates:
    * Fixed bug in determining whether a file had been modified during
        syspatch(8) execution ([#15](https://github.com/morgant/swupdate-openbsd/issues/15))

### Changed

* Code quality improvements ([#15](https://github.com/morgant/swupdate-openbsd/issues/15))

## [0.7.0] - 2023-07-02

### Added

* When listing/downloading/installing updates:
    * Automatically checks for next newer OpenBSD release which may be
        installed via `sysupgrade` (unless running snapshots or `sysupgrade`
        is not installed; [#2](https://github.com/morgant/swupdate-openbsd/issues/2))
        * If a newer OpenBSD release is found, links to appropriate HTML
            documents for detailed changes, errata, and the upgrade guide
            ([#2](https://github.com/morgant/swupdate-openbsd/issues/2))
* When installing updates:
    * Prompts to install the next newer OpenBSD release via `sysupgrade`, if
        one is found (unless running snapshots or `sysupgrade` is not
        installed; [#2](https://github.com/morgant/swupdate-openbsd/issues/2))

## [0.6.1] - 2023-03-31

**Important**: _Please update to this version of you have v0.6 installed!_

### Added

* Drops root user privileges before executing `ftp` for improved security
    ([#11](https://github.com/morgant/swupdate-openbsd/issues/11))
* Verbose output now states when `syspatch` has been skipped due to running a
    snapshot or post-beta/pre-release

## [0.6.0] - 2023-03-31

**Important**: _This version introduced a potential security vulnerability by
executing `ftp` as the root user. Please update to
[v0.6.1](https://github.com/morgant/swupdate-openbsd/releases/tag/0.6.1)
if you have this version installed!_

### Added

* When listing/downloading updates:
    * Automatically detects when kernel is post-beta/pre-release and skips
        `syspatch`, plus uses snapshots for packages
        ([#8](https://github.com/morgant/swupdate-openbsd/issues/8))
* When installing updates:
    * Automatically detects when kernel is post-beta/pre-release and uses
        snapshots for package updates ([#8](https://github.com/morgant/swupdate-openbsd/issues/8))
* Added `Makefile` ([#9](https://github.com/morgant/swupdate-openbsd/issues/9))

### Fixed

* When installing updates:
    * Only executes `syspatch` a second time if it updated itself
        ([#7](https://github.com/morgant/swupdate-openbsd/issues/7))
    * Rounds up to nearest whole minute when calculating execution time of
        `syspatch` to more accurately detect updated kernel and prompting for
        reboot ([#6](https://github.com/morgant/swupdate-openbsd/issues/6))

## [0.5.0] - 2023-03-29

### Added

* When installing updates:
    * Remove unused package dependencies after install (Issue
        [#1](https://github.com/morgant/swupdate-openbsd/issues/1))

### Fixed

* Fixed error from `fw_update` when listing pending updates (Issue
    [#3](https://github.com/morgant/swupdate-openbsd/issues/3))

### Changed

* When installing updates:
    * Only prompt to reboot if kernel was updated during the execution of
        `syspatch` instead of within the last 15 minutes (Issue
        [#5](https://github.com/morgant/swupdate-openbsd/issues/5))
    * Run `syspatch` a second time if it reports it didn't install any patches
        (which it will do if it updated itself)

## [0.4.0] - 2021-05-27

### Added

* Don't try to list/install syspatches on snapshots
* Use [checkrestart(8)](https://github.com/semarie/checkrestart) after
    install, if available

## [0.3.0] - 2021-02-26

### Added

* Updates firmware prior to applying syspatches

### Fixed

* Safer check for root

## [0.2.0] - 2020-12-22

### Added

* Prompt to reboot after install if kernel was changed

## [0.1.0] - 2020-12-22

* Initial release

[unreleased]: https://github.com/morgant/swupdate-openbsd/compare/0.7.1...master
[0.7.1]: https://github.com/morgant/swupdate-openbsd/compare/0.7...0.7.1
[0.7.0]: https://github.com/morgant/swupdate-openbsd/compare/0.6.1...0.7
[0.6.1]: https://github.com/morgant/swupdate-openbsd/compare/0.6...0.6.1
[0.6.0]: https://github.com/morgant/swupdate-openbsd/compare/0.5...0.6
[0.5.0]: https://github.com/morgant/swupdate-openbsd/compare/0.4...0.5
[0.4.0]: https://github.com/morgant/swupdate-openbsd/compare/0.3...0.4
[0.3.0]: https://github.com/morgant/swupdate-openbsd/compare/0.2...0.3
[0.2.0]: https://github.com/morgant/swupdate-openbsd/compare/0.1...0.2
[0.1.0]: https://github.com/morgant/swupdate-openbsd/releases/tag/0.1
