# README.md

`swaymaxxing` is a Bash script that lets you use variables set in your Sway
configs in other files. `swaymaxxing` is written in (mostly) pure Bash. The
exceptions are:

- `tput`, to add color to logs
- `mv`, to create backup files
- `sway`, to validate Sway configuration files and obtain variables from them

I have tried to use the external programs above sparingly.

## Basic Usage

> [!Note]
> See the `--help` flag for more options.

Provide paths to `.smxt` template files as arguments for `swaymaxxing` using
the `-f` (or `--file`) flag. For example:

```bash
./swaymaxxing -f path/to/file0.smxt -f path/to/file1.smxt -f path/to/file2.smxt
```

Alternatively, use `swaymaxxing` with another program or in a script:

```bash
#!/usr/bin/env bash

declare -i lvl
lvl="${1:-1}"

shopt -s globstar

declare -a flags
while IFS= read -r -d '' file
do
    flags+=(--file "$file")
done < <(printf "%s\0" ~/.config/**/*.smxt)

shopt -u globstar

swaymaxxing --log-level "${lvl}" --strip-characters \"\# "${flags[@]}"
```

`.smxt` (`swaymaxxing` template) is a made-up file extension. `.smxt` files use
`%%this_format%%` to mark items as variables, but should be identical to
whatever file you want to operate on aside from that. For instance, if you had
the following configuration file for `mako`:

```ini
# ~/.config/mako/config

font=LiterationMono Nerd Font Propo 11
background-color=#282828
border-color=#665c54
text-color=#ebdbb2
```

You would create the corresponding `.smxt` file in the same directory but use
the following format instead:

```ini
# ~/.config/mako/config.smxt

font=%%font_mono%% %%font_size%%
background-color=%%bg0%%
border-color=%%bg4%%
text-color=%%fg1%%
```

***Crucially***, this assumes that `font_mono`, `font_size`, `bg0`, `bg4`, and
`fg1` are real variables somewhere in one of your Sway configuration files. If
you wanted to quote these variables in this configuration file, but not in your
Sway files, then you would have to put quotes outside of the `%%variable%%`,
resulting in `"%%variable%%"` or `'%%variable%%'`.
