Like any XML document, [`dat/mission.xml`][] contains exactly one root element. In this case, the `<Missions>` start tag and it's corresponding `</Missions>` end tag begin and end the root element of the [`dat/mission.xml`][] document. 

The root element contains multiple `<mission></mission>` child elements, which define individual missions.

## Sample Mission Tag

The following XML snippet demonstrates all the tags that can make up the XML portion of a Naev mission:

```xml
<mission name="Example 2">
 <lua>example2</lua>
 <flags>
  <unique />
 </flags>
 <avail>
  <priority>5</priority>
  <cond>var.peek(boolean_condition) == true</cond>
  <done>Example 1</done>
  <chance>220</chance>
  <location>Computer</location>
  <faction>Some Faction</faction>
  <planet>Some Planet</planet>
 </avail>
</mission>
```

## Tag by Tag Explanation of the Mission XML

The `<mission></mission>` xml element and its child elements determine some basic attributes of the mission. Read on for explanations about what they do. Only the `<unique />` tag is self-closing. All other tags must be paired: one opening, or start tag such as `<chance>` with a similar closing, or end tag such as `</chance>`. The content of the element belongs between the start and end tags.

### Mission Element

The `<mission></mission>` element defines an individual mission. Each `<mission>` start tag has a `name` attribute, declared in the form `name="sample name"` placed after `<mission` and before the concluding `>` of the start tag. The mission element must contain a `<lua></lua>` element and an `<avail></avail>` element with appropriate content, and can also contain an optional `<flags></flags>` element.

### Lua Element

The `<lua></lua>` element can contain text, but not another XML tags or elements. It links the mission XML element to a corresponding Lua file. To find the file, the Naev engine looks in the directory [`dat/missions/`][] for a file with the same name as the content of the element, without the `.lua` filename suffix. In the example snippet above, the element `<lua>example2</lua>` points to the file `dat/missions/example2.lua`. This element can also point to files in subdirectories. `<lua>tutorial/tutorial</lua>` points to the file [`dat/missions/tutorial/tutorial.lua`][], which is the main mission script for the Tutorial mission. If the `<lua></lua>` element names a file that Naev can't find, the mission will not appear in the game.

### Flags Element

The `<flags></flags>` element is optional. If it appears as a `<mission></mission>` element's child, it can contain a `<unique />` tag, but no other content.

### Unique Element

At the moment, `<unique />` is the only valid child element of the `<flags></flags>` element. The `<unique />` element does not contain any content. If it appears as a `<flags></flags>` child element, it ensures that the relevant mission will not appear again if that mission exits by calling the Lua API function [`misn.finish(true)`][]. Missions can have multiple events or conditions that cause them to end. If a mission exits with [`misn.finish(false)`][`misn.finish(true)`], that mission may appear again, even if the `<unique />` flag is present in the `<flags></flags>` element.

### Avail Element

The `<avail></avail>` element contains child elements that determine the conditions under which a mission will appear. Although by itself it does nothing, this element is required for a mission to appear in the game. The `<avail></avail>` element can contain only the following elements:

- `<priority>`
- `<cond>`
- `<done>`
- `<chance>`
- `<location>`
- `<faction>`
- `<planet>`

### Priority Element

The `<priority></priority>` element is optional, and if it's present should only contain a number. If it appears, it indicates how important the mission is. Lower priorities are more important. The default is `5`.

### Cond Element

The `<cond></cond>` element is optional. If it appears, it must be the child element of a containing `<avail>` element. The `<cond>` element contains text which must be a Lua expression that evaluates to `true` or `false`. If the expression evaluates to `true`, and the other availability conditions are satisfied, the mission appears in the game. The Lua expression in a `<cond>` element is meant to use the [Naev Lua API][] to check, for instance, whether the player has a high enough combat rating, or is friendly with a certain faction. In the XML snippet above, the element `<cond>var.peek(boolean_condition) == true</cond>` checks whether the mission variable `boolean_condition` has been set to `true`, using [`var.peek()`][].

### Done Element

The `<done></done>` element is optional. If it appears it must be the child of a containing `<avail></avail>` element. The `<done></done>` element contains text which must be the the same as the `name` attribute of another mission element's `<mission>` start tag. If the element content names a mission that the player has already successfully completed (a mission that has exited with [`misn.finish(true)`][]), then the present mission will be available, assuming other conditions are met. In the XML snippet above, the element `<done>Example 1</done>` means that the mission "`Example 2`" will only be available after a mission with the attribute `name="Example 1"` has been successfully completed.

### Chance Element

The `<chance></chance>` element is a required child of an `<avail></avail>` element. It can contain only a number larger than or equal to `0`. The last two digits of the number in a `<chance></chance>` element determine the likelihood a mission will appear when a player lands on a planet (i.e. the probability of the mission being made available). If the number is three digits long, the first digit determines how many times that probability is calculated on each landing.

The numbers `101` through `199` inclusive are equivalent to the `1` to `99` range (i.e. both indicate that the mission script has one chance of being called, with there being between a 1% and 99% chance of that happening). A number `200` or larger means the mission may appear more than once simultaneously.

This is useful, for instance, for the Empire Shipping missions, where the same mission script ([`dat/missions/empire/es_cargo.lua`][]) is called to generate a random variation of the same type of mission. Having multiple chances that a mission of this type will show up in the mission computer makes the game feel dynamic.

To further explain the way the value is interpreted, with `#` representing any number from `0` through `9`, the ambiguous case of `#00` is treated as a 100% chance, so for example a `<chance></chance>` element containing `300` would cause the mission to have a 100% chance of showing up 3 times (as long as the other conditions are met). `299` would be 2 chances, each with a 99% chance to happen. `301` would be 3 chances with a 1% chance each. In the XML snippet above, the element `<chance>220</chance>` means the "`Example 2`" mission can appear up to 2 times, and has a 20% probability of appearing each time.

The highest probability a mission can appear is 100% with `<chance>100</chance>`. The largest number of missions that can be generated from one `<mission>` element is 9 with `<chance>9##</chance>`, with `999` meaning that 9 missions each have a 99% chance of showing up, and `900` guaranteeing 9 missions show up.

### Location Element

The `<location></location>` element determines where a mission will appear. This is a required child element of an `<avail></avail>` element. The `<location></location>` element can contain text that matches only one of the following:

* `None`
* `Computer`
* `Bar`
* `Outfit`
* `Shipyard`
* `Land`
* `Commodity`
* `Space`

Each option corresponds to a location where the mission can be found. Missions with a location of `Space` are tested each time the player enters the system. In the XML snippet above, the element `<location>Computer</location>` means that the "`Example 2`" mission is offered from the Mission Computer.

### Faction Element

The `<faction></faction>` element is an optional child of an `<avail></avail>` element. It limits the mission to appearing in ports that belong to a specific faction. To be valid, this element should contain text identical to the content of the `<name></name>` child element of a `<faction></faction>` element in the file [`dat/faction.xml`][]. In the XML snippet above, the element `<faction>Some Faction</faction>` means that the mission will appear only on planets belonging to the faction with the name "`Some Faction`" defined in [`dat/faction.xml`][]. There can be multiple `<faction>` elements in each `<avail>` element.

### Planet Tag

The `<planet></planet>` element is an optional child of an `<avail>>/avail>` element. It allows the mission to appear on specific planets. To be valid, this element should contain text identical to the `name` attribute of an `<asset>` start tag in the folder [`dat/assets/`][]. In the XML snippet above, the element `<planet>Some Planet</planet>` means that the mission can appear on the planet with the name "`Some Planet`" defined in [`dat/assets/`][]. There can be multiple `<planet></planet>` elements in each `<avail></avail>` element.


[`dat/mission.xml`]: <https://github.com/naev/naev/blob/master/dat/mission.xml> "dat/mission.xml on GitHub"
[`dat/missions/`]: <https://github.com/naev/naev/tree/master/dat/missions> "dat/missions/ on GitHub"
[`dat/missions/tutorial/tutorial.lua`]: <https://github.com/naev/naev/blob/master/dat/missions/tutorial/tutorial.lua> "Main tutorial mission script on GitHub"
[`dat/faction.xml`]: <https://github.com/naev/naev/blob/master/dat/faction.xml> "dat/faction.xml file on GitHub"
[`dat/missions/empire/es_cargo.lua`]: <https://github.com/naev/naev/blob/master/dat/missions/empire/es_cargo.lua> "dat/missions/empire/es_cargo.lua mission script on GitHub"
[`dat/assets/`]: <https://github.com/naev/naev/tree/master/dat/assets> "dat/assets/ folder on GitHub"
[`misn.finish(true)`]: <http://api.naev.org/modules/misn.html#finish> "misn.finish() in Naev Lua API docs"
[Naev Lua API]: <http://api.naev.org/> "The Naev Lua API docs"
[`var.peek()`]: <http://api.naev.org/modules/var.html#peek> "var.peek() function in Naev Lua API docs"