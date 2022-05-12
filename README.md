This is my Ergodox config.

I've separated it out so that I don't have to negotiate the huge fs hierarchy
in `qmk_firmware`.

# Setup

Warning: haven't tried these steps yet!

This is more for me than for others.

Clone this repo somewhere:

```bash
cd $YOUR_DEV
git clone https://github.com/jws85/ergodox
```

Copy `config/qmk.ini` in place:

```bash
mkdir $HOME/.config/qmk
cp $YOUR_DEV/ergodox/config/qmk.ini $HOME/.config/qmk
```

Clone QMK, and optionally check out the exact commit I started this from:

```bash
cd $YOUR_DEV
git clone https://github.com/qmk/qmk_firmware
cd qmk_firmware
# git checkout 0b2bc8955949e21e40f5dbc888d785dcd370ca07
```

Symlink the `ergodox` directory into the `qmk_firmware` hierarchy:

```bash
ln -s $YOUR_DEV/ergodox keyboards/ergodox_ez/keymaps/jws85
```

## Nix setup

This is not strictly necessary, if you have vanilla Linux you can do that as
well, at least until that git commit's dependencies are deprecated... then
Nix might be your only option.

QMK has a `shell.nix` file for use with the [Nix package manager](https://nixos.org/).
This pulls in cross-compilation toolchains, programmers, and such, and at the
end of it, you can run the `qmk` utility to build your stuff as per normal, and
you know you have the versions of everything for this specific version of QMK.

Install the Nix package manager (you don't need NixOS) and [direnv](https://github.com/direnv/direnv).
With those, what I like to do is go in the `qmk_firmware` folder and run:

```bash
echo 'use nix' > .envrc
direnv allow

# The moment you run 'direnv allow' it'll build all QMK dependencies and
# the QMK utility!
#
# Depending on your hardware, this could take anywhere from "get a quick
# drink" to "go get a nice dinner out"...
```

From here you should be able to `qmk build` or `qmk flash` and it do the right
thing, but only within the `qmk_firmware` directory.
