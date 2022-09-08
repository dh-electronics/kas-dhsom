KAS configuration for DH electronics platforms
==============================================

This repository provides KAS configuration for DH electronics platforms.

# Building OE image
-------------------

The [KAS](https://github.com/siemens/kas) tool downloads select OE layers, emits
matching bblayers.conf and local.conf, sets up required OE build variables and
even executes the build. The tool also provides menu-based build configuration.

A good starting point for setting up the build using KAS is the KAS documentation,
namely [Introduction](https://kas.readthedocs.io/en/latest/intro.html),
[User Guide](https://kas.readthedocs.io/en/latest/userguide.html),
[Command line usage](https://kas.readthedocs.io/en/latest/command-line.html) and
[Environment variables](https://kas.readthedocs.io/en/latest/command-line.html#environment-variables).

First, install KAS to current user local bin directory:

```
$ pip3 install kas
```

Second, clone this metalayer git repository into a location accessible to the build system.

```
$ git clone https://github.com/dh-electronics/kas-dhsom.git -b main
```

Third, configure the build parameters, especially the work directory where the
build stores all the data. This directory must have sufficient amount of space,
around 25 GiB for basic build and 100 GiB for build with all examples.

The `kas menu` command displays an ncurses-based menu, which offers selection of
one of MACHINEs supported by this metalayer and the option to perform full build
including [meta-dhsom-extras](https://github.com/dh-electronics/meta-dhsom-extras)
example and demonstration layer. Select suitable MACHINE (use SPACEBAR to change
the selection), optionally enable full build (takes longer and requires extra
disk space), and use either `Save & Build` or `Save & Exit` button to save
changes and exit the menu (use TAB key to navigate the buttons).

```
$ export KAS_WORK_DIR=/path/to/work/directory/
$ cd kas-dhsom/
$ PATH=${PATH}:~/.local/bin kas menu
```

The `*** Inferred and expert settings ***` section does not need to be changed.

The `Save & Build` button stores the build configuration in `${KAS_WORK_DIR}/.config.yaml`
and immediately triggers default build target for the selected configuration.
The `Save & Exit` button stores the build configuration and exits, the KAS build
can then be resumed using KAS [build](https://kas.readthedocs.io/en/latest/command-line.html#build)
command, `kas build`.
