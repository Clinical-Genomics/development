# Crontab

[Cron][cron] is a unix tool to run programs at certain times. Automatically! How great is that?
Cron saves this information into a file called `crontab`. Sometimes, cron and crontab are used interchangeably.

This document outlines how to write the perfect crontab entry.

## TL;DR

```
0 0 * * * $CRONIC your-awesome-program >> your-awesome.log 2> >(tee -a your-awesome.log >&2)
```

We use `$CRONIC` to make sure only errors are emailed.

That's it! How does it work? Read on!

## Edit the crontab

```
crontab -e
```

This will drop you into a `vim` session.

## Crontab format


```
 ┌───────────── minute (0 - 59)
 │ ┌───────────── hour (0 - 23)
 │ │ ┌───────────── day of month (1 - 31)
 │ │ │ ┌───────────── month (1 - 12)
 │ │ │ │ ┌───────────── day of week (0 - 6) (Sunday to Saturday;
 │ │ │ │ │                                       7 is also Sunday on some systems)
 │ │ │ │ │
 │ │ │ │ │
 * * * * *  command to execute
```
See [Cron][cron] for more explanation on crontab's format.

## command to execute

Quite often the command is a bash script that you want to execute, bash scripts goes under 
servers/resources/yourserver/crontabs and needs to be executable. 
Do a `chmod ugo+x yourscript.sh ` and commit it to github to make it executable. 

## Errors!

You really want to be notified when your automation goes wrong. This line will add an email address to the crontab[^1].

```MAILTO=clinical-logwatch@scilifelab.se```

This will mail any output made by a crontab started program to the above mentioned email address.

## Only errors!

You don't want to be spammed with _all_ output of your programs. You only want to be notified when something goes wrong.

What does it mean "to go wrong"?

On the highest level, this mean when a program exits with a non-zero exit code. To make sure we only get emailed with the full output of our program when the program exits with a non-zero exit code, we make use of [cronic][cronic].
Cronic will capture all output of your program, including everything printed to stderr. If all goes well, all that captured output will be printed to stdout, including everything that was caught from stderr. Only when the program exits with a non-zero exit status will everything be printed to stderr.

## Cronic 

How can we make use of this nifty feature?

Like this:

```cronic your-awesome-program >> your-awesome.log```

All output to stdout will be caught by your log (all went well!). All output to stderr will be caught by crontab which will send it by email if `MAILTO` is set (program exited with non-zero exit code).

## Logging

What if you also want to log all output, even when something goes wrong?

Then comes in some bash magic [^1]

```
SHELL=/bin/bash
cronic your-awesome-program >> your-awesome.log 2> >(tee -a your-awesome.log >&2)
```

Here we add a stderr redirect (`2>`) to the program [tee][tee]. Tee captures all stdin (through `>(tee ...)` [process substitution][process substitution]), appends it to your-awesome.log, and prints stdin back to stdout. Stdout gets redirected to stderr (`>&2`). And remember: stderr is sent to crontab, which will mail the content to `MAILTO` if set.

## $CRONIC

Lastly, you do not want to write the full path to `cronic` for each crontab entry. Create a bash variable at the start of the crontab, which you then can use in your crontab entry: [^1]

```
CRONIC=~/server/resources/cronic
0 0 * * * $CRONIC your-awesome-program >> your-awesome.log 2> >(tee -a your-awesome.log >&2)
```

[^1]: Please be aware that in most certainty, the shell variables `SHELL`, `MAILTO`, and `CRONIC` will already by set at the top of the server's crontab.

[cron]: https://en.wikipedia.org/wiki/Cron
[cronic]: https://github.com/Clinical-Genomics/servers/blob/master/resources/cronic
[tee]: https://en.wikipedia.org/wiki/Tee_(command)
[process substitution]: http://tldp.org/LDP/abs/html/process-sub.html
