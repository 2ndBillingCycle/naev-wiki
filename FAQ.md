# Installing and Troubleshooting

## I just installed the game and tried running it and it exits right away or says "INSERT NDATA"!

You are most likely missing the ndata and only have the binary. Try downloading the ndata related to your version from the downloads page. Place it into the same directory as your Naev binary and start the game again. The following table is accurate for our official builds.

| OS | Location for ndata |
| --- | --- |
| Windows | C:\Progam Files\Naev\ or C:\Program Files (x86)\Naev\ |
| Mac OS X | naev.app/Contents/Resources/ |
| Linux	| ~/.local/share/naev/ will usually work. |

## The game does nothing when I try to run it!
If you are running on Linux, you may be missing some dependencies. You can find the list of dependencies on the Compiling Nix page. On Linux, you can run your distribution's package manager (e.g. Synaptic on Ubuntu, and apt-get from the command line of any Debian-derived distributions).

If problems persist and you're on Linux or Mac OS X, start Naev from a terminal and open a new bug report, including Naev's output.

On Windows, please do the same, but attach the files "stdout.txt" and "stderr.txt", which can be found in the directory where you installed Naev, commonly C:\Program Files\Naev.

## I get an undefined symbol error! (Linux)

The undefined symbol: ov_read_filter error is, unfortunately, fairly common on older installs. This error is caused by an antiquated version of libvorbis.

The majority of older Linux distributions package outdated versions of libvorbis, including Ubuntu 9.10 and earlier, Debian Lenny, Fedora 11, Mandriva 2009.1 and Slackware 13, among others.

Gentoo, Arch Linux, Debian Testing (Squeeze) as well as Ubuntu 10.04 Lucid Lynx and newer are known to package up-to-date versions.

If your version of libvorbis is outdated, you can either manually upgrade your packages or use a statically-linked binary.

If you're attempting to compile Naev and get this error, see the compiling section of the README.

For more specific help installing Naev on your system, please ask your question on IRC, the mailing list, or the forum.

## I can't see my ship / the menu looks broken / I get a weird crash immediately on launch

Your graphics card (or driver) doesn't support VBOs. To remedy the graphical issues, you can disable VBOs and mipmaps in the graphics options menu, or edit conf.lua and add these lines to the bottom:

```
vbo = false
mipmaps = false
```

## Sound doesn't work on Windows.
Some Windows sound drivers don't provide OpenAL. If you have no sound, download and install OpenAL from here.

## When I accelerate or fire certain weapons, Naev crashes. (Windows)
The software implementation of OpenGL on Windows supports multi-texturing incorrectly, and when interpolation starts, Naev will crash.

To remedy this, you can install the official drivers for your graphics hardware, or you can disable interpolation and engine glow in the video tab of the options menu.

# General
## Will there be multiplayer?
Naev's primary objective is to make a solid singleplayer game with an immersive plot and a dynamic, lively universe. While this could be translated into multiplayer, there are a substantial number of issues in the way, particularly mechanics that make time progress non-linearly. While preserving gameplay in a persistent-world multiplayer game mode is highly difficult, a simpler deathmatch would be feasible. However, this is not a concrete goal, and it will very likely not be a focus until after Naev 1.0 - the release where Naev's singleplayer is considered to be more or less complete.

## Will the game ever be done in 3D?
This is planned for the future. All ships are currently renders of 3D models, but with large sprites (to ensure smooth turning animations) and an increasing number of ships, memory use is increasing with every release.

Currently, a proof-of-concept 3D ship branch exists, though the developer responsible for it is absent. Contributors are welcome.

## Why is it written in C? C++ is omfgwtfbbq times better!
I believe that C is superior in the fact that it is much simpler. There are few basic rules, yet with them you can do everything. It's basically portable assembly. If you want to contribute and don't want to touch C, there is a lot done in Lua to add to. An increasing number of things are done in Lua, including all missions and events, the spawning and equipping of ships, and ship AI.

## Where is the source?
The source is hosted on GitHub. You can view the source online, or download nightly builds with the Git Version Control System. On the wiki, we have step by step instructions for getting Naev code from the Git repository.

Alternately you can grab the source tarball from the download section. It's purely code, however: It doesn't include any of the media included in ndata. See the Simple Development Guide for instructions on acquiring the unpacked contents of the ndata.

## Where are saves and screenshots stored?

| OS |Path | Notes |
| --- | --- | --- |
| Windows | %APPDATA%\naev\ | |
| Mac OS X | ~/Library/Application Data/naev/ | Prior to 0.6.0, OS X used the Linux path. |
| Linux | ~/.local/share/naev/ | |

Saves and screenshots can be found in the saves and screenshots directories, respectively.

## Where is conf.lua stored?

| OS | Path | Notes |
| --- | --- | --- |
| Windows | %APPDATA%\naev\conf.lua | |
| Mac OS X | ~/Library/Application Data/naev/conf.lua | Prior to 0.6.0, OS X used the Linux path. |
| Linux | ~/.config/naev/conf.lua | |


# Gameplay
## How do I save?
Every time you land on a planet the game automatically saves. There's no need to actively save.

## How do I change the key bindings?
As of 0.4.0 the keybindings window within the game is able to reassign keys in a rather intuitive manner.

While still useful, the below information is no longer necessary for most players:

Linux and Mac OS X users can edit the file at ~/.config/naev/conf.lua (or %APPDATA%\naev\conf.lua on Windows). At the bottom of the file, you can find the keybindings. Each line will look something like this:

```
--accel          = { type = "keyboard", key = "up", mod = "any" }
```

With each key assigned to the default setting. To change the key binding, change quoted string after 'key=' and uncomment the line. For example, if you wanted to change the accelleration key from the default up arrow to the 'i' key, you would modify the first line of the keyboard binding to look like this:

```
accel          = { type = "keyboard", key = "i", mod = "any" }
```

Make sure there is no '--' at the beginning of the line, as that will cause Naev to ignore the line.

## How do I make Naev run full screen, or windowed?
With recent versions of Naev, it's possible to set this in-game. Enter the Options menu, open the Video tab and toggle the Fullscreen button. Save the setting and restart the game.

While still useful, the below information is no longer necessary for most players:

Full screen mode, like all user configuration, is determined by the file at ~/.config/naev/conf.lua on Linux or Mac OS X or %APPDATA%\naev\conf.lua on Windows. To enable full screen mode, when Naev is configured to run in a window edit the line in the config file that reads

```
fullscreen = 0
```

to read
```
fullscreen = 1
```
To disable full screen mode, do the reverse.

## How do I get a Heavy Weapon / Heavy Combat Vessel License?
These licenses are granted through missions. The former becomes purchasable after you complete the first scripted Empire Shipping mission, and the latter becomes purchasable once you complete the three scripted Empire Shipping missions and beat a special bounty mission, available through the bar.

If you're having trouble finding the bounty mission despite having finished the Empire Shipping missions, you need a decent amount of combat experience (kills) to be able to start it.

## Are there any cheats?
Not as such. However, the Lua console (accessible with F2) allows you to modify _many_ things, including adding credits, refuelling or adding outfits.

Two simple examples:

```
player.pay( 1000 ) -- This will give you 1000 credits.
player.refuel() -- This will fully refuel your ship.
```
... And a slightly more complex set:

```
player.pilot():setInvincible() -- Makes you invulnerable until you next reload.
player.pilot():setInvincible(false) -- Makes you vulnerable again.
```

For (much) more, see the full Lua API documentation.

## Are there any mods?
Currently no, however we accept contributions from everyone and actively encourage everyone to help out with Naev. In the long run we do plan to have some sort of mod system to allow much more flexibility, but at the moment if you want to add user content you have to modify the ndata or create a new ndata.


# Development
## How can I translate Naev to $FOO language?
There is currently no NLS nor real translation support. Before being able to properly support and ask for translations the following has to be solved:

Naev must be mature. We can not have strings changing all the time making maintaining translations impossible.
Need unicode rendering support. Currently only ASCII is supported.
Need a sane mechanism to detect when translations are out of date or not done.
Need sane tools to help with Lua translations.
As you can see it is not really recommended. Although nothing is stopping anyone from trying to tackle these problems. The main issue to avoid is increasing maintenance or complexity of mission development. As that can impact the entire project.