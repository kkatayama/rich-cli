# Rich CLI

Rich-cli is a command line toolbox for fancy output in the terminal, built with [Rich](https://github.com/Textualize/rich).

Rich-cli can syntax highlight a large number of file types in the terminal, with specialized rendering for Markdown and JSON files. It also provides an interface to console text rendering with many options to format and style your output.

## Installation

Rich-cli is distributed as a Python application, which you can install via Pip:

```
python -m pip install rich-cli
```

Alternatively, you can use `pipx` to install it globally:

```
pipx install rich-cli
```

Once installed, you should have the `rich` command on your path.

```
rich -h
```

## Syntax highlighting

To syntax highlight a file enter `rich` followed by the path to your file.

```
rich loop.py
```

TODO: screenshot

Add the `--line-number` or `-n` switch to enable line numbers. Add `--guides` or `-g` to enable indentation guides.

```
rich loop.py -n -g
```

TODO: screenshot

You can specify a [theme](https://pygments.org/styles/) with `--theme` or `-t`.

```
rich loop.py --theme dracula
```

By default, `rich` will wrap lines if they don't fit within the available width. You can disable this behaviour with `--no-wrap`.

TODO: screenshot

`Rich` will try to deduce the format of the via from the filename, if the chosen _lexer_ is wrong or you want to override the auto-detected lexer you can explicitly set it with the `--lexer` or `-x` switch.

## Markdown

You can request markdown rendering by adding the `--markdown` switch or `-m`.

```
rich README.md -m
```

TODO: screenshot

If your terminal supports hyperlinks, you can add `--hyperlinks` or `-y` which will output hyperlinks rather than full URLs.

```
rich README.md --hyperlinks
```

## JSON

You can request JSON pretty formatting and highlighting with the `--json` or `-j` switches.

```
rich cats.json --json
```

### Rules

You can render a horizontal rule with `--rule` or `-u`. Specify a rule style with `--rule-style`. Set the character(s) to render the line with `--rule-char`.

```
rich "Hello [b]World[b]!" --rule
rich "Hello [b]World[b]!" --rule --rule-style "red"
rich "Hello [b]World[b]!" --rule --rule-style "red" --rule-char "="
```

TODO: screenshot

## Exporting

In addition to rendering to the console, `rich` can write an HTML file. This works with any command. Add `--export-html` or `-o` followed by the output path.

```
rich README.md -o readme.html
```

Nothing will be shown in the terminal, but you should find a "readme.html" in your current working directory.

## Rich Printing

If you add the `--print` or `--p` option then Rich will treat the first argument as [console markup](https://rich.readthedocs.io/en/latest/markup.html) which allows you to insert styles with a markup similar in design to bbcode.

```
rich "Hello, [bold magenta]World[/]!"
```

TODO: screenshot

### Soft wrapping

Rich will word wrap your text by default by inserting newlines where appropriate. If you don't want this behavior you can enable _soft_ wrapping with `--soft`.

## Reading from Stdin

Where `rich` accepts a path, you can enter `-` which reads the content from stdin. You may want this if you are piping output from another process.

Note that when rich isn't writing directly to the terminal it will disable ansi color codes, so you may want to add `--force-terminal` or `-F` to tell `rich` you want to keep ansi codes in the output.

```
cat README.md | rich - --markdown --force-terminal
```

TODO: screenshot

## General Options

There are a number of additional switches you may add to modify the content rendered to the terminal. These options are universal and apply to all of the above features.

### Style

You can set a style to apply to the output with `--style` or `-s`. The styles are specified with [this syntax](https://rich.readthedocs.io/en/latest/style.html).

```
rich "Hello, [b]World[/b]!" --print --style "on blue"
```

TODO: screenshot

### Alignment

You can align output to the left, center, or right with the `--left`, `--center`, or `--right` options, or their single letter counterparts: `-l`, `-c`, or `-r`.

```
rich "Hello [b]World[/b]!" --print --center
```

### Width

You can set the width of the output with `--width` or `-w` and the desired width. Note that the default behavior is to wrap text.

```
rich "I must not fear. Fear is the mind-killer. Fear is the little-death that brings total obliteration." -p -w 40
```

TODO: screenshot

### Text Justify

You can set how `rich` will justify text with `--text-left`, `--text-right`, `--text-center`, and `--text-full`; or the single letter equivalents: `-L`, `-R`, `-C`, and `-F`.

The difference between `--left` and `--text-left` may not be obvious unless you specify the width of the output. The `--left`, `--center`, and `--right` options will center the block of text within the terminal dimensions. Whereas, the `--text-left`, `--text-center`, and `--text-right` options define how text is rendered _within_ that block.

In the following examples, we specify a width of 40 (`-w 40`) which is center aligned with the `-c` switch. Note how the `-R`, `-C` and `-F` apply the text justification within the 40 character block:

```
rich "I must not fear. Fear is the mind-killer. Fear is the little-death that brings total obliteration." -p -w 40 -c -L
rich "I must not fear. Fear is the mind-killer. Fear is the little-death that brings total obliteration." -p -w 40 -c -R
rich "I must not fear. Fear is the mind-killer. Fear is the little-death that brings total obliteration." -p -w 40 -c -C
rich "I must not fear. Fear is the mind-killer. Fear is the little-death that brings total obliteration." -p -w 40 -c -F
```

### Padding

You can apply _padding_ around the output with `--padding` or `-d`.

```
rich "Hello [b]World[/b]!" -p -c --padding 3 --style "on blue"
```

### Panel

You can draw a _panel_ around content with `--panel` or `-a`, which takes one of a number of [styles](https://rich.readthedocs.io/en/latest/appendix/box.html).

```
rich "Hello, [b]World[/b]!" -p -a heavy
```