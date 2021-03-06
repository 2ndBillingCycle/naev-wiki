Welcome to the Naev player's manual.

This manual is a work in progress. If it appears to be missing something, feel free to let us know on [IRC][] or [Discord][]. You can also suggest changes by [editing this page][edit].

This manual primarily expands on concepts that are omitted from, or only briefly mentioned in the in-game tutorial. Some things are better learned hands-on, so if you're looking for the basics like ship piloting and combat, please check out the in-game tutorial.

## About Naev

Naev is a 2D space trading and combat game, taking inspiration from the [Escape Velocity][escape-velocity-wiki] series, among others.

You pilot a space ship from a top-down perspective, and are more or less free to do what you want. As the genre name implies, you're able to trade and engage in combat at will. Beyond that, there's an ever-growing number of storyline missions, equipment, and ships. Even the galaxy itself grows larger with each release. For the literarily-inclined, there are large amounts of lore accompanying everything from planets to equipment.

We're always open to feedback and contributions, you can contact us via [IRC][] or [discord][].

Downloads for many operating systems can be found at the [downloads page][downloads].

## Controls

Naev is primarily controlled (by default) through <kbd>W</kbd><kbd>A</kbd><kbd>S</kbd><kbd>D</kbd> for movement, <kbd>Space</kbd> and <kbd>Shift</kbd> to fire weapons, left click for selecting targets, and double-click for performing actions on targets. There are many other useful controls as well:

* <kbd>R</kbd> to target the nearest hostile pilot.
* <kbd>T</kbd> to cycle through pilot targets.
* <kbd>P</kbd> to cycle through planet/station targets.
* <kbd>H</kbd> to hail the current target.
* <kbd>B</kbd> to board the current pilot target.
* <kbd>L</kbd> to land on the current planet/station target.
* <kbd>M</kbd> to open the starmap.
* <kbd>I</kbd> to open the Info window.
* <kbd>~</kbd> to toggle double speed.
* <kbd>Home</kbd><kbd>Del</kbd><kbd>Insert</kbd><kbd>End</kbd> to issue orders to escorts ("clear orders", "return to ship", "hold position", and "attack target" respectively).

## Outfits

Outfits are items that are bought and sold through spaceport outfitters. They include items that are equipped directly on ships (weapons, engines, etc.) as well as licenses and maps.

Generally speaking, in Naev's parlance any item that isn't a ship or commodity is an outfit.

## Slots

Slots are how Naev categorizes outfits. Each ship has a fixed number of slots each of which can hold a single outfit. The restriction on the number of slots functions as a way to limit the roles a given ship may fulfill.

Each slot has both a type and a size. The three slot types are weapon, utility, and structure. All equippable outfits fall into one type or another.

There are also three slot sizes, used as an upper limit for what fits into a slot. Slots of a particular size can hold an outfit the same or a smaller size.

Finally, all ships require three core outfits equipped: Core Systems (utility), Engines (structure), and Hull (structure). Core slots can only equip their respective type of core outfit and a ship is not spaceworthy until it has all core slots equipped.

### Weapon Slots

Weapon slots are rather self-explanatory. Anything that deals damage or launches projectiles (or fighters) fits into a weapon slot.

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

Utility slots also include one required Core Systems slot. Core Systems determine the ship's base energy and shield regeneration and capacity.

### Structure Slots

Structure slots are used for "passive" upgrades.

- Batteries
- Shield Capacitors
- Cargo Pods
- Fuel Pods

Structure slots also include one required Engines slot and one required Hull slot. Engines determine the ship's base speed and fuel, while the Hull determines the ship's base hull strength and cargo.

### Slot Sizes

The three slot sizes are small, medium, and large. Currently, these sizes are represented in-game by colored backgrounds: <span style="color:yellow">yellow</span>, <span style="color:green">green</span>, and <span style="color:blue">blue</span>, respectively. (To be supplemented with something colorblind-friendly later on, most likely icons; see [#868](https://github.com/naev/naev/issues/868) for progress on that.)

Slot sizes serve as an upper limit. You can't place a large outfit into a medium slot, but you can put a medium outfit into a large slot.

## Time

All time in Naev is standardized according to Universal Synchronized Time (UST). This is a uniform way to express time across the entire galaxy. A full explanation can be found in the [[Universal Synchronized Time]] article.

There are five commonly used units:

<dl>
  <dt><strong>Seconds</strong></dt>
  <dd>equivalent to Earth seconds and used in the same way.</dd>
  <dt><strong>Hectoseconds</strong></dt>
  <dd>used in the same way as Earth minutes.</dd>
  <dt><strong>Periods</strong></dt>
  <dd>used in the same way as Earth hours.</dd>
  <dt><strong>Decaperiods</strong></dt>
  <dd>used in the same way as Earth days.</dd>
  <dt><strong>Cycles</strong></dt>
  <dd>used in the same way as Earth years.</dd>
</dl>

## Reputation

[[Reputation]] is a fairly complex mechanic, but the most important bit is that factions will become hostile if your reputation with them falls below zero. Being hostile with peaceful factions is mostly unimportant, but hostile military ships will attack on sight.

The player's current reputation can be viewed in-game in the Information Menu (default key <kbd>i</kbd>) section labeled `Reputation`.

Reputation can usually be gained (up to a point) by killing a faction's enemies, though it's usually far more efficient to do missions for the faction instead. Killing a faction's ships will often incur a harsh reputation penalty, much larger than the gain for killing one of their enemies.

Luckily, if you become hostile with a major faction, they will offer rehabilitation missions, available through the mission computer, though making amends is rather expensive.

[escape-velocity-wiki]: <https://en.wikipedia.org/wiki/Escape_Velocity_(video_game)> "Escape Velocity on Wikipedia"
[irc]: <http://webchat.freenode.net/?channels=naev> "#naev on Freenode"
[discord]: <https://discord.gg/nd2M5BR> "Naev Discord"
[downloads]: <https://naev.org/downloads/> "Naev downloads"
[edit]: <https://github.com/naev/naev/wiki/Manual/_edit> "Edit this page"