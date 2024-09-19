# Vanilla Probabilities

This document covers how Pokémon Pinball: Ruby & Sapphire determines which Pokémon appear in Catch 'Em and Egg modes. Hacks in this folder may reference changes to these probabilities, so it is important that you understand how the vanilla game works.

## Before We Begin...

Various parts of this document will refer to something called the *Rayquaza trigger*. The Rayquaza trigger behaves as follows:

* The default state of the Rayquaza trigger is off.
* If you scan the Encounter Rate UP e-Reader card, the Rayquaza trigger turns on.
* If you defeat Rayquaza (catch not necessary), the Rayquaza trigger turns on.
* If you save the game while the Rayquaza trigger is on, this state is preserved in the save file, yet the Rayquaza trigger remains on.
* If you continue a game where the Rayquaza trigger was on, the Rayquaza trigger turns on.

This behavior is extremely lenient. Notably:

* If you save and start a new game, the Rayquaza trigger remains on.
* If you game over and start a new game, the Rayquaza trigger remains on.
* If you soft reset (A+B+Start+Select) and either continue or start a new game, the Rayquaza trigger remains on.

*The only way the Rayquaza trigger can be turned off is by turning the console off and on again.*

## Catch 'Em Mode

### Step 1: Super-Rare Pokémon

The game first determines whether a super-rare Pokémon will appear. For reference, the super-rare Pokémon are:

* Latias
* Latios
* Event-exclusive Pokémon
	* Chikorita
	* Cyndaquil
	* Totodile
	* Aerodactyl

First, you must have caught or evolved 5 Pokémon this game. Second, you must have 100 Pokémon registered as caught in the Pokédex. If one of these requirements is not met, the game will not spawn a super-rare Pokémon.

**NOTE: Once you register your 100th Pokémon in the Pokédex, you MUST reload the main playfield in order for super-rare Pokémon to begin appearing. This can be done by entering and exiting a bonus field, saving and continuing, or starting a new game. This restriction does NOT apply to the 5 Pokémon requirement.**

If the requirements are met, there is a 1-in-100 chance that the game will spawn a super-rare Pokémon, regardless of playfield or area. If the Rayquaza trigger is on, the chance is increased to 1-in-50.

Once the game has decided to spawn a super-rare Pokémon, it then decides which super-rare Pokémon are eligible to appear. *All super-rare Pokémon share the same 1%/2% chance to appear.* The game decides which super-rare Pokémon are eligible using Pokémon-specific criteria:

* Latias is only eligible to appear on the Sapphire playfield.
* Latios is only eligible to appear on the Ruby playfield.
* Each event-exclusive Pokémon is only eligible to appear if (a) they are registered in the Pokédex as seen or caught, or (b) you have received their Pokédex entry via link cable.

Lastly, the game decides which eligible super-rare Pokémon will appear. The game does this by selecting the first eligible Pokémon in the following list that is not registered as caught in the Pokédex:

* Latias
* Latios
* Cyndaquil
* Totodile
* Chikorita
* Aerodactyl

If all eligible Pokémon are registered as caught in the Pokédex, then the game selects an eligible Pokémon at random.

### Step 2: Everyone Else

If the game decides it will not spawn a super-rare Pokémon, it then determines which Pokémon will appear using a weighted random number generator. The algorithm is as follows:

1. For each Pokémon that could appear in this location, determine if it is a *common* or *rare* Pokémon.
2. If it is a common Pokémon, assign it a number called a *weight* as follows:
	* If you have caught 0 Pokémon this game, and this Pokémon cannot evolve, the weight is 0.
	* Else, if it and all of its evolutions are registered as caught in the Pokédex, the weight is 2.
	* Else, if you have recived via link cable the Pokédex entry for the Pokémon or any of its evolutions, the weight is 15.
	* Else, the weight is 10.
3. If it is a rare Pokémon, assign it a weight as follows:
	* If you have caught 0 Pokémon this game, the weight is 0.
	* Else, if it is registered as caught in the Pokédex, the weight is 2.
	* Else, if you have received its Pokédex entry via link cable, the weight is 2.
	* Else, the weight is 1.
4. For rare Pokémon, double its assigned weight if the Rayquaza trigger is on.
5. For each Pokémon, check if it is the last Pokémon encountered in Catch 'Em Mode. If it is, its weight is reset to 0.
6. Determine the *total weight* by adding together the weights of each Pokémon that could appear in this area.
7. The probability that a Pokémon appears is their assigned weight divided by the total weight.

*NOTE: Unlike common Pokémon, rare Pokémon ignore the Pokédex entries of their evolutions when determining their assigned weight. Pokédex entries for pre-evolutions are always ignored for determining the assigned weight.*

*NOTE: Catching a Pokémon causes the game to forget that it previously received that Pokémon's Pokédex entry via link cable. Merely seeing a Pokémon does not have this effect.*

The rare Pokémon are:

* Nosepass
* Skarmory
* Lileep
* Anorith
* Feebas
* Castform
* Kecleon
* Absol
* Wobbufet

All other Pokémon are considered common.

## Egg Mode

### Step 1: Pichu

Similar to super-rare Pokémon in Catch 'Em Mode, the game first determines whether Pichu will appear.

First, you must have caught or evolved 5 Pokémon this game. Second, the last Pokémon that hatched must not be Pichu. If one of these requirements is not met, the game will not spawn Pichu. There is no Pokédex requirement.

There is a bug with the way Pichu's probability is calculated. If the requirements are met, there is a **1-in-50** chance that the game will spawn Pichu, regardless of playfield. If the Rayquaza trigger is on, the chance is **decreased to 1-in-100**.

### Step 2: Everyone Else

Similar to Catch 'Em Mode, if the game decides it will not spawn Pichu, it then determines which Pokémon will appear using a weighted random number generator. The algorithm is identical to the one used in Catch 'Em Mode, with two exceptions:

1. Step 5 checks against the last Pokémon encountered in Egg Mode instead of Catch 'Em Mode.
2. Oddish always ignores its own Pokédex entry. Its weight is decided solely by the state of the Pokédex entry of its field-dependent evolution.

*NOTE: All Pokémon that can be encountered in Egg Mode are considered common.*

## GET Special Guests Card

In addition to the mechanism described in the Catch 'Em Mode section, there is a second way that event-exclusive Pokémon can appear. By scanning the GET Special Guests e-Reader card, the next time Catch 'Em Mode is entered, the standard algorithm is overriden with the following algorithm:

1. Select one of the four event-exclusive Pokémon at random.
2. Check if that Pokémon is registered as caught in the Pokédex. If it is not, choose that Pokémon. If it is, move to the next Pokémon in the following list, returning to the top if necessary. Repeat this step as necessary up to 4 times total.
	* Chikorita
	* Cyndaquil
	* Totodile
	* Aerodactyl
3. If all event-exclusive Pokémon are registered as caught, use the Pokémon selected in step 1.

_NOTE: The game only checks if the Pokémon is **caught**. If some but not all event-exclusive Pokémon are available to you, make sure to catch them all before scanning the e-Reader card, or else the Pokémon that appears may be one that is already available to you!_

## FAQ

### Can I encounter event-exclusive Pokémon in normal gameplay?

No. Event-exclusive Pokémon are not available in games starting from an empty Pokédex. To encounter an event-exclusive Pokémon, you must (a) use the GET Special Guests e-Reader card, (b) use a cheating device or memory editor, or \(c\) connect with another player who has already caught the event-exclusive Pokémon.

### I heard a rumor that event-exclusive Pokémon can only appear on the Ruby playfield. Is that true?

No, although you would be forgiven for thinking so. The English Pokédex entries incorrectly state that event-exclusive Pokémon can only appear on the Ruby board, but this is false.

### Can I encounter a given Pokémon twice in a row?

The only Pokémon that can appear twice in a row are the super-rare Pokémon. All other Pokémon (including Pichu) have a check to prevent them from appearing twice in a row.

### What's this about `unk12B` and `unk12C`?

`unk12B` and `unk12C` are variables which are checked when determining whether Pichu or super-rare Pokémon can spawn. If they are enabled, they bypass all other requirements, including the 1%/2% chance. However, searching through the game's code (including code not yet decompiled) does not reveal any other references to `unk12B` or `unk12C`. While we will not know for certain until the game is fully decompiled, it is extremely likely that these are debug variables that cannot be set without the use of a cheating device.

### What are you basing this information on?

This information is based on the decompilation. The relevant file is here: https://github.com/pret/pokepinballrs/blob/21a824464cf67793567e1881f41e1ca91dd2d881/src/rom_31F6C.c#L11-L619
