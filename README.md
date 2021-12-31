This is my Ergodox config.

I've separated it out so that I don't have to negotiate the huge fs hierarchy
in `qmk_firmware`.

# Setup

Warning: haven't tried these steps yet!

This is more for me than for others.

This is also assuming you have Nix installed.  Again, more for my weird setup.
Sorry!

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

Here's the Nix part, for fetching the `qmk` utility and its dependencies:

```bash
echo 'use nix' > .envrc
direnv allow
# go get something to drink or doomscroll or something
```

From here you should be able to `qmk build` or `qmk flash` and it
do the right thing.
