# swupdate
by Morgan Aldridge <morgant@makkintosshu.com>

## OVERVIEW

A simple utility to roll the various software update related utilities in OpenBSD into a single command, a la macOS's (nee Mac OS X's) [`softwareupdate`](https://ss64.com/osx/softwareupdate.html).

## USAGE

To check for software updates:

    doas swupdate -l

To download, but not install software updates:

    doas swupdate -d

To install all software updates, including system patches and firmware:

    doas swupdate -i

## LICENSE

Released under the [MIT license](LICENSE).
