# Base16 GNU ls dircolors

A python script to generate `$LS_COLORS` shell environment variable.

The program ls uses the environment variable LS_COLORS to determine the colors
in which the filenames and filetypes (like directories and symlinks) are displayed.
This environment variable is usually set by a command like:

``` bash
eval 'dircolors some_path/dir_colors'
```

The GNU version of ls allows more suffisticated color definitions.

## Installation

For the base16 workflow see:
[base16](https://github.com/chriskempson/base16)

## Usage

Either method A or B.

### A: Stored

Store the output of the generated python script:

``` bash
./path/to/gen_dircolors.py > ~/.dircolors.256dark
```

And use it:

``` bash
eval 'dircolors ~/.dircolors.256dark'
```

For persistence across shell sessions you want to
write this line in your shell rc file (.bash_profile, .zshrc...).

### B: Computed

Use the script output directly:

``` bash
eval 'dircolors <(python /path/to/gen_dircolors.py)'
```

(You could also skip the base16 workflow and define
colors in `default.mustache` and use it as python script.)

# dircolors documentation

Below are the color init strings for the basic file types. A color init
string consists of one or more of the following numeric codes:

## Attribute codes:

Code | Style
---- | -----
00 | none
01 | bold
04 | underscore
05 | blink
07 | reverse
08 | concealed

## Text color codes:

Code | Style
---- | -----
30 | black
31 | red
32 | green
33 | yellow
34 | blue
35 | magenta
36 | cyan
37 | white

## Background color codes:

Code | Style
---- | -----
40 | black
41 | red
42 | green
43 | yellow
44 | blue
45 | magenta
46 | cyan
47 | white

256 color support see:
[256 color support](http://www.mail-archive.com/bug-coreutils@gnu.org/msg11030.html)

## Ansi escape codes

Text 256 color coding:
`38;5;COLOR_NUMBER`

Background 256 color coding:
`48;5;COLOR_NUMBER`

Further reading
[linux die](https://linux.die.net/man/5/dir_colors)
[ANSI escape code colors](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors)

## Conventions

File | Style
---- | -----
Dev relevant files | bold
Directories | bold and reversed
Executable files | system red and bold
Special files (links, pipes...) | white on an colorful background

# Troubleshooting

The dircolors.256dark template has to live relative to
the generated script gen_dircolors.py.

``` bash
├── README.md
├── colortrans.py
├── scripts
│   └── gen_dircolors.py
└── templates
    ├── config.yaml
    ├── default.mustache
    └── dircolors.256dark
```

If this is not the case in your workflow, you have
to manually set it in `default.mustache`:

``` python
template = os.path.join(os.path.dirname(__file__),
                        '../templates/dircolors.256dark')
```
