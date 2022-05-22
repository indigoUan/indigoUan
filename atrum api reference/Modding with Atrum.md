# Modding with Atrum (home page)

This engine has a great amount of moddable features, which range from custom stages, to custom ratings.  
In this reference I will go over:
* Installing a mod
* Changing the options
* Changing rating timings
* Custom script on note hit
* LUA

## Installing a mod
Much like the renowned Psych Engine, Atrum supports "mod folders", essentially you just put a folder in the `mods/` folder of the game, and it just kinda works.  
For now only the folder `default/` works.

## Changing the options
In the `assets/` folder there are `options.json` and `options.lua`.

The first one contains the tabs; the options (`"name also used for saving"`, `"description"`, `"tab"`, `initial_value`); and the eventual "meta data" for options that aren't just `true`/`false`.

The second one reads every option when it gets changed, and acts accordingly.

## Changing rating timings
When you hit a note and the game spawns a "Sick!!" or a "Good!" and so on... that's called a rating, and this engine has completely customizable rating timings.

First you need to go to `assets/rating/` and open the file `milliseconds.json`.  
In here you will see two variables: `default_set_used` and `sets`: `default_set_used` indicates which set in the `sets` variable should be used by the game.  
Each array in `default_set_used` indicates specific milliseconds for each rating (Marvelous, Sick, Good, Bad, Shit, Miss).

## Custom script on note hit
In the folder `assets/rating/` there is the file `logics.lua`, which contains a funciton that reads the rating (Marvelous, Sick, Good, Bad, Shit, Miss), and runs a piece of script accordingly (increasing health, score, missing...).

## LUA
You can find the full API reference [here](https://github.com/indigoUan/indigoUan/blob/main/atrum%20api%20reference/Atrum%20Engine%20LUA%20API%20reference.md).

When the game starts a song, all LUA files in the `scripts/` folder and `modchart.lua` in the song chart folder get loaded, and the `main` function is called on all of them.
