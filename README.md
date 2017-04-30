# autols
Causes cd to automatically trigger ls under certain conditions. This script provides a strict superset of the functionality of cd.

# Installation
To get this working right away, just put the script in your root directory and put `. $HOME/autols` at *the end of your .bash_profile*. It can also be put in your .bash_rc (or wherever you want), but there is a common "gotcha" that I'll write about at the bottom of this README.

# Usage
When this script is in use, by default, cd-ing into a directory will automatically ls it's contents unless it has more than 150 non-hidden files/directories. If there are more than 150, it will simply cd you into the directory and give a short message about how many visible files the directory contains.

cd also gets a new "-b" flag that switches to it's [b]uiltin functionality for that single use of cd.

In addition to that, this script provides "set_max_auto_ls" function in the shell that accepts an integer as an argument, setting the maximum number of files a directory can contain and still trigger an automatic ls.

Lastly, it gives you a "toggle_auto_ls" function in the shell that reverts cd functionality between it's builtin version, and the autols version. This function doesn't require any arguments, and will tell you which version of cd you are currently set to.

# Gotchas
So the reason for putting `. $HOME/autols` at the bottom of your .bash_profile is to ensure that it's the last thing that's sourced by the scripts that automatically run when you create a new shell. The reason for this is a really odd problem I ran into.

If you've installed rvm, there's a good chance you have a line in your .bash_profile or .bash_rc or some file that's sourced by one of those those that contains something functionally similar to `source "$HOME/.rvm/scripts/rvm"`. Here's a really weird thing about that line: it overloads your default cd functionality, clobbering the functionality of this script if it's sourced *after* running/sourcing the autols script.

The reason it overloads cd is so that every time you cd into a new directory, rvm can check for a file called ".rvmrc" in the new directory, and if it exists, it will run it (and echo a note that changes are being made).

Maybe this is useful to you if you're a rails developer or something, but I believe to most people it's totally useless. If you're curious you can check if you have any .rvmrc files other than one you may have made in your root directory by running `find . -type f -name '.rvmrc'` in your root directory.

If you don't care about this functionality, add this line to your root directory's .rvmrc file (or create one if it's not already there): `rvm_project_rvmrc=0`. Once that's done, you're free to put `. $HOME/autols` wherever you like in .bash_profile or .bashrc or wherever.
