# Manual

<!--TOC-->

## Introduction

Welcome to the Naev player's manual.

This manual is a work in progress. If there's anything you feel it needs, feel free to let us know via forum or this page's discussion tab.

This manual primarily expands on concepts that are omitted or only briefly mentioned in the in-game tutorial. Some things are better learned hands-on, so if you're looking for the basics like ship piloting and combat, please check out the in-game tutorial.

## About Naev

Naev is a 2D space trading and combat game, taking inspiration from the [Escape Velocity][escape-velocity-wiki] series, among others.

You pilot a space ship from a top-down perspective, and are more or less free to do what you want. As the genre name implies, you're able to trade and engage in combat at will. Beyond that, there's an ever-growing number of storyline missions, equipment, and ships; Even the galaxy itself grows larger with each release. For the literarily-inclined, there are large amounts of lore accompanying everything from planets to equipment.

<!--
Which honors the spirit of the forum?

- Discord
- GitHub issue tracker
-->

We're always open to feedback and contributions, you can contact us via [IRC][naev-freenode] or post on the [forum][naev-forum] (_archived_).

Downloads for many operating systems can be found at the [downloads page][downloads].

## Controls

> Main article: [[Keybinds]]

<!--
How are keyboard entries best rendered?

- <kbd>Ctrl+X</kbd>
- <kbd>Ctrl</kbd>`+`<kbd>X</kbd>
- <kbd>Ctrl</kbd>+<kbd>X</kbd>
- <kbd>Ctrl</kbd><kbd>X</kbd>
-->
While Naev is primarily keyboard-oriented, mouse flying can also be toggled by clicking the middle mouse button or <kbd>Ctrl</kbd><kbd>X</kbd> by default. This will cause your ship to point towards the cursor, and by default engage the engines as well.

## Outfits

Outfits are items that are bought and sold through spaceport outfitters. They include items that are equipped directly on ships (weapons, engines, etc.) as well as ammunition, licenses, and maps.

Generally speaking, in Naev's parlance any item that isn't a ship or commodity is an outfit.

## Slots

Slots are how Naev categorizes outfits. Each ship has a fixed number of slots which fit equipment, functioning as a way to limit the roles a given ship may fill.

Each slot has both a type and a size. The three slot types are weapon, utility, and structure. All equippable outfits fall into one type or another.

There are also three slot sizes, used as an upper limit for what fits into a slot.

### Weapon Slots

Weapon slots are rather self-explanatory. Anything that deals damage or launching projectiles (or fighters) fits into a weapon slot.

- Cannons
- Turrets
- Beams
- Launchers
- Fighter bays

### Utility Slots

Utility slots are used primarily for high-tech outfits, including manually-triggered "active" outfits such as afterburners. They're also used for outfits that have significant impacts on the ship's regeneration and other dynamic properties.

- Reactors (Energy regeneration)
- Shield Boosters (Shield regeneration)
- Scramblers (Electronic warfare masking)
- Afterburners and other active outfits

### Structure Slots

Structure slots are used for simplistic "passive" upgrades.

- Batteries
- Shield Capacitors
- Cargo Pods
- Fuel Pods

### Slot Sizes

The three slot sizes are small, medium, and large. Currently, these sizes are represented in-game by coloured backgrounds: <span style="color:yellow">yellow</span>, <span style="color:green">green</span>, and <span style="color:blue">blue</span>, respectively.

Slot sizes serve as an upper limit. You can't place a large outfit into a medium slot, but you can put medium outfit into a large slot.

## Time

> Main article: [[Time]]

Time in Naev is all standardized according to the Universal Synchronized Time (UST). This is a uniform way to express time across the entire galaxy.

There are three time units in common use, explained below. Currently, time is written as `SCU:STP.hSTU`; a real example might be **`UST 603:3728.91`**.

### Time units

- **STU (Standard Time Unit)**  
  Smallest named time unit. Equal to the Earth second.
  - hSTU: Also known as the hectoSTU, equal to 100 STU. Its usage in-game is broadly equivalent to a minute. Ship chronometers commonly use this as the smallest displayed unit.

- **STP (Standard Time Period)**  
  Most commonly used time unit. STPs are the new hours. 1 STP = 10,000 STU (about 2.8 Earth hours).

- **SCU (Standard Cycle Unit)**  
  Used for long-term time periods. 1 SCU = 5000 STP (about 579 Earth days, or a year and seven months). In informal situations this is generally called a "cycle".

### Time passage

- **Flying in space**  
  When in space, time passes at a rate of 30 STU per second, which is why the GUI's clock increases by 0.01 STP every 3⅓ seconds.

- **Landed**  
  Time does not pass while landed.

- **Takeoff**  
  Taking off takes 1 STP, which means that stopping to refuel during time-sensitive missions is generally a bad idea.

- **Jumping**  
  Hyperspace jumps also take time, generally 1 STP per jump, though some ships such as the Quicksilver take less.

## Reputation

> Main article: [[Reputation]]

Reputation is a fairly complex mechanic, but the most important bit is that factions will become hostile if your reputation with them falls below zero. Being hostile with peaceful factions is mostly unimportant, but hostile military ships will attack on sight.

Reputation can usually be gained (up to a point) by killing a faction's enemies, though it's usually far more efficient to do missions for the faction instead. Killing a faction's ships will often incur a harsh reputation penalty, many times what the benefit would be for killing one of their enemies.

Luckily, if you become hostile with a major faction, most of them offer rehabilitation missions at the mission computer, though making amends is rather expensive.

[escape-velocity-wiki]: <https://en.wikipedia.org/wiki/Escape_Velocity_(video_game)> "Escape Velocity on Wikipedia"
[naev-freenode]: <http://webchat.freenode.net/?channels=naev> "#naev on Freenode"
[naev-forum]: <https://web.archive.org/web/20190414185706/http://forum.naev.org/> "An archive of the Naev forum on The Wayback Machine"
[downloads]: <https://naev.org/downloads/> "Naev downloads"