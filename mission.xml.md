Like any XML document, mission.xml contains exactly one root element. In this case, the &lt;Missions&gt; tag and it's corresponding &lt;/Missions&gt; closing tag begin and end the mission.xml document. 
The root tag contains multiple &lt;mission&gt; tags, which define individual missions.

# Sample Mission Tag

The following XML snippet demonstrates all the tags that can make up the XML portion of a NAEV mission:

```
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

# Tag by Tag Explanation of the Mission XML

The &lt;mission&gt; xml tag and its children determine some basic attributes of the mission. Read on for explanations about what they do. Only the &lt;unique /&gt; tag is self-closing. All other tags must be paired: one opening tag such as &lt;chance&gt; with a similar closing tag such as &lt;/chance&gt;. The content of the tag belongs between the opening and closing tag.
Mission Tag

The &lt;mission&gt; tag defines an individual mission. Each mission tag has a name attribute, declared in the form name="sample_name" before the concluding &gt; of the opening tag. The &lt;mission&gt; tag must contain a &lt;lua&gt; tag and an &lt;avail&gt; tag, and can also contain an optional &lt;flags&gt; tag.
Lua Tag

The &lt;lua&gt; tag can contain text, but not another XML tag. It links the mission XML to a corresponding Lua file. To find the file, the NAEV engine looks within the directory /naev/dat/missions/ for a file with the same name as the content of the tag. In the example snippet above, the tag &lt;lua&gt;example2&lt;/lua&gt; points to the file naev/dat/missions/example2.lua This tag can also point to files in subdirectories. &lt;lua&gt;neutral/example2&lt;/lua&gt; points to the file naev/dat/missions/neutral/example2.lua Unless the &lt;lua&gt; tag names a valid file, the mission will not appear in the game.
Flags Tag

The &lt;flags&gt; tag is optional. If it appears in a mission's XML, the tag can contain a &lt;unique&gt; tag, but no other content.
Unique Tag

At the moment, there is only one valid flag tag. The &lt;unique /&gt; tag has no content. If it appears in a &lt;flags&gt; tag, it ensures that the relevant mission will not appear again if that mission exits with the Lua API function mission.finish( true). Missions can have multiple end points. If a mission exits with mission.finish( false) that mission may appear again, even if the &lt;unique&gt; flag is present in the mission XML.

## Avail Tag

The &lt;avail&gt; tag contains tags that determine the conditions under which a mission will appear. Although by itself it does nothing, this tag is required for a mission to appear in the game. The &lt;avail&gt; tag can contain only the following tags: &lt;priority&gt;, &lt;cond&gt;, &lt;done&gt;, &lt;chance&gt;, &lt;location&gt;, &lt;faction&gt;, and &lt;planet&gt;.

## Priority Tag

The &lt;priority&gt; tag is optional. If it appears it indicates how important the mission is. Lower priorities are more important. The default is 5.

## Cond Tag

The &lt;cond&gt; tag is optional. If it appears, it must be the child tag of a containing &lt;avail&gt; tag. The &lt;cond&gt; contains text which must be a boolean expression written in Lua. If the expression evaluates to true, and other availability conditions are satisfied, the mission appears in the game. The Lua expression in a &lt;cond&gt; tag is meant to use the NAEV Lua API to check, for instance, whether the player has a high enough combat rating, or is friendly with a certain faction. In the XML snippet above, the tag &lt;cond&gt;var.peek(boolean_condition) == true&lt;/cond&gt; checks whether a mission variable has been set to true.

## Done Tag

The &lt;done&gt; tag is optional. If it appears it must be the child of a containing &lt;avail&gt; tag. The &lt;done&gt; tag contains text which must be the name attribute of another mission. If the tag content names a mission the player has successfully completed (a mission that has exited with misn.finish( true)), then the present mission will be available, assuming other conditions are met. In the XML snippet above, the tag &lt;done&gt;Example 1&lt;/done&gt; means that the mission "Example 2" will only be available after the mission with the name "Example 1" has been successfully completed.

## Chance Tag

The &lt;chance&gt; tag is a required child of an &lt;avail&gt; tag. It can contain only a number larger than or equal to 0. The last two digits of the number in a &lt;chance&gt; tag determine the likelihood a mission will appear when a player lands on a planet. If the chance number is three digits long, the first digit determines how many times that probability is calculated on each landing. A number larger than 200 means the mission may appear more than once simultaneously. A number between 101 and 200 has an equivalent in the 1 to 100 range. The ambiguous case of #00 is treated as 100%, so for example 300 would be 3 missions always, while 299 would be 2 with 99% chance and 301 would be 3 with 1% chance. In the XML snippet above, the tag &lt;chance&gt;220&lt;/chance&gt; means the "Example 2" mission can appear up to two times. Each appearance has a 20 percent probability.

## Location Tag

The &lt;location&gt; tag determines where a mission will appear. This tag is a required child of an &lt;avail&gt; tag. The &lt;location&gt; tag can contain only one of the following texts:

* `None`
* `Computer`
* `Bar`
* `Outfit`
* `Shipyard`
* `Land`
* `Commodity`
* `Space`

Each option corresponds to a location where the mission can be found. Missions located in "Space" are tested each time the player enters the system. In the XML snippet above, the tag &lt;location&gt;Computer&lt;/location&gt; mean that the "Example 2" mission is offered from the Mission Computer.

## Faction Tag

The &lt;faction&gt; tag is an optional child of an &lt;avail&gt; tag. It limits the mission to appear in ports that belong to a specific faction. To be valid, this tag should contain text identical to the name attribute of a &lt;faction&gt; tag in the file naev/dat/faction.xml In the XML snippet above, the tag &lt;faction&gt;Some Faction&lt;/faction&gt; means that the mission will appear only on planets belonging to the faction with the name "Some Faction" defined in naev/dat/faction.xml There can be multiple &lt;faction&gt; tags in each &lt;avail&gt; tag.
Planet Tag

The &lt;planet&gt; tag is an optional child of an &lt;avail&gt; tag. It allows the mission to appear on specific planets. To be valid, this tag should contain text identical to the name attribute of a &lt;asset&gt; tag in the file naev/dat/asset.xml In the XML snippet above, the tag &lt;planet&gt;Some Planet&lt;/planet&gt; means that the mission can appear on the planet with the name "Some Planet" defined in naev/dat/asset.xml There can be multiple &lt;planet&gt; tags in each &lt;avail&gt; tag.