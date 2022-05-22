_[home](https://github.com/indigoUan/indigoUan/blob/main/atrum%20api%20reference/Modding%20with%20Atrum.md)_
# Atrum (aka Atro) Engine LUA API reference
[Official LUA documentation](http://www.lua.org/docs.html)  
[Official LUA 5.1 (used in Atrum) documentation](http://www.lua.org/manual/5.1/)
***
***

# # commands
\# commands are lines that get read once when the script is opened by the game:

## `#include: "header_here" "other_header_here" [...]`
This command takes the script in the scripts folder that has the given name; these are called "headers".  
You can load as many as you want.

## `#ignore_cin: function_here another_function_here [...]`
This command will have the game NOT call the functions you listed: only the script itself can call them. (You could also make those functions `local` instead)  
You can set as many as you want.

## `#ignore_cout: function_here another_function_here [...]`
This command will have the script call the functions you listed ONLY FROM ITSELF, and not from the game. (E.G. if you put `setValue`, the script will not call the game-given `setValue` funciton, but will instead call the one determined in the script)  
You can set as many as you want.

## `#tick_length: time_in_seconds`
This command sets the initial tick length. You can later change it calling `changeTickLength(time_in_seconds)`.  
Every tick the function `tick(tick_count, tick_length)` is called.

***

# Variables
Variables that are always available no matter what.

## `bpm:Int`_todo: make it a float_
The current BPM of the song.  
`60 / bpm` returns the duration in seconds of a beat.

## `curStep:Int`
The current step count.  
A step lasts a quarter of a beat.

## `curBeat:Int`
The current beat count.  
A beat lasts 60 / bpm of the song.

***

# Callbacks
These are funcitons embedded in the game that you can call from the script. (`#ignore_cout` afflicts these)

## `broadcast(name:String, argument:Any)`
This function calls `name` functions in all loaded scripts, with `argument` as the only argument.

## `controlPress(name:String)`; `controlHold(name:String)`; `controlLift(name:String)`
They check whether or not `name` control has been pressed/held/released.

These are the only possible names:
* `"left"`
* `"down"`
* `"up"`
* `"right"`
* `"accept"` (only `controlPress`)
* `"back"` (only `controlPress`).  
And anything else will return `false`.

## `keyPress(name:String)`; `keyHold(name:String)`; `keyLift(name:String)`
They check `FlxG.keys.(justPressed/pressed/justReleased)."name"`.  
[These](https://github.com/indigoUan/indigoUan/blob/main/atrum%20api%20reference/all%20keys.md) are all the possible key names.

## `changeTickLength(duration_in_seconds:Float)`
Changes the duration of a tick.

## `setSave(name:String, value:Any)`
Saves `value` to `name`.  
You can use it to overwrite options too.

## `getSave(name:String)`
Returns the value of `name`.  
You can use it to read options too.

## `flushSaves`
Writes the cached save data onto the internal storage, to prevent loss of it.

## `setValue(class:String, name:String, value:Any)`
Sets the variable `name` in the class `class` to `value`.  
If `class` is `"game"` or `""`, the game will set the public variables of PlayState.

## `getValue(class:String, name:String)`
Returns the value of the variable `name` in the class `class`.  
If `class` is `"game"` or `""`, the game will get the public variables of PlayState.

## `setValueToGroup(class:String, group:String, id:Int, variable:String, value:Any)`
Sets the variable `variable` of the value at `id` of the `group` array in the class `class` to `value`.  
If `class` is `"game"` or `""`, the game will set the public variables of PlayState.

## `getValueFromGroup(class:String, group:String, id:Int, variable:String)`
Returns the value of the variable `variable` of the value at `id` of the `group` array in the class `class`.  
If `class` is `"game"` or `""`, the game will set the public variables of PlayState.

## `tween` _WiP_
Unfinished

## `cancelTween` _WiP_
Unfinished

## `timer(tag:String, duration:Float, loops:Int)`
Runs a timer named `tag` for `duration` seconds `loops` times.  
When it completes, it calls `timerCompleted(tag, elapsedLoops)`.

## `cancelTimer(tag:String)`
Cancels the timer named `tag`.

No questions there.

## `newSprite(tag:String, imagePath:String, X:Float, Y:Float, antialiasing:Bool)`
Creates a new sprite at `X` and `Y`, loading the texture named `imagePath` in the images folder.

## `addSprite(tag:String)`
Adds `tag` sprite to the current PlayState instance.

## `setScrollFactor(tag:String, X:Float, Y:Float)`
Sets the scroll factor of the `tag` sprite to (`X`; `Y`).

## `scale(tag:String, X:Float, Y:Float)`
Sets the scale value of the `tag` sprite to (`X`; `Y`).

## `setGraphicSixe(tag:String, Width:Int, Height:Int)`
Sets the size of the `tag` sprite to (`X`; `Y`) pixel-perfectly.

## `updateHitbox(tag:String)`
Updates the hitbox of the `tag` sprite.

## `playAnim(obj:String, name:String, forced:Bool, reversed:Bool, startingFrame:Int)`
Self explenatory.

## `charPlayAnim(char:String, name:String, forced:Bool, reversed:Bool, startingFrame:Int)`
Also self explenatory.

## `missAnim(direction:Int)`
Plays the miss animation in the given direction.

## `missNote(id:Int)`
Causes the note at position `id` to be missed.

## `tohex(num:Int)`
Returns a string which contains the base-sixteen equivalent of the given base-ten number `num`.

## `fromhex(hex:String)`
Returns an integer which contains the base-ten equivalent of the given base-sixteen number `hex`.

## `fromRGB(r:Int, g:Int, b:Int)`
Returns an integer which contains the base-ten equivalent of the given numbers mixed into one hexadecimal number.

## `roundDecimal(num:Float, quantity:Int)`
Returns `num` but every digit past `quantity` after the point has been removed.

## `warn(title:String, content:Any)`
Creates a system dialog box giving one single message.

## `super_throw(error:String)`
Throws.

***

# Functions
These are the funcitons that the game calls from the script. (`#ignore_cin` afflicts these)

## `main()`
The initial function that gets called before the game starts loading other assets.

## `create()`
Called after some assets are loaded.

## `createPost()`
Called ones the creation of the state finishes.

## `update(elapsed:Float)`
Called every time a new frame pops in.  
`elapsed` is how much time in seconds has passed since the previous frame.

## `updatePost(elapsed:Float)`
Called every time a new frame is about to pop out.  
`elapsed` is how much time in seconds has passed since the previous frame.

## `stepHit(step:Int)`
Called when a new step hits.  
`step` is the equivalent of `curStep`.

## `stepHitPost(step:Int)`
Called when a new step finishes.  
`step` is the equivalent of `curStep`.

## `beatHit(beat:Int)`
Called when a new beat hits.  
`beat` is the equivalent of `curBeat`.

## `beatHitPost(beat:Int)`
Called when a new beat finishes.  
`beat` is the equivalent of `curBeat`.
