# DeBugFix

DeBugFix (**Deb**ian **bug** **fix**) is a tool to patch a given Debian package.

If you encounter a bug in some program and want to fix it yourself before the Debian maintainers will upload the next release, you can use this tool instead of trying to rebuild the package manually.

## Pre-requisities

- Install `sudo`, `dpkg-dev` and `python3-appdirs`
- Enable source repositories in your `/etc/apt/sources.list`. To do this, you can copy the lines starting with `deb` and replace `deb` to `deb-src` in the beginning of these copied lines
- Create a config (at `~/.config/debugfix.json`) using the template in the repository

## Usage

If you want to patch `kate` with the patch names `patches/some.patch`, use the following:

```
$ # Build the patches packages
$ ./debugfix build -p kate -P patches/some.patch -d 'Insert patch description here'
$ # Update the installed packages to the patched version
$ ./debugfix install -p kate
```

## Safety notes

The script will install build dependencies in the beginning and remove it in the end. The code for this is not super reliable, so you should take extra care and look out for which packages are really installed or removed.

Also, for the same reason, you should run the script only on the fully updated system.

It would be a better idea to create a sandbox and build inside it, but I am lazy to write such code. Any contributions are welcome, though.
