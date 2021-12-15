# The Binding of Isaac: Repentance Modding FAQ

<br />

## Read the Docs

Search [Wofsuage's API documentation](https://wofsauge.github.io/IsaacDocs/rep/) before you ask a question.

<br />

## Use Discord Syntax Highlighting

When pasting code into Discord, make sure to paste it in a "code block" by using triple backticks. And make sure to use syntax highlighting for the language, by typing the name of the language next to the backticks.

For example, this is a code snippet for Lua:

````
```lua
local foo = "bar"
Isaac.DebugString(foo)
```
````

Or, a code snippet for TypeScript:

````
```ts
const foo = "bar";
Isaac.DebugString(foo);
```
````

<br />

## Format Code

When asking for help, it is common to post a code-snippet. Before posting code, **please format it with an auto-formatter** so that it can be easily understood by others.

- In Lua, use [Lua Beautifier](https://goonlinetools.com/lua-beautifier/), [LuaFormatter](https://github.com/Koihik/LuaFormatter), or [lua-fmt](https://github.com/trixnz/lua-fmt).
- In TypeScript, use [Prettier](https://prettier.io/).

<br />

## No Screenshots

When asking for help, it is common to post a screenshot of your code. **Don't do this**, because it isn't editable or copy-pastable. Instead, post the actual text of the code. Also see the section on [Discord syntax highlighting](#use-discord-syntax-highlighting).

<br />

## Use Minimal, Reproducible Examples

When asking for help, it is common to post a bunch of code that is unrelated to the problem. This makes questions hard to understand and usually means that the person asking the question is putting forth very little effort.

Please read [this StackOverflow post on how to create minimal, reproducable examples](https://stackoverflow.com/help/minimal-reproducible-example).

<br />

## Don't Use Link Previews

Link previews can clutter the conversion, turning a tiny message into a massive wall of text. It is courteous to enclose all links in <>.

For example:

```
Here's a link to my code: <https://github.com/IsaacScript/isaacscript-common/blob/main/src/functions/array.ts#L3-L16>
```

<br />

## How do I get started modding Isaac?

We generally recommend that people watch the Lytebringr's series of [video tutorials on YouTube](https://www.youtube.com/playlist?list=PLMZJyHSWa_My5DDoTQcKCgs475xIpQHSF). These were made for Afterbirth+, but not much has changed now that Repentance is out, so they are still your best bet for learning the ropes.

The main difference with Repentance is that the mods folder is now located at:

```
C:\Program Files (x86)\Steam\steamapps\common\The Binding of Isaac Rebirth\mods
```

Other resources:

- Cucco has also made a series of [video tutorials on YouTube](https://www.youtube.com/playlist?list=PLUYzSIp7NO8cEer2FmtxSXlXoMFirvYDN).
- The IsaacScript website has a good [text tutorial](https://isaacscript.github.io/docs/example-mod) on how to build an example mod using [IsaacScript](https://isaacscript.github.io/).

<br />

## How do I use the resource extractor? How do I unpack the game files?

By default, the game's resources are located here:

```
C:\Program Files (x86)\Steam\steamapps\common\The Binding of Isaac Rebirth\resources
```

However, this directory will be mostly empty unless you run the provided resource extrator. It is located here:

```
C:\Program Files (x86)\Steam\steamapps\common\The Binding of Isaac Rebirth\tools\ResourceExtractor\ResourceExtractor.exe
```

Once you run the extractor, the resources directory will fill up with all of the XML files, ANM2 files, images, and other various files that the game uses.

<br />

## Why is my sprite showing up in-game as a black square?

This happens when the sprite is saved with the wrong bit depth. Set it at 32-bit depth specifically. (Don't set it to be "Automatic".)

<br />

## How do I make sprites in the Isaac style?

Watch [this video](https://www.youtube.com/watch?v=cJ68vYqzSm0) by LeatherIceCream.

<br />

## Why isn't my code working? How do I know when errors occur?

Lua is an interpretted language, which means that if you make a typo or have otherwise bad code, you will only be able to discover it once the program actually runs. If the Lua interpreters encounters an error, it will write it to the game's log.txt file.

By default, this file is located at: `C:\Users\james\Documents\My Games\Binding of Isaac Repentance\log.txt`

Open this file and search it carefully for Lua-related errors. (Ctrl + f for "error" is a good start.) This will often tell you the line number that you messed up on.

It is also recommended to set `FadedConsoleDisplay=1` in the options.ini file so that it is a little bit more easy to discover errors while you play.

For people comfortable with command-line applications, use my [isaac-log-viewer](https://github.com/Zamiell/isaac-log-viewer) script and have it running on a second monitor as you code & test.

<br />

## When is the log.txt cleared?

Every time that you open the game, all of the contents of the log.txt is deleted. Thus, if you need information from the log after a bug occurs, make sure that you do not re-launch the game.

<br />

## How do I troubleshoot my code?

When you write programs, they may not work right away. Your first reaction should not be to paste a bunch of code into Discord and ask "why doesn't this work?". Doing that means you aren't putting forth very much effort to try and solve the problem on your own.

The tried-and-true method to figure out almost any bug is called "print debugging". In Isaac, this means printing out a bunch of messages to the log.txt file so that you can view it and see which parts of your code are being executed, and which are not. So, go to a bunch of places in your code and add `Isaac.DebugString("GETTING HERE 1")`, `Isaac.DebugString("GETTING HERE 2")`, and so on. Then, run your code (i.e. walk around in-game and trigger the bug), and study the log.txt file to try and see what is happening.

Often times, the reason that your code is not working is that your variables are not what you think they are. So, print out what the variables are at each step of the way so that you can confirm that they are what you think they are. Use something along the lines of: `Isaac.DebugString("GETTING HERE - FOO IS: " .. tostring(foo))`

<br />

## I modified an XML file and the game crashes when I open it or when I go into a new run.

A crash means that the XML file is invalid, meaning that you messed up somewhere while editing the file. Start over from scratch and make tiny edits one at a time until you find the exact part that crashes the game.

Another helpful troubleshooting tool is validators like [xmlvalidation.com](https://www.xmlvalidation.com/).

<br />

## I enabled a mod and now my game is crashing. How can I fix this?

You can try looking through the log.txt file to see if anything interesting is there. However, in the vast majority of cases, the log will not show any helpful information when the game crashes.

Instead, you can find the problem by simply disabling your mods one by one until you find the exact mod that is causing the crash. Then, you can report it to the developer of the mod, or try to manually fix the code yourself.

<br />

## What is the ID of [the sound that I care about]?

Simply use [this mod](misc/sounds-display.lua), which will tell you what the ID of any currently playing sound effect is.

<br />

## What is Single Line Responsibility (SLR)?

When writing code, put some effort into making it look nice and be easy to read for others, especially if you are showing it to other people or asking for help. In this vein, it is a good idea to follow the "single line responsibility" rule - meaning that **one line** should only do **one thing**. Read [this blog](https://midu.dev/single-line-responsability-haz-una-cosa-por-linea/) for more details about why SLR is great.

<br />

## How do I code X?

The fastest way to figure out how to do something is to simply download a few mods that provide similar functionality to what you want to do, and then study the code.

<br />

<br />

## How do I apply a costume to my character?

This is called a "null costume" and it is accomplished via the `EntityPlayer.AddNullCostume()` method. For more information, see [Lytebringr's 8th video](https://www.youtube.com/watch?v=R1CdCyGL1DQ&list=PLMZJyHSWa_My5DDoTQcKCgs475xIpQHSF&index=9).

<br />

## What is a callback?

Mods affect the game by putting code inside of *callbacks*. Each callback fires when a particular event happens in the game. There are 72 different callbacks to choose from, so you have to choose the right one depending on what you want to do.

For example, the most basic callback is `MC_POST_GAME_STARTED`, which fires once at the beginning of a new run. You would put code in here to do something custom at the beginning of every run.

Another common callback that mods use is `MC_POST_UPDATE`, which fires on every single update frame (i.e. 30 times per second). You would put code in this callback for custom items that have constant effects.

Go through the [official docs](https://wofsauge.github.io/IsaacDocs/rep/enums/ModCallbacks.html) and read what all of the callbacks do so that you can get familiar with them.

<br />

## How do I create a new floor/level/stage?

Unfortunately, Isaac does not natively support modded custom floors. BudJMT and DeadInfinity have built a custom system called [StageAPI](https://github.com/Meowlala/BOIStageAPI15) that allows mods to add custom floors in a hacky way. However, StageAPI is not easy to use, so unless you are already an experienced Isaac modder & coder, you should stick to more simple projects.

<br />

## How do I modify the Devil Room / Angel Room chances?

There is no built-in way to do this, so you will have to get inventive. For the most control, you can delete all vanilla Devil/Angel doors and completely re-implement the system from scratch. Otherwise, you can temporarily give items to the player such as Goat Head or Rosary Bead, or use things like [Game.SetLastDevilRoomStage()](SetLastDevilRoomStage ) or [Level.SetRedHeartDamage()](https://wofsauge.github.io/IsaacDocs/rep/Level.html#setredheartdamage). You also might want to use [LevelStateFlags](https://wofsauge.github.io/IsaacDocs/rep/enums/LevelStateFlag.html).

<br />

## How do I make the costume on my custom character persistent?

Simply use [Sanio's library](https://steamcommunity.com/sharedfiles/filedetails/?id=2541362255) for this, or study the source code and reimplement it yourself.

<br />

## What is the difference between an API and a library?

Some mods on the workshop package functionality together as an abstraction for other poeple to use. In software, this is what is typically known as a "library". As a programmer, it is usually a lot easier to leverage other people's battle-tested libraries than to roll your own from scratch.

On the other hand, an API is short for application programming interface, and it is exactly what it sounds like. An application might want to expose some functionality to external users and software, and it would do that through an explicitly defined interface. Libraries expose an API so that end-users can consume them. But note that *any* software can have an API, not just a library. For example, the Revelations Mod is a popular mod that adds new floors, bosses, and items to the game. But it also exposes an API so that it can be made compatible with other mods.

Historically, Isaac libraries have labeled themselves as "APIs", but this is a misnomer. Some examples of this include [StageAPI](https://github.com/Meowlala/BOIStageAPI15) and [MinimapAPI](https://github.com/TazTxUK/MinimapAPI). On the other hand, an example of a library that is correctly named is Sanio's [Costume Protector](https://steamcommunity.com/sharedfiles/filedetails/?id=2541362255).

If you are creating a new library, please use the correct terminology to name your project, which helps prevent confusion for newcomers to the Isaac modding scene.

<br />

## How do I overwrite vanilla music?

- For normal music replacement, you can simply blow away the respective vanilla resource files.
- For dynamic replacement, use Taz's [Music Mod Callback](https://steamcommunity.com/sharedfiles/filedetails/?id=2491006386).

<br />

## How do I iterate over a list object from the API?

For example, in Lua:

```lua
local game = Game()
local level = game:GetLevel()
local rooms = level:GetRooms()
for i = 0, rooms.Size - 1 do
  local room = rooms:Get(i)
  -- Do something with the room
end
```

For example, in TypeScript:

```ts
const game = Game();
const level = game.GetLevel();
const rooms = level.GetRooms();
for (let i = 0; i < rooms.Size; i++) {
  const room = rooms.Get(i);
  // Do something with the room
}
```

<br />

## How do I get a familiar to follow the player like Brother Bobby does?

For example, in Lua:

```lua
function postFamiliarInitMyFamiliar(familiar)
  familiar:AddToFollowers()
end

function postFamiliarUpdateMyFamiliar(familiar)
  familiar:FollowParent()
end
```

For example, in TypeScript:

```ts
function postFamiliarInitMyFamiliar(familiar: EntityFamiliar) {
  familiar.AddToFollowers();
}

function postFamiliarUpdateMyFamiliar(familiar: EntityFamiliar) {
  familiar.FollowParent();
}
```

<br />

## What are ANM2 files?

- In Isaac, animations are represented by anm2 files in the `resources/gfx` folder.
- Each entity in the game has an associated anm2 file.
- Additionally, UI elements are rendered using various anm2 files (in the `resources/gfx/ui` folder).
- anm2 files are simply XML files with a different file extension.
- To edit the vanilla animations or add new animations, you can:
  - Edit the files directly using a text editor. (Kilburn does this.)
  - Edit the files using the provided Isaac Animation Editor, which is located at: `C:\Program Files (x86)\Steam\steamapps\common\The Binding of Isaac Rebirth\tools\IsaacAnimationEditor\IsaacAnimationEditor.exe`

<br />

## How do you use StageAPI to add new bosses?

See [this screenshot](https://cdn.discordapp.com/attachments/205854782542315520/895485829458325604/unknown.png) from Xalum.

<br />

## What is the difference between `require` and `include`?

See the [docs](https://wofsauge.github.io/IsaacDocs/rep/tutorials/Using-Additional-Lua-Files.html).

<br />

## How do I edit rooms?

The official room editor is provided with the game and is located at:<br />
`C:\Program Files (x86)\Steam\steamapps\common\The Binding of Isaac Rebirth\tools\RoomEditor\RoomEditor.exe`

This was the tool that Edmund used to create all of the rooms for Rebirth and Afterbirth. However, the official editor is not very good and does not work properly with any Repentance rooms.

In 2014, Chronometrics made a 3rd party room editor called [Basement Renovator](https://github.com/Basement-Renovator/Basement-Renovator) to improve upon the official editor. It is open-source and is located on GitHub. Since Basement Renovator is so much better than the official room editor, even the official developers now use Basement Renovator. (This is why none of the Repentance rooms will work in the official editor.)

Basement Renovator is written in Python, so you can either run it from source or simply download a pre-bundled exe file from the [releases page](https://github.com/Basement-Renovator/Basement-Renovator/releases).

<br />

## Where can I see the code for [some vanilla item] or [some vanilla mechanic]?

You can't. The game is programmed in the C++ programming language and the source code is propritary, for what should be obvious reasons. This means that if you want to make a custom item that works in a similar way to a vanilla item, you will have to completely reimplement it yourself from scratch. (You can often use the wiki as an implementation reference.)

<br />

## How do I know when a player has picked up a collectible item?

There is no vanilla callback for this. As a workaround, you can check `EntityPlayer.IsItemQueueEmpty()` on every PostUpdate frame, and then check `EntityPlayer.QueuedItem` when it is not empty. Obviously, this will not work for items that never get queued.

For IsaacScript users, you can simply use the provided `[MC_POST_ITEM_PICKUP](https://isaacscript.github.io/docs/function-signatures-custom#mc_post_item_pickup)` callback.

If you want to implement this callback yourself, the source code / algorithm is provided [here](https://github.com/IsaacScript/isaacscript-common/blob/main/src/callbacks/itemPickup.ts).

<br />

## What is the difference between `pairs` and `ipairs`?

- `pairs` is for iterating over Lua tables that represent a [map](https://en.wikipedia.org/wiki/Associative_array). In other words, something with key/value associations.
- `ipairs` is for iterating over Lua tables that represent an [array](https://en.wikipedia.org/wiki/Array_data_structure). In other words, something that contains a list of elements.

[Code speaks louder than words](https://code.labstack.com/9n1B9g7n).

Since Lua is [untyped](https://www.tutorialspoint.com/What-are-the-differences-between-untyped-and-dynamically-typed-programming-languages) and uses tables to represent multiple different data structures, `pairs` and `ipairs` serve as a flag to tell the reader what the underlying data structure really is.

<br />

## How do you tell what the entity type, variant, or subtype of a particular entity is?

You can:

1) Type "spawn x" into the in-game console. For example, "spawn confessional" would show that the Confessional entity has an identifier of 6.17. This means that it has an entity type of 6 and a variant of 17.
2) Or, you can ctrl+f in the "resources/entities2.xml" file (or the "resources-dlc3/entities2.xml" file) for the entity you want.
