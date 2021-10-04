# Emacs
I recently switched from vim to Emacs! Some observations commense here

## Emacs is not a text editor!
Well. not _just_ a text editor...
From the website:
"At its core is an interpreter for Emacs Lisp, a dialect of the Lisp programming language with extensions to support text editing."

What does this mean?
Emacs is purely a lisp interpreter, same as you might find a python intepreter installed on your system. But it also contains many useful functions to present useful methods of editing text, built in. So yeah, it's a text editor. and also more

## Emacs is bad for RSI... or your wrists... or whatever
I agree! I started off using the default GNU keybindings... `M-x M-f` and all that. It hurt, quickly. But there's this thing called evil-mode, a way of using the vim keybinds (`:w` etc) in emacs. and it's perfect! I can use all my nice muscle memorised keybinds, with all the rest of the awesome emacs features

# Distro
So, Emacs comes in distros, much like, say, linux. Of course, you could choose GNU emacs, and I did for a bit, but I settled on Doom.
## GNU
I did like GNU Emacs when I started. I did a bit of setting up and ended up with a useable config. But it was _effort_. Configuring anything took 20x longer than it should have, just for stuff that honestly _should_ be the default.
Also, it was very slow.
And then I heard about doom. Doom was a distro made for evil users, with better defaults, and nicer everything

## Doom
### Speed
So when I first started doom the first thing I noticed was the snappyness. Even after loading _far_ more packages than GNU, it loaded in pretty much the same, if not faster, speed than GNU. I dont know what black-magic they pulled off do that but well _done_.
### Packages
Doom has it's own package management system, defined in its `init.el` and `packages.el` files. I much prefer the way they do it to the way GNU does it, or even the third-party `use-package` program.

# Configuration
## Org
I'd like to start by talking about org-mode. Org is an absolute _joy_ to use. In itself, it's just another markup language, but when combined with Emacs' tools it becomes great. (As a student), I now use it for all my Schoolwork, made possible by the org-export feature and being able to convert it to ODT with only a `C-c C-e o o`, as well as my emacs config. Using org-babel(-tangle), I can hit a keybinding and all my code blocks go out into their own files. I manage three seperate files for my config, and all three are managed from my single config.org file.
### Literate Programming
Noticed how I said code blocks? In my config, I use literate programming (and not just in my config - I use it for a couple of my programming projects too). This means that I write the code primarially for the human to understand, and then add all the code as a secondary bit. I can write an intro, organise it into headings and subheadings, write a little explanation without lines upon lines of #s or //s. Then I add a bit of code.
I really enjoy working with my code like this as it makes it feel much more like, say, writing a piece of art than writing a program.
## Plagerism
Okay, yeah yeah, most of my config is plagerised. Fair enough.
I found Tecosaurs config - who appears to be a prominent member of the doom community - online.
I also created lots of my config using stuff found from SystemCrafters live streams on vanilla emacs configuration.
So yeah, credit to them

[My Emacs Config](https://edencreeper.ml/posts/config.org)
