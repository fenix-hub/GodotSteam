# GodotSteam for Godot Engine
Steam API for the Godot game engine (version 3.0 - 3.1). For the Windows, Linux, and Mac platforms. 

Additional flavors include: [Godot 2.x](https://github.com/Gramps/GodotSteam/tree/godot2), [Godot 2.x Minimal](https://github.com/Gramps/GodotSteam/tree/godot2-min), [Godot 3.x Minimal](https://github.com/Gramps/GodotSteam/tree/godot3-min), [Server](https://github.com/Gramps/GodotSteam/tree/server), and [GDNative](https://github.com/Gramps/GodotSteam/tree/gdnative).

Documentation
----------
Documentation is available here: https://gramps.github.io/GodotSteam/

You can also check out the Search Help section inside Godot Engine after compiling it with GodotSteam.

Current Build
----------
You can download pre-compiled versions _(currently v3.3)_ of this repo here: https://github.com/Gramps/GodotSteam/releases

**Version 3.3 Changes**

- Added: all Steam Input functions; used to be Steam Controller
- Added: all Steam Input constants
- Added: new Apps functions
- Added: missing Friends functions
- Added: missing Screenshots functions
- Added: all missing Screenshot constants
- Changed: removed Steam Controller as it is now depreciated
- Changed: split up call results and callbacks in godotsteam.h for editing ease
- Changed: user_stats_received to current_stats_received for requestCurrentStats callback / signal
- Changed: sorted Apps and Friends functions alphabetically like Steamworks Docs to find new functions easier
- Changed: getAchievementIcon; now returns the handle
- Changed: getInputTypeForHandle to output verbose controller type
- Changed: SteamInput function init to inputInit
- Changed: SteamInput function shutdown to inputShutdown
- Removed: user_achievement_icon_fetched signal / callback as it is never called

Known Issues
----------
- None... so far

Quick How-To
----------
- Download this repository and unpack it.
- Download and unpack the [Steamworks SDK](https://partner.steamgames.com); this requires a Steam developer account.
- Download and unpack the [Godot source](https://github.com/godotengine/godot); preferably 3.0.6 or 3.1.2.
- Move the following to godotsteam/sdk/:
````
    sdk/public/
    sdk/redistributable_bin/
````
- The repo's directory contents should now look like this:
````
    godotsteam/sdk/public/*
    godotsteam/sdk/redistributable_bin/*
    godotsteam/SCsub
    godotsteam/config.py
    godotsteam/godotsteam.cpp
    godotsteam/godotsteam.h
    godotsteam/register_types.cpp
    godotsteam/register_types.h
````
- Now move the "godotsteam" directory into the "modules" directory of the unpacked Godot Engine source.
- Recompile for your platform:
  - Windows ( http://docs.godotengine.org/en/stable/reference/compiling_for_windows.html )
  - Linux ( http://docs.godotengine.org/en/stable/reference/compiling_for_x11.html )
    - If using Ubuntu 16.10 or higher and having issues with PIE security in GCC, use LINKFLAGS='-no-pie' to get an executable instead of a shared library.
  - OSX ( http://docs.godotengine.org/en/stable/reference/compiling_for_osx.html )
    - When creating templates for this, please refer to this post for assistance as the documentation is a bit lacking ( http://steamcommunity.com/app/404790/discussions/0/364042703865087202/ ).
- When recompiling the engine is finished do the following before running it the first time:
  - Copy the shared library (steam_api), for your OS, from sdk/redistributable_bin/ folders to the Godot binary location (by default in the godot source /bin/ file but you can move them to a new folder).
  - Create a steam_appid.txt file with your game's app ID or 480 in this folder.  Necessary if the editor or game is run _outtside_ of Steam.

- The finished hierarchy should look like this:
  - Linux 32/64-bit
  ```
  libsteam_api.so
  steam_appid.txt
  ./godot.linux.tools.32 or ./godot.linux.tools.64
  ```
  - OSX
  ```
  libsteam_api.dylib
  steam_appid.txt
  ./godot.osx.tools.32 or ./godot.osx.tools.64
  ```
  - Windows 32-bit
  ```
  steam_api.dll
  steam_appid.txt
  ./godot.windows.tools.32.exe
  ```
  - Windows 64-bit
  ```
  steam_api64.dll
  steam_appid.txt
  ./godot.windows.tools.64.exe
  ```
- Your game must ship with the executable, Steam API DLL/SO/DyLIB, and steam_appid.txt to function. Lack of the Steam API DLL/SO/DyLib (for your respective OS) or the steam_appid.txt will cause it fail and crash.
  - **NOTE:** For OSX, the libsteam_api.dylib and steam_appid.txt must be in the Content/MacOS/ folder in your application zip or the game will crash.

From here you should be able to call various functions of Steamworks. You should be able to look up the functions in Godot itself under the search section. In addition, you should be able to read the Steamworks API documentation to see what all is available and cross-reference with GodotSteam.

Donate
-------------
Pull-requests are the best way to help the project out but you can also donate through [Patreon](https://patreon.com/coaguco) or [Paypal](https://www.paypal.me/sithlordkyle)!

License
-------------
MIT license
