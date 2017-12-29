# Southclaw's Simple Map Parser

Loads .map files populated with CreateObject (or any variation) lines, supports materials and text.

Default load directory: `./scriptfiles/Maps/`

## Installation

Simply install to your project:

```bash
sampctl package install Southclaws/samp-object-loader
```

Include in your code and begin using the library:

```pawn
#include <object-loader>
```

## Supported Syntax

### Objects

```pawn
CreateObject(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0);
CreateDynamicObject(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0);
```

Any string starting with 'Create' is parsed as a CreateObject line, this is also valid:

```pawn
CreateCake(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0);
```

### Object Materials

```pawn
CreateObject(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0);
SetObjectMaterial(object, 0, 18837, "mickeytextures", "ws_gayflag1", 0);
```

Any `SetObjectMaterial` or `SetObjectMaterialText` line will affect the last created object. The first parameter (`objectid`) is ignored and can be any string for flexibility.

### Object Removal

```pawn
RemoveBuildingForPlayer(playerid, 615, 0.0, 0.0, 0.0, 200.0);
```

'playerid' is ignored, but still valid to allow flexibility when copying from .pwn source code.

When a player connects (or when the filterscript loads, whichever comes first) a list of removed buildings is built and saved for that player.

If the filterscript reloads (perhaps to load an update to object data) any RemoveBuilding instructions that have already been called for each player are ignored. When a player disconnects, their data is discarded.

This data is stored in binary format in `./scriptfiles/Maps/session/`

### Options

Custom 'function' for altering world, interior and stream distance. This updates the settings for the current file, any lines below this will use these settings when creating objects. This function can be used multiple times.

```pawn
options(world, interior, stream distance)
```

For example, to make all the objects after this line create in world 0, interior 1 and a stream distance of 300:

```pawn
options(0, 1, 300)
```

### Comments

Single line `//` comments are supported at the end of lines or on their own.

```pawn
// comment
options(0, 1, 200) // comment
CreateObject(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0); // comment
```

## Debugging

Create a file inside './scriptfiles/Maps/' called 'maps.cfg'
Use debug option followed by level parameter to make the script load with debug
mode enabled. Each 'level' of debugging offers different information:

* `-d0` = Print information messages
* `-d1` = Print each folder
* `-d2` = Print each loaded file
* `-d3` = Print each loaded data line in each file
* `-d4` = Print each line in each file

## Testing

To test, simply run the package:

```bash
sampctl package run
```

And connect to `localhost:7777` to test.
