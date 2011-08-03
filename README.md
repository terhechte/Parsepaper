## ParsePaper

ParsePaper will help you to commit project changes to git if you keep all your
tasks in a simple todo list textfile (typically a taskpaper file)

## Example

Taskpaper is a file format for easy task description. It is available as a Mac
App, iPad App, Vim Plugin, or Emacs Plugin [1].

A typical taskpaper project looks like this:

    Fantastic New App:
    - Have Idea @done
    - Write app @testing
    - Fix user interface
    - Fix unicode bug
    - Profit!

@Something provides you with context on the task, @done marks a task as done.
That's it.

This is a great and easy way to collect todo's, and it is useful if your project or team it too small to use a full fledged bug tracking system like fogbuz or bugzilla or trac. I met a couple of developers at WWDC that, just like me, had a simple taskpaper file in every of ther iOS / Mac projects where they tracked the todo's. That makes most sense if you're a lone developer working on your own apps. This doesn't scale at all if you work in a team, of course.

## Usecase

However, imagine you fix the unicode bug above.  You happily add the @done, and within taskpaper, the problem is solved.  *However, when you finally commit this change to Git, you need to enter the details again.*

* Wouldn't it be great if something could automatically link your commit to your taskpaper file? 
* Even better, if you somehow magically would get ticket numbers for every task in your taskpaper file?

## Features

Parsepaper will help you sync your taskpaper todo file with your version
management. It:

* reads your taskpaper file and adds ticket numbers (#4481) to every line that
  hasn't got a @done yet.
* checks the diff from your taskpaper file in Git and lists all the tasks that
  you finished since your last commit
* Commits all your files and lists your changed tickets in the commit message
* has a "auto" mode that almost automatically takes care of everything you want
  and just asks you if it should commit.

### Even more features

* Ability to only commit some of the tickets that have a done (via
  --tickets=... flag)
* Ability to add additional message to be prepended to the commit (via the -m
  flag)
* And more. See commandline for details.

## Basic Usage

Just run: 

**'parsepaper' or 'parsepaper auto'**

What happens is this:

1. Add ticket numbers to all items that don't have a number  yet.
2. Determine which tickets have actually been closed
3. Commit everything with these tickets as the commit log.

However, it will show yout the proposed commit log and ask if you really want
to commit. If you don't want that, add a '-f' (force)

**You can always call --help (parsepaper --help) if you have problems.**

Parsepaper expects your todo file to be named **todo.taskpaper**. If that's not the
case either add the commandline flag '-t (location of file)' or, if that's too
cumbersome, simply change it in the script.

## Advanced usage

You can also run the individual steps as seperate tasks:

* 'parsepaper decorate' will read your todo file and add tickets
* 'parsepaper status' will show you what would be commited
* 'parsepaper commit' will commit the changes.

If you want to commit only certain tickets, do a 'parsepaper commit --tickets=#1111,#2284'

## Caveats

* parsepaper will alwys do a commit -a. There's no easy way to find out which files should be commited. If you need that behaviour pipe the parsepaper status output to git commit.
* Limited to Git. It's actually easy to implement a different system by just
  subclassing the Parsepaper class, but I just use Git.
* Ticket numbers are always in the range from 1 to 9999. That's trivial to
  change but it is hardcoded into the script right now because I deemed it
  sufficient.
* It only works with taskpaper files an the @done / - / project: terminology.
 
## Installation

This script is just one single Ruby script that takes care of everything. The
easiest installation would be to download / clone the repository, copy the
script to /usr/local/bin or /usr/bin and give it executable flags:

    git clone ...
    cd parsepaper
    cp ./parsepaper /usr/local/bin/
    chmod +x /usr/loal/bin/parsepaper

## Details

This script is written in Ruby, and it's actually my first Ruby script. I'm a
longtime Python guy so everything is new and unknown. So forgive any weird
errors that are not the Ruby  way of things and, if you feeel like it, clone
the repository and change it :)


[1]

* Emacs: <http://coderepos.org/share/browser/lang/elisp/taskpaper/trunk/taskpaper.el>
* Vim: <http://www.vim.org/scripts/script.php?script_id=2027>
* Mac / iPhone /iPad: <http://www.hogbaysoftware.com/products/taskpaper>
