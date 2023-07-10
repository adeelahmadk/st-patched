# A Resilient & Suckless Simple Terminal

This repo a custom configuration of Suckless Terminal with the patches applied according to the workflow of my convinence.

## Patches

| Patch | Description |
|-------|-------------|
| scrollback | for backwards scroll support|
| colorschemes | switch among 8 color schemes |
| boxdraw | adds options to render most of the lines/blocks characters and/or the the braille ones without using the font |
| ligatures | adds options to render most of the lines/blocks characters and/or the the braille ones without using the font |
| anysize | allows st to resize to any pixel size, makes the inner border size dynamic, and centers the content of the terminal. st will always fill the entire space allocated on a tiling WM. |
| delkey | Return BS on pressing backspace and DEL on pressing the delete key. |

## Dependencies

1. Development files for FreeType-based font drawing library for X (XFT).
2. Development files for `Harfbuzz` library for ligatures support, an OpenType text shaping engine.

```sh
# for Debian/Ubuntu based distros
sudo apt install build-essential libxft-dev libharfbuzz-dev
```

## Patching

Suckless’ programs are meant to be as minimal as possible after all. That’s not to say you’re left completely in the dust if you want something like scrollback support though. [st’s patches](https://st.suckless.org/patches/) provide you with an easy way of adding some extra functionality.

Most of the newbies, unfimilier with the open-source software development process (i.e. patches), are troubled by the lack of guidance and documentation. However, a careful look at the [suckless' website](https://suckless.org/) reveals the [hacking guide](https://suckless.org/hacking/).

This guide lists three methods of patching a program:

For git users, use -3 to fix the conflict easily:
```sh
cd program-directory
git apply path/to/patch.diff
```

For patches formatted with git format-patch:

```sh
cd program-directory
git am path/to/patch.diff
```

For tarballs:

```sh
cd program-directory
patch -p1 < path/to/patch.diff
```

In addition to these, there's another good method is by using `patch` command with `--merge` option which merges a patch file into the original files.

```sh
cd program-directory
patch --merge -i path/to/patch.diff
```

The last mathod is the most favored one accross the _hacker community_.

## Special notes on the applied patches and tweaks

### Tweaks

#### Font

The default font is set to FiraCode Nerd Font (config.def.h/config.h, line# 8):
```c
static char *font = "FiraCode Nerd Font:pixelsize=11:antialias=true:autohint=true";
```

#### Color Scheme

The colorschemes patch must be applied prior to this tweak. The default color scheme is set to One Half dark (config.def.h/config.h, line# 167):
```c
int colorscheme = 2;  // One Half dark
```

### boxdraw

This patch adds options to render most of the lines/blocks characters and/or the the braille ones without using the font.

Unlike others, this patch has been generated using `git --format-patch`. Most suitable command for patching is:
```sh
patch -p1 < st-boxdraw_v2-0.8.5.diff
```

### colorschemes

Predefined color schemes:

- the default (dark) st color scheme
- the default (dark) alacritty color scheme
- One Half (dark & light)
- Solarized (dark & light)
- Gruvbox (dark & light)

Key bindings:

- Select the first..eighth color scheme with Alt+1..8.
- Select the next color scheme with Alt+0.
- Select the previous one with Ctrl+Alt+0.

| Binding | Color Scheme |
|---------|--------------|
| `Alt+1` | st dark |
| `Alt+2` | Alacritty dark |
| `Alt+3` | One Half dark |
| `Alt+4` | One Half light |
| `Alt+5` | Solarized dark |
| `Alt+6` | Solarized light |
| `Alt+7` | Gruvbox dark |
| `Alt+8` | Gruvbox light |

