graalvm-ce
=====

This repository provides the contents of the online packages for Oracle's [GraalVM Community Edition](https://github.com/oracle/graal), which is serviced via [Launchpad PPA repository](https://launchpad.net/graalvm-ce) and accesable with `apt` package tool.

As of present, the latest version is `22.1.0` and java11, java17 based packages are provided.

These packages download appropriate GraalVM distribution on each installation from github; For the offline packages which contains the whole contents in the package, please refer [here](https://github.com/dongjinleekr/graalvm-ce-deb).

# How to use

```
# Add a PPA Repository
sudo add-apt-repository ppa:dongjinleekr/graalvm-ce

# Install Java 11 based distribution
sudo apt -y install graalvm-ce-java11
```

# Contents description

This package provides all graalvm ce binaries along with the additional ones.

The binaries provided in this repo are categorized into the following groups:

## Standard Java binaries

All standard java binaries in the JDK distributions are also provided by graalvm-ce and, in turn, by these packages.

Since the package additionally provides an appropriate `jinfo` file in `/usr/lib/jvm/`, you can switch the HOME directory of the default java distribution:, like:

```
# List all installed java distributions
sudo update-java-alternatives --list

# Switch the standard java binaries like java, javac, ... to the ones under `{java_home}/bin` at once
sudo update-java-alternatives --set {java_home}
```

## Standard GraalVM tools

These binaries are built-in to the GraalVM CE distribution, but not part of standard java

- `gu`: installs and updates the graalvm submodules.
- `js`
- `lli`: executes plain bitcode files in GraalVM.
- `polyglot`

## Truffle Language Implementations

These language implementations are written with the Truffle framework and run in GraamVM. They can be accessed with a `graal-` prefixed launcher and registered as alternatives to the original implementation.

- R: `graal-R`
- python: `graal-python`
- nodejs: `graal-node`, `graal-npm`, `graal-npx`

For example, you can run `graal-R` directly or set `/usr/bin/R` to point `graal-R` with:

```
# show all available installation of R
sudo update-alternatives --list R

# Make graal-R in graalvm-ce-java11 to default R
sudo update-alternatives --set R /usr/lib/jvm/graalvm-ce-java11/bin/graal-R
```

Before you use the Truffle Language Implementations, you should install the required packages with `gu`; for detailed descriptions, just run the `graal-` version binary:

```
graal-python
ERROR: python runtime is not installed yet: run 'gu install python'
```

## GraalVM tools

`graal-native-image` is provided but to use it properly, it also requires manual installation, like:

```
gu install native-image
```

## LLVM tools

These tools are also accessible with a `graal-` prefixed launcher and registered as alternatives to the original implementation.

- clang: `graal-clang`
- clang++: `graal-clang++`

To use it properly, it also requires manual installation, like:

```
gu install llvm-toolchain
```

