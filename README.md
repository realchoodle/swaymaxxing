# README.md

`swaymaxxing` is a Bash script that lets you use variables set in your Sway
configs in other files. This script is a ***work in progress***; if you decide
to use it, do so with caution. While `swaymaxxing` attempts to preserve your
configuration files, it is still not as safe and featureful as it needs to be.

## Usage

Provide paths to `.smxt` template files as arguments for `swaymaxxing`. For
example:

```bash
swaymaxxing path/to/file0.smxt path/to/file1.smxt path/to/file2.smxt
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

font=%%font_mono%%
background-color=%%bg0%%
border-color=%%bg4%%
text-color=%%fg1%%
```

***Crucially***, this assumes that `font_mono`, `bg0`, `bg4`, and `fg1` are real
variables somewhere in one of your Sway configuration files. If you wanted to
quote these variables in this configuration file, but not in your Sway files,
then you would have to put quotes outside of the `%%variable%%`, resulting in
`"%%variable%%"` or `'%%variable%%'`.
