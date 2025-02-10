# Pokémon Pinball: Ruby & Sapphire Speedchoice

As with other "speedchoice" ROM hacks, Pokémon Pinball: Ruby & Sapphire Speedchoice is a hack designed to make the game more speedrun-friendly. Specifically, this hack is designed to drastically reduce the amount of time necessary for the "Complete Pokédex" category.

Pokémon Pinball: Ruby & Sapphire Speedchoice is currently a half-decompilation, half-binary hack. As PinballRS decompilation progresses, it will transition to a fully decompilation-based hack.

## Features

### Reduced Interaction Counts

- Pokémon only take 1 hit to catch
  - Pokémon still take 3 bumper hits to reveal in Catch'Em mode
  - Jirachi still takes 3 hits to catch
- After exiting Catch'Em mode, 1 GET light will remain illuminated
- Pokémon only require 1 EXP to evolve
- After exiting EVO mode, 1 EVO light will remain illuminated
- The number of interactions required to hatch eggs has been reduced
  - On the Ruby field, eggs now only take 3 interactions to hatch
  - On the Sapphire field, eggs now only take 2 interactions to hatch
  - As in vanilla, the first egg of each game starts with one interaction

### Adjusted Probabilities

- The Pichu spawn rate bug has been fixed: Pichu now has a 1% probability to hatch *before* defeating Rayquaza, and 2% *after* defeating Rayquaza
- The probability of encountering duplicate Pokémon is significantly reduced
  - A Pokémon is considered a duplicate if it and all of its evolutions are registered as caught in the Pokédex

More detailed information on probability adjustments can be found in CHANGELOG.md.

## Download

To download the patch file for this hack, click on the bps file above, then click the "Download raw file" button. It looks like this: ![image](https://github.com/user-attachments/assets/96a892a8-794f-490c-8a4b-447175de8e53)
