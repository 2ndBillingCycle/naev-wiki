This article describes steps you can take if you run into a problem with Naev.

## Bug reporting channels
If you want to report a bug, you can do so in the following ways:

* Tracker: Open an issue on the issue tracker. Make sure to include all the relevant information, such as when and where the problem occurs and the backtrace if applicable.
* Discord: Join the discord channel and report the problem there. You can join with the [discord invite](https://discord.gg/nd2M5BR).
* IRC: Join our IRC channel and report the problem there. The IRC channel is #naev on irc.freenode.net.
* ~~Forum: Post about your problem in the technical support forum.~~

In all cases, try to see if your bug has already been reported by looking at the forum and issue tracker!

## Content Errors

Content fixes are always appreciated, whether you've found a typo, grammar error, nonsensical description, or a clearly-wrong value.

If you've found a bit of content that needs fixing, report the specific error and where it occurs.

## Scripting Errors

If a mission or pilot is behaving strangely, you can check for Lua errors in the console (F2 by default). If there are errors (highlighted in red), you can find a copy of them in your log directory.

However, plenty of behavioural errors (like missions getting stuck) don't produce Lua errors, so in that case, just report the issue along with steps to reproduce it, if applicable.

Crashes
On Linux, backtraces are automatically generated and written to stderr. If you're not running Naev from a terminal, the backtrace will be located in your log directory.

On other platforms, debugging crashes is more difficult. Advanced users may want to see Debugging for information on getting backtraces on Windows and OS X.

Regardless of whether you're able to get a backtrace, we want to know about all crash issues. Steps to reproduce the crash are useful in all circumstances.

## Log location

If you're running 0.6.0-beta2 or newer, Naev automatically stores logs when errors occur. Platform-specific paths are as follows:

| OS | Path |
| --- | --- |
| Windows | %APPDATA%\naev\logs\ |
| Mac OS X | ~/Library/Application Data/naev/logs/ |
| Linux | ~/.local/share/naev/logs/ |

Or, if you're running in portable mode, the logs directory will be in the same directory as everything else.

Please attach recent logs (both stdout and stderr) when reporting crashes and Lua errors.