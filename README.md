![console overhaul](https://github.com/8BitShadow/media-resources/blob/main/console%20overhaul.png?raw=true)
# A utility modpack for Risk of Rain 2

## **This modpack is currently in beta! Do not create mods with dependencies to any of the mods yet!**
Due to the size of of the modpack; it's impossible for a single person to bugtest all the mods and some refactoring is planned, hence the mod is not yet available on the thunderstore to avoid other modders from using the modpack as a dependency <i>yet</i>. Expect the mods to crash or have unexpected behavior constantly and please report any of this in the [issues tab](https://github.com/8BtS-A-to-IA/Console-Overhaul/issues) using the the correct [formatting (todo)]().

## About
Console overhaul is a modding utility modpack for Risk of Rain 2. Made for modders and server administrators alike, by adding multiple new and powerful functions to the in-game 'command console', creating command specific mods, be it for managing players on a server or modding the game experience through only commands, or just using the console is now easier than ever.
<br><br>
Console Overhual currently boasts 3 <b>main systems</b> which work in tandem, 1 minor system and 2 extra command specific expceptions to massively improve upon the vanilla Console. The modpack may also, in the future, improve the look the console to give more of a sleek, less 'developer' feel.
<br><br>
This is the main repository of the modpack where the full stable package of the modpack, or each mod sperately, can be downloaded. Feel free to post any suggestions [here](https://github.com/8BtS-A-to-IA/Console-Overhaul/issues).<br>
If you to support the development of the project, regardless of if you have any programming skill or not, refer to the suggestions in the [developing](#developing) segment.

<details open>
  <summary>Mods:</summary>
  <details>
    <summary><b><a href="https://github.com/8BtS-A-to-IA/Console-Overhaul-TMI">Too Much Information (T.M.I.):</a></b></summary>
  
- The T.M.I system is called either the "Too Much Information" system or the "Player Stats" API - this systems allows any mod and CC to retrieve virtually any supported information on a players' CharacterBody.<br>
      And yes, before you ask, the name <b><i>is</i></b> pun name based off of the minecraft mods 'Not/Just Enough Items' (N/J.E.I.).<br><br>
The system uses a generic interface allowing retrieval of any data from just a single method called `GetVariableFromString()`, requiring only the name of the variable, the body to target and an object of the return type. To help with finding what the type of a specific stat is (dynamically), a method exists which allows you to retrieve the type of any of the fetchable data; `GetVariableTypeFromString()`, requiring only the name of the variable and the body to target.
<br><br>
- As an alternative to `GetVariableFromString()`, you can use `GetVariableObjectFromString()` with just the variables' name, body and optionally the type if it's already known and it will return the stat in object form.<br>
      It is, however, recommended to define the type if possible as the runtime will spend much less time searching for the object.
<br><br>
- This system is planned to be extensible; meaning if you want to add a new type that can be retrieved/changed or any missed stat you can create an 'extension' mod which adds this functionality. This should be available sometime in late-beta/early-realease.
</details>

<details>
  <summary><b><a href="https://github.com/8BtS-A-to-IA/Console-Overhaul-MUT">Multi-User Targeting (M.U.T):</a></b></summary>
  
- The M.U.T system is called the "Multi-User Targeting" system - this system allows both console commands and other mods to be able to easily target multiple players' CharacterBodies with an extremely flexible targeting system.
<br><br>
Almost all statistics that a characterBody has access to can be queried against to allow accurate targeting, instead of just a user's name - anything from their health to the amount of hitboxes their current character has can be queried thanks to the T.M.I system.
<br><br>
- M.U.T. 'queries' can add to, or remove from, the list of CharacterBodies to get, allowing you to--for example--quickly target everyone but yourself with the simple query: "all&!me", which translates to "all players AND NOT the local player", or more powerfully; to target everyone with at least 10 items and not yourself: "all:itemcountany=>10&!me".<br>
    There is no (soft) limit to the amount of 'additional queries' (&s) that can be made in a single query, you can--if you're so inclined--have a query with even 100 'additional queries'.
  <br><br>
  <summary>Sadly, this is not extensible due to its complexity and there are no plans of making it extensible.</summary>
</details>

<details>
  <summary><a href="https://github.com/8BtS-A-to-IA/Console-Overhaul-TSBind">TSBind (Toggle/Simul-bind):</a></summary>
  
- The 'Binding' system is a very simple alternative system to the "SimpleMacros" mod which allows you to bind any console command (CC) to any key unity supports, this mod has no UI and is controlled entirely from the console - enabling support with any mod.
  <br><br>
- Simply bind a key by doing `COSimulBind [key] [command]` in the console then press the key when the console is closed and the CC will automatically be sent.<br>
    If the command is run multiple times with the same key, all commands defined when binding will run one after the other - all at once.
  <br><br>
You can also use `CObind [key] [command]`--similarly to `COSimulBind` when used multiple times--to preform the same action but each press will switch between calling one command then the next in the order of when it was bound, for example running `CObind p 'timescale 0'` then `CObind p 'timescale 1'` will set the timescale of the game to 0 when the <kbd>p</kbd> key is pressed then back to 1 when it is pressed again - looping back to 0 when pressed again.
  <br><br>
You can also unbind the latest bind of the respective type by calling the command with no second parameter, for example: running `COBind P` will attempt to unbind the latest command bound to the <kbd>p</kbd> key.
</details>

<details>
  <summary><b><a href="https://github.com/8BtS-A-to-IA/Console-Overhaul-BAC">Better Auto Compete (B.A.C):</a></b></summary>
  
- The B.A.C system is called the "Better Auto Complete" system; it's an alternative from "DebugToolkit" where this uses the <kbd>TAB</kbd> key to cycle through suggestions instead of the <kbd>↓</kbd> key, is extensible and gets the closest matching suggestion according to a levishtein sort.<br>
The name was made before DebugToolkit was even public...so...
  <br><br>
- This system can work seamlessly with any new CC from any mod as long as it follows the simple naming convention; in the name of the CC, have the order of identifiers be in the same order as the arguments for your CC.
  <br><br>
- If the user presses tab when there is no argument text then all items related to the identifier will be suggested in cycle--including M.U.T's "me", "all", "*", "alive", e.c.t special queries when cycling through the players if it's installed--otherwise the closest possible match will be suggested instead.
  <br><br>
- The identifiers may be any of the following: player, item, buff, equipment or team and is possible to have multiple identifiers in a single CC. This can be extended by other mods that have their own enumerable sets that their CCs can use may inject that enumerable into B.A.C. For example a mod may add a CC which only targets enemy NPCs, thus this specific CC would want to cycle through enemy NPC names/object-IDs - the mod can generate that list and inject it, along with a recognition token (a new ACRI), directly into B.A.C. allowing for *any* CC with that specific ACRI in its name to be able to cycle through the newly added enumerable.<br>
A mod can also create a 'special fill' extension where B.A.C. will only itterate through the injected enumerable on a specific set of console commands instead of the ACRI, like the CC "COBind" (from ['TSBind'](https://github.com/8BtS-A-to-IA/Console-Overhaul-TSBind)) will be the only case where all possible non-bound key-binds will be cycled through as it is specially filled to only ever run specifically on the "COBind" CC - unless changed by other mods.
</details>
</details>

<details>
  <summary>Other:</summary>
  <details>
    <summary>'not in mission' exception:</summary>
    
- When creating a new ConCommand, you can use the method `CheckIfInStage()` at the head to force players to have a stage loaded for your command to be usable.
    <br><br>
- This is particularly useful if your command requires a player or structure to be loaded.
  </details>
  <details>
    <summary>'One player targetable' exception:</summary>
- When creating multiple new ConCommands, where some use M.U.T. and some must not, you can use the method `GetPlayerBodyByName()` instead of `GetPlayerBodiesByName()`, which will attempt to retrieve just one player's CharacterBody and stop a console command if the user is trying to target multiple players - producing a warning to the player that the command is incompatible with M.U.T.
    <br><br>
- This is particularly useful for cleaning your commands up while also handling users attempting to misuse the command.
  </details>

</details>

## Installation
This mod requires [BepInEx](https://thunderstore.io/package/bbepis/BepInExPack/) to be installed.<br>
Simply extract the contents of the `CO.zip` into the `BepInEx\plugins` folder, though for the sake of simplifying the use of the [exporter helper tool (todo)]() you should create a new folder for the modpack. As the mod does not exist on the thunderstore yet, this is the only method of installation.

## Wiki
The wiki is being built.<br>
Refer to the wiki for how:
- To use the T.M.I system effectively.
- To implement M.U.T into your commands.
- To create non-inlined & inlined-extensions for B.A.C.
- Use bind directly within your mod.

and what:
- The call hierarchies of M.U.T. and inline-extensions for B.A.C are.
- The data structures the mods use.
- methods are publicly exposed and how to use them.

## Developing
[todo](https://github.com/18F/open-source-guide/blob/18f-pages/pages/making-readmes-readable.md#instructions-for-how-people-can-help)

## RoadMap
(todo)

## Legals:
- This projects [licence](LICENSE) is an MIT lisence, this means you may use the code in this project freely in commercial and non-commercial projects as long as proper accreditation is used.<br>
- [Font used in title](https://www.dafont.com/frozen-crystal.font). An awesome dontaionware font, which can be used [commercially](www.iconian.com/commercial.html) or non-commercially.<br>
- This project makes use of the [levinshtein sort](https://www.dotnetperls.com/levenshtein) for 'Better Auto Complete'.<br>

## Changelog
<details>
    <summary>V1.0.0:</summary>
</details>


## 
[alpha changelog](./Alpha%20Changelog)
