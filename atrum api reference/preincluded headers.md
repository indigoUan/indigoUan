> _[back to the home page](https://github.com/indigoUan/indigoUan/blob/main/atrum%20api%20reference/Modding%20with%20Atrum.md)_  
> _[back to the LUA docs](https://github.com/indigoUan/indigoUan/blob/main/atrum%20api%20reference/Atrum%20Engine%20LUA%20API%20reference.md)_
***

# Preincluded heared LUA files of Atrum Engine


## `"math"`

### `randomFloat(min:Int, max:Int)`
Returns a random floating point number of 4 digits after the point, between `min` and `max`.

### `randomBool(percent:Int)`
Returns a random bool with a `percent`% of being `true`.

## `"note_helper"`

### `getNote(id:Int, variable:String)`
Acts like `getValue` but on the note with the id `id`.

### `setNote(id:Int, variable:String, value:Any)`
Acts like `setValue` but on the note with the id `id`.

### `getUnote(id:Int, variable:String)`
Acts like `getNote` but on the unspawned note with the id `id`.

### `getUnote(id:Int, variable:String)`
Acts like `setNote` but on the unspawned note with the id `id`.

## `"flicker"`

### `flick(character:String)`
Makes `character` flicker.

## `"io"`

### `beatDuration()`
Alias for `60 / bpm`.

### `"splitString(string:String, divisor:String)"`
Returns an array od strings, splitting `string` on every `divisor`.

## `"psychify"`
As the name suggests, this just imports a bunch of aliases that allow you to use psych scripts on Atrum.  
[This is the official Psych LUA documentation](https://github.com/ShadowMario/FNF-PsychEngine/wiki/Lua-Script-API).
