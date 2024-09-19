# Changelog

## Version 0.0.1 - Released 2024-09-19

* Adjusted Pokémon spawn probabilities.
	* Pichu now appears 1% of the time when the Rayquaza trigger is off, and 2% of the time when the Rayquaza trigger is on.
	* Pokémon no longer consider whether Pokédex entries were received via link cable when determining weights.
	* Rare Pokémon now consider their evolutions when determining weights.
	* Weights have been updated:

| Category | Before being caught | After being caught |
|---|---|---|
| Common | 9100 | 1 |
| Rare (Rayquaza trigger off) | 910 | 1 |
| Rare (Rayquaza trigger on) | 1820 | 1 |
| Egg | 2621 | 1 |

	
* Reduced interactions required to encounter Pokémon.
	* After exiting Catch 'Em Mode, 1 GET arrow will remain lit.
	* After exiting Evo Mode, 1 EVO arrow will remain lit.
		* The game still starts with 0 EVO arrows lit.
	* On the Sapphire playfield, hatching an egg now only requires 2 interactions.
		* The first egg of the game only requires 1 interaction.
	* On the Ruby playfield, hatching an egg now only requires 3 interactions.
		* The first egg of the game only requires 2 interactions.
* Reduced interactions required to catch or evolve Pokémon.
	* In both Catch 'Em and Egg Modes, Pokémon now only require 1 hit to catch.
	* In Evo Mode, Pokémon now only require 1 EXP/stone/etc. to evolve.

Important notes:
* For design reasons, bonus stages have not been altered.
* For design reasons, the number of hits required to catch Jirachi has not been changed.
* For technical reasons, it is not currently possible to start the game with 1 EVO arrow lit.
* For technical reasons, it is not currently possible to reduce the number of interactions required to hatch an Egg on the Ruby playfield to 2.
* For technical reasons, it is not currently possible to reduce the number of bumper hits required to reveal the Pokémon in Catch 'Em mode.
* For technical reasons, it is not currently possible to speed up or eliminate animations.
