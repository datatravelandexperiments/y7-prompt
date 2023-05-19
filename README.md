# y7 prompt

An opinionated prompt for
[y7](https://codeberg.org/datatravelandexperiments/y7).

The basic prompt format is:

**: 12:34;** █

The colon-semicolon form allows entire lines including the prompt to be
copied and pasted into a shell.

## Features

### Failure colour

If the terminal supports 256 colours, the prompt colour can change
when the previous command fails.

The specific colours can be set by:

`y7promptcolor` [_normal_ [_failure_]]

where _normal_ and _failure_ are 256-colour numbers.
The defaults are 232 (almost black) and 1 (red).
Users with different taste can put a `y7promptcolor` command
in `$XDG_CONFIG_HOME/y7/prompt`.

### Prompt notes

Prompt notes are text before the final ‘;’. They are primarily intended to
label subshells that are not in the default state, e.g. are set up with a
specific project environment, or connected to a remote host.

Add a prompt note using

`y7promptnote` [_text_ …]

### Window title

If the terminal supports setting the window title,
it will be set to _hostname_`: `_directory_.
The icon name will also be set, but uses only the tail of the directory.

## Configuration

`prompt` sources a configuration file, if present.
Some will want to set `y7promptcolor` here.
Mine looks like:

```
if [[ -n "$DTACH_SOCKET" ]]
then
    y7promptnote ${DTACH_SOCKET##*/}
elif [[ -n "$SSH_TTY" ]]
then
    y7promptnote ${Y7HOST%%.*}
fi
```
