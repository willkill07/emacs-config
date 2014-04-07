emacs-config-switcher
=====================

An emacs configuration backup / switcher

Installation:
-------------

Place `emacs-config` into your user bin directory (`~/bin`) or another favorite location and add it to your `PATH`


Usage:
------

  `emacs-config [flag]`

Flags:
------

`-h`       - show help

`-i <tag>` - initialize configuration manager and create configuration called `<tag>`

`-b <tag>` - backup current configuration to <tag>

`-L`       - list current configurations

`-a <tag>` - make `<tag>` the active configuration

`-r <tag>` - remove `<tag>`

Note: only one flag is supported at a time
