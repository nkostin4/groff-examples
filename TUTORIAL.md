# N. Kostin's (normie-friendly) Guide to GNU troff (groff)

Let's make groff more accessible to normies! I was inspired by [Luke Smith](https://lukesmith.xyz) to start using the groff typesetting system.

_Troff_ is the original UNIX typesetting software developed in the 1970s. It takes plain text files, mixed with embedded formatting commands, and produces formatted output (much like LaTeX). [Groff, the GNU clone of troff,](https://gnu.org/software/groff/) remains an important part of UNIX-like systems to this day.

**Note**: Even if you already use [LaTeX](https://github.com/nkostin4/LaTeX-templates), I highly recommend learning groff; it comes with all of the extensibilty of LaTeX, but is far more lightweight and minimal.

## Contents

* [Installation](#installation)
* [Quick Start](#quick-start)
	* [Macro Packages](#macro-packages)
	* [My First Document](#my-first-document)
* [Common Macros](#common-macros)
	* [Cover Page](#cover-page)
	* [Paragraphs](#paragraphs)
	* [Headings](#headings)
	* [Highlighting](#highlighting)
	* [Indents](#indents)
	* [Lists](#lists)

## Installation

If you're a GNU/Linux user, you probably already have groff installed on your system! How cool is that?

- On Arch/Artix Linux, groff is included in the `base-devel` package.

If you're a Mac OS user, groff can be installed with Homebrew:

```
brew install groff
```

If you're a Windows user, you can find a pre-built binaries [here](https://sourceforge.net/projects/ezwinports/files/).

## Quick Start

Groff is a typesetting system that takes plain text files, mixed with embedded formatting commands, and produces formatted output.

### Macro Packages

Groff has a bunch of different macro packages. These packages contain dozens of useful macros for headers, footers, titles, lists, tables, and so on. Some common macro packages include

- `man` for writing man pages
- `mom` for writing books
- `ms` for writing technical papers and reports
- `www` for writing web pages

I'll be focusing on the `ms` macro package in this tutorial.

### My First Document

Now it's time to write your first groff document. Create a file called `hello.ms`, then fire up your favorite text editor and copy the following: 

```
.TL
My First Groff Document
.AU
Billy Gates
.AI
Microsoft Corporation
.SH
FitnessGram Pacer Test
.PP
The FitnessGram Pacer test is a multistage aerobic capacity test that
progressively gets more difficult as it continues. The 20 meter Pacer test will
begin in 30 seconds. Line up at the start. The running speed starts slowly, but
gets faster each minute after you hear this signal *boop*. A single lap should
be completed each time you hear this sound *ding*. Remember to run in a
straight line, and run as long as possible. The second time you fail to
complete a lap before the sound, your test is over. The test will begin on the
word start. On your mark, get ready, start.
```

Note that the Pacer test is [owned and copyright by FitnessGram](https://www.fitnessgrampacertest.com/). Feel free to replace "Billy Gates" with your name. Now run the following command in the same directory as `hello.ms`:

```
groff -ms hello.ms
```

The `-ms` option tells groff to include the `ms` macro package that we're using. You probably just saw a bunch of nonsense appear on your screen. What happened was that PostScript got printed to your terminal. PostScript isn't very readable. The industry standard seems to be PDFs nowadays. So let's now run the following:

```
groff -ms hello.ms -T pdf > hello.pdf
```

The `-T pdf` option tells groff to output to a PDF. Big-brained UNIX chads know that the right chevron means "redirect the STDOUT of a program to a file." So in this case, we're taking the output and putting it in a file called `hello.pdf`. (Otherwise, more nonsense would be printed to the screen.) 

At this point, we have a nice PDF. So now let's interpret what each of the commands did. Observe that all groff commands begin with a `.` and must come at the beginning of a line.

- `.TL` is the title.
- `.AU` is the author.
- `.AI` is the author's institution.
- `.SH` is a silent heading (as opposed to numbered heading).
- `.PP` means start a new indented paragraph.

## Common Macros

### Cover Page

| Macro | Functionality |
|:-----:|:-------------:|
| .RP | If omitted, groff prints a subset of the cover page on page 1 |
| .P1 | Prints the header on page 1 |
| .DA | Print the current date on the title page and in the footers |
| .ND | Print the current date on the title page but not in the footers | 
| .TL | Specifies the document title |
| .AU | Specifies the author's name |
| .AI | Specifies the author's institution |
| .AB [no] | Begins the abstract |
| .AE | End the abstract |

### Paragraphs

| Macro | Functionality |
|:-----:|:-------------:|
| .PP | Creates indented paragraph |
| .LP | Creates paragraph with no initial indent |
| .QP | Creates quoted paragraph |

### Headings

| Macro | Functionality |
|:-----:|:-------------:|
| .NH xx | Numbered heading, where the argument xx specifies the level of the heading |
| .SH | Silent (unnumbered) heading |

### Highlighting

| Macro | Functionality |
|:-----:|:-------------:|
| .B | Bold type |
| .R | Roman type |
| .I | Italic type |
| .CW | Constant-width face |
| .BI | Bold italic type |
| .BX | Draws a box around text |
| .UL | Underlines text |
| .LG | Larger type (2 points larger than current) |
| .SM | Smaller type (2 points smaller than current) |

### Indents

| Macro | Functionality |
|:-----:|:-------------:|
| .RS | Starts indented text |
| .RE | Ends indented text |

### Lists

| Macro | Functionality |
|:-----:|:-------------:|
| .IP [marker [width]] | List item. The marker is `\(bu` for bulleted lists. The width specifies the indent for the body of each list item. |
