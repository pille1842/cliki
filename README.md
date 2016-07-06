# cliki -- a command-line interface wiki based on Git and Markdown

Cliki is a simple interface to use a local Git repository as your personal
wiki. It allows you to view individual Markdown-formatted pages, edit those
pages and automatically commit your changes into the repository, delete
pages, show a log and blame a file line-wise.

Cliki relies on well-established tools like git, pandoc and less, although
it is highly customizable: You may use your own toolchain that suits your
needs. Since cliki is free software, you may also change the original program
to your liking.

# Installation

Clone this repository somewhere on your computer. You may then move the cliki
script file to a location inside your $PATH variable:

```
# mv cliki /usr/local/bin
```

## Requirements

* You must have Git installed.
* By default, cliki uses pandoc as its typesetter, so you should have pandoc
  installed. You may also change the typesetter to your liking (see section
  "Configuration").
* You'll need a viewer program. The default is less, which is installed on
  most systems.
* You'll need an editor. Either set the $EDITOR environment variable to an
  editor your like, or change cliki's configuration (see "Configuration").

# Configuration

If you run cliki, it will test if a default configuration file exists at
$HOME/.config/cliki.conf. If not, it will create this file and fill it with
some documentation of the values you can set. You may either change that file
or create a new configuration file and have cliki load it by using the -c
command-line option.

Cliki will read its configuration in the following order:

1. The default configuration file ($HOME/.config/cliki.conf)
2. The command line (see "Usage")
3. The configuration file given by the -c command-line option.

# Usage

**Synopsis**: cliki [OPTION] OPERATION [PAGE]

## Options

<table>
    <tr>
        <td>-c FILE</td>
        <td>
            read configuration values from FILE. These values override
            values in the default configuration file (~/.config/cliki.conf)
            as well as those given on the command line!
        </td>
    </tr>
    <tr>
        <td>-l DIR</td>
        <td>use DIR as the wiki's location (default: current directory)</td>
    </tr>
    <tr>
        <td>-s PROGRAM</td>
        <td>use PROGRAM as the page viewer (default: less)</td>
    </tr>
    <tr>
        <td>-t PROGRAM</td>
        <td>use PROGRAM as the page typesetter (default: pandoc)</td>
    </tr>
    <tr>
        <td>-e PROGRAM</td>
        <td>use PROGRAM as the page editor (default: \$EDITOR)</td>
    </tr>
    <tr>
        <td>-n</td>
        <td>when editing a page, don't commit the changes into Git</td>
    </tr>
    <tr>
        <td>-h</td>
        <td>display this help and exit</td>
    </tr>
    <tr>
        <td>-v</td>
        <td>output version information and exit</td>
    </tr>
</table>

## Operations

A PAGE's filename is built by cliki by prepending the wiki's location that
was given in the configuration file or via the -l option, then appending the
.md suffix that specifies Markdown syntax.

<table>
    <tr>
        <td>s, show PAGE</td>
        <td>typeset PAGE and view it</td>
    </tr>
    <tr>
        <td>e, edit PAGE</td>
        <td>
            edit PAGE with the specified editor, then commit the changes
            into the Git repository (unless option -n was specified)
        </td>
    </tr>
    <tr>
        <td>d, delete PAGE</td>
        <td>delete PAGE from the repository</td>
    </tr>
    <tr>
        <td>l, log [PAGE]</td>
        <td>
            show either the complete commit log or, when PAGE is given,
            the commits containing that particular page
        </td>
    </tr>
    <tr>
        <td>b, blame PAGE</td>
        <td>do a 'git blame' for a page file</td>
    </tr>
</table>

# Examples

Create a new wiki and a page called "Frontpage" in it:

```
git init
cliki edit Frontpage
```

You may then view the contents of the Frontpage:

```
cliki s Frontpage
```

Change the Frontpage file, but don't automatically commit the changes:

```
cliki -n e Frontpage
```
