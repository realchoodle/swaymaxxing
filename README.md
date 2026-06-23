# README.md

`swaymaxxing` is a Bash script that lets you use variables set in your Sway
configuration files in other files. This script is a ***work in progress***; if
you decide to use it, do so with caution. While `swaymaxxing` attempts to
preserve your configuration files, it is still not as safe and featureful as it
needs to be.

## Usage

Provide paths to your configuration files as arguments for `swaymaxxing`. For
example:

```bash
swaymaxxing config.d/file0 config.d/file1 config.d/file2
```
