This script will read a taskpaper file and add ticket numbers to each line.

That's useful if your primary ticketing system is actually a taskpaper file. I met a couple of developers at wwdc that, just like me, had a simple taskpaper file in every of ther iOS / Mac projects where they tracked the todo's. That makes most sense if you're a lone developer working on your own apps. This doesn't scale at all if you work in a team.

However, if you are one of these lone souls (kinda like me), then this script might be helpful to you.

My biggest gripe with the taskpaper format is, that I don't have ticket numbers for the individual entries that I have in there.
Take for example the following entry:

New Version 3:
    - Create stunning login animation
    - Fix the memory problem in the slideshow
    - Add logout button in main interface.

Now, when you fix the memory problem, you happily add the @done, and within taskpaper, the problem is solved.
However, when you finally commit, you need to enter this change again. Wouldn't it be great if something could automatically connect that fix with your commit?

That's what parsepaper is for. It does two things:
    1. when you run it, it will add # folowed by a number to every line that starts with a "-" and doesn't have a @done.
    2. When you fixed stuff (@done) you can run parsepaper with the ticket numbers that you just finished, and it will do a git commit for you, setting the ticket number and the ticket contents into the commit log (+ anything else you give parsepaper via the -m flag.
    3. When you are sure that your taskpaper file is absolutely flawless, and you just @done'ed some flags, then you can just let parsepaper do the commit for you based on all the changes in the taskpaper file that it can gather from git diff.

Caveats:
parsepaper will alwys do a commit -a. There's no easy way to find out which
files should be commited. If you need that behaviour pipe the parsepaper status
output to git commit.
