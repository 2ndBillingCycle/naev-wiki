Mission scripting is something that most people can do. Missions in Naev are written in the [Lua][] scripting language. For those who don't have any experience with programming or scripting, there are mission templates available for creating simple missions.

The Naev Lua API can be found [here][lua-api].

A Lua script is a plaintext file using the `.lua` file extension. No special tools are needed to edit a script, any text editor will do. In Naev, mission files are stored in the [`dat/missions/`][dat-missions] folder. Events go into the [`dat/events/`][dat-events] folder.

## How missions work

A mission is offered to the player through one of several means. Most missions are started when the player has landed and talks to an NPC in the spaceport bar, but it's also possible for missions to start in space. Typically, the player will be given a brief explanation of what the mission is about, as well as the opportunity to decline. Once the mission starts, the player may choose to cancel the mission at any time by going to the Information Menu (default key <kbd>i</kbd>), selecting the mission on the **Missions** tab and clicking the **abort** button. Otherwise, the player can complete or fail the mission, depending on their performance.

To make a mission work, the following is needed:

- An entry in [[Mission.xml|mission.xml]]

  The master mission index (found in [`dat/mission.xml`][dat-mission]) is what the game uses for reference. This file determines the in-game name of the mission, and it tells the game where the mission script is located. It also tells the game when and where to spawn the mission. Note that the path for the mission file is relative to [`dat/missions/`][dat-missions].

  See the [[Mission.xml]] article for more information.

- A `create()` function in the mission script

  The mission script must contain a `create()` function. This function is the code entry point for the mission, no matter how it is started. Missions started from spaceport bar NPCs and the mission computer also need an `accept()` function, which is the function that gets called when the player approaches the NPC or accepts the computer mission.

- A [`misn.accept()`][misn-accept] call

  A mission is not considered "active" until [`misn.accept()`][misn-accept] has been called. This function registers the mission in the player's mission log and activates the OSD.

  _Note: [`misn.accept()`][misn-accept] is **NOT** the same thing as `accept()`! Typically, [`misn.accept()`][misn-accept] is called in the mission's `accept()` function._

- A [`misn.finish()`][misn-finish] call  

  An active mission can end in two ways. The first is when the player manually aborts the mission. The other way is when the mission script calls [`misn.finish()`][misn-finish]. This function de-registers the mission, deactivates the OSD, removes all mission related information (such as mission cargo) and stops executing the mission script. [`misn.finish()`][misn-finish] should be the last command called in any mission script.

## Events

Events are much like missions in that they use largely the same API and can make about the same things happen in the universe. The difference between events and missions is that while missions are player-accepted and can be player-aborted, the same is not true for events. An event will trigger according to certain conditions, and when it does, the player does not have the ability to prevent it. An event will continue to run until it is ended, again according to certain conditions.

To make an event work, the following is needed:

- An entry in [[Event.xml|event.xml]]

  The master event index (found in [`dat/event.xml`][dat-event]) is what the game uses for reference. This file determined the in-game name of the event, and it tells the game where the event script is located. It also tells the game when and where to spawn the event. Note that the path for the event file is relative to [`dat/events`][dat-events].

- A `create()` function in the event script

  The event script must contain a `create()` function. This function is the code entry point for the event.

- An [`evt.finish()`][evt-finish] call

    An active event can end in only one way, and that is when the mission script calls [`evt.finish()`][evt-finish]. This function de-registers the event, removes all event related information and stops executing the mission script. [`evt.finish()`][evt-finish] should be the last command called in any event script.

## Examples

There are several annotated example mission scripts available. If you have a copy of the Naev source code ([available on github][naev-github]), you will find these in [`docs/missions/`][docs-missions]. This page lists them as well.

- There is a [template for a mission started by talking with someone in a spaceport bar][bar-template]
- There is a [mission computer template][computer-template], for missions available through the **`Missions`** tab on planets
- [A more complete example][complete-template], explaining several aspects of mission scripting, including some pitfalls that should be avoided

## Ideas to implement

The best way to learn to develop missions for Naev is by implementing them. If you can't think of an idea or want a simple concept to get started, check out the [[Mission Ideas]] page. It has general, simple missions that could fit into the current world of Naev. If you need help or advice you can always reach out on [IRC][] or [Discord][].

## How to achieve common tasks

### Spawning a pilot

Pilots can be added using [`pilot.add()`][pilot-add], which spawns fleets defined in [`dat/fleet.xml`][dat-fleet], or using [`pilot.addRaw()`][pilot-addraw], which spawns ships defined in [`dat/ships/`][dat-ships].

AI names are taken from the AI script file names, found in [`dat/ai/`][ai-dir].

## Tips

There are some things that you should keep in mind when scripting a mission:

Testing missions
Mission scripts are loaded when you load a game. If you make a change to your script, you usually only have to reload your game to test the changes. However, keep in mind that the mission will NOT re-run code that was previously run! Typically, this means that calls made in the create() or accept() functions will require you to restart the mission to see the changes.

If you want to force start an event while testing use naev.eventStart() and to force start missions use naev.missionStart(). Note that the event "name" mentioned here is from the relevant xml file!

Unlike mission Lua code, the XML data is only loaded at game startup. If you change anything about the mission appearance, you will need to restart Naev before the changes are applied.

If an error occurs during execution the stack trace is both shown in the Lua console and printed to stderr. You can also use print(x) to print something to the Lua console to help debug.

The abort() function
Missions (not events) may or may not include an abort() function. This function will be called when the player aborts the mission using the abort button in the game. Scripters may use this function to perform cleanup on abort, such as removing stack variables or displaying a customized abort message. A mission does not need an abort() function to work.

Tables
Lua can use anything as a table index, but most commonly tables are indexed numerically. It's important to note that Lua's indexing starts at 1, unlike other languages where it starts at 0. For example:

my_table = {} -- Declares the table.
my_table[1] = "string" -- First element
my_table[2] = "string" -- Second element

Saving tables
All information is saved automatically except tables. To save tables you must set "__save" to true. That can be done with:

my_table = {} -- Creates the table
my_table["some_data"] = 5 -- Some data to save
my_table["__save"] = true -- Will save the table

The table will then be available when the mission gets loaded up from a savegame.

Mission NPCs versus mission-generated NPCs
A mission can add NPC characters to the spaceport bar for the player to interact with. There are, however, two cases in this: the NPC that actually gives the mission and NPCs that are used as part of the mission. In the first case, there can be only one NPC, and it uses a somewhat different command. The reason for this is that a kind of bootstrapping process is going on. While the mission is inactive no mission related data is kept, yet the mission-associated NPC still has to show up.

Here is an example showing the difference in usage between the two NPC types:

function create() -- code entry point.
    misn.setDesc("This is the description text for the NPC")
    misn.setNPC("Name of the NPC", "none") -- none is for the portrait. Normally you'd use something else.
end

function accept() -- Remember, function accept() automatically gets called when the player approaches the mission NPC.
    misn.accept() -- Normally, you'd give the player the opportunity to decline before doing this.
    misn.npcAdd("my_function", "My NPC's name 1", "none", "My NPC's description 1", 5) -- Notice how you get to specify the hooked function yourself in this case.
    misn.npcAdd("my_function", "My NPC's name 2", "none", "My NPC's description 2", 5) -- Notice how you get to add as many NPCs as you like, now that the mission has started.
end

Iterating over pilots
When iterating over the pilots in a fleet, ALWAYS make sure the pilots exists before trying to do anything with them, unless you're certain that they exist! If a ship is destroyed in the game, its pilot handle will not automatically be removed (and can still be referenced). Here is an example of typical iteration code:

for i, j in ipairs(some_fleet) do -- i stores the index number, j stores the pilot
    if j:exists() then -- equivalent to pilot.exists(j)
        -- j does indeed exist, you may do something with it now.
    end
end

Spawning one-pilot fleets
Quite often, you'll want to add a single ship to a system, rather than a whole fleet. However, even single ships belong to a fleet. When you spawn them using pilot.add, you will get a table containing all the pilots in your fleet, even if there is only one pilot. Here is a short-hand notation to get the pilot right when you spawn it:

my_pilot = pilot.add("Civilian Gawain")[1] -- Assign the first element of the table returned by pilot.add() to my_pilot.

Including code
In Lua you may include other Lua files. Doing so will give you access to the code in those Lua files as if you copy-pasted it into your own code. There are some useful, generic functions available in the scripts directory. The include path is relative to the naev binary. For example:

include "scripts/jumpdist.lua" -- include external code
my_table = getsysatdistance(system.cur(), 2, 3) -- Get a table of all systems at least 2 and at most 3 jumps away from the current system

Making timer-based cutscenes
When making events happen one after another, you're going to need timer hooks. Timer hooks trigger n milliseconds after they were created, where n is the first argument. Since Lua doesn't have a sleep function, you are going to need to set the times for the hooks so that they will trigger in succession. A good way to make the sequence more manageable is by keeping a helper variable:

local delay = 0 -- "local" means the variable only exists within the current function.
hook.timer(delay, "playerControl", true) -- First argument is the delay, second argument is the function to call when the hook triggers, third argument is the argument to pass to the function
delay = delay + 2000 -- time between last timer and next timer
hook.timer(delay, "zoomTo", joe)
delay = delay + 4000 -- time between last timer and next timer
hook.timer(delay, "showText", Jorscene[1]) 

Giving pilots orders in manual control
Pilots may be put under manual control, and given specific orders. These orders go in a queue, and will be executed consecutively. If you want to abort the current order and issue a new one right away, you should clear the order queue first by using pilot.taskClear() or a new pilot.control(). Note also that you may hook the pilot with hook.pilot(p, "idle"). This hook will trigger as soon as the pilot has no orders in its queue.

Passing multiple arguments to a hooked function
Hooks are very useful, but they only allow you to pass a single argument to the function they call. If you want to pass more than one argument, you can get around this by storing your arguments in a table and passing the table. Example:

hook.timer(1000, "my_function", {pilot = my_pilot, text = "Hello!"}) -- Pass a table with custom named indices

function my_function(args)
    p = args.pilot -- Get pilot from the table. In this example, this will be my_pilot.
    t = args.text -- Get text from the table In this example, this will be "Hello!".
    pilot.broadcast(p, t) -- Make pilot p broadcast text t
end

[lua]: <https://www.lua.org/manual/5.1/> "Lua 5.1 Manual"
[lua-api]: <http://api.naev.org/> "Naev Lua API"
[dat-missions]: <https://github.com/naev/naev/tree/master/dat/missions> "dat/missions/ on GitHub"
[dat-events]: <https://github.com/naev/naev/tree/master/dat/events> "dat/events/ on GitHub"
[dat-mission]: <https://github.com/naev/naev/blob/master/dat/mission.xml> "dat/mission.xml on GitHub"
[misn-accept]: <http://api.naev.org/modules/misn.html#accept> "misn.accept() in Naev Lua API docs"
[misn-finish]: <http://api.naev.org/modules/misn.html#finish> "misn.finish() in Naev Lua API docs"
[dat-event]: <https://github.com/naev/naev/blob/master/dat/event.xml> "dat/event.xml on GitHub"
[evt-finish]: <http://api.naev.org/modules/evt.html#finish> "evt.finish() in the Naev Lua API docs"
[naev-github]: <https://github.com/naev/naev> "Naev source code hosted at GitHub"
[doc-missions]: <https://github.com/naev/naev/tree/master/docs/missions> "docs/missions/ folder on GitHub"
[bar-template]: <https://github.com/naev/naev/blob/master/docs/missions/bar_template.lua> "Template for a mission started in the spaceport bar"
[computer-template]: <https://github.com/naev/naev/blob/master/docs/missions/computer_template.lua> "Template for a mission available the the mission computer"
[complete-template]: <https://github.com/naev/naev/blob/master/docs/missions/complete.lua> "A complete example of a mission script"
[irc]: <http://webchat.freenode.net/?channels=naev> "#naev on Freenode"
[discord]: <https://discord.gg/nd2M5BR> "Naev Discord"
[pilot-add]: <http://api.naev.org/modules/pilot.html#add> "pilot.add() in Naev Lua API docs"
[dat-fleet]: <https://github.com/naev/naev/blob/master/dat/fleet.xml> "dat/fleet.xml on GitHub"
[pilot-addraw]: <http://api.naev.org/modules/pilot.html#addRaw> "pilot.addRaw() in Naev Lua API docs"
[dat-ships]: <https://github.com/naev/naev/tree/master/dat/ships> "dat/ships/ folder on GitHub"
[ai-dir]: <https://github.com/naev/naev/tree/master/dat/ai> "dat/ai/ folder on GitHub"