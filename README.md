# Dark Souls 3 Patcher
A tool aimed at enhancing the experience when playing the game by patching the executable so you don't need to mess with .dlls.

> This Programm fully supports Linux/Wine

## Features
- custom resolution (Basically allows you to use fullscreen on not supported aspect ratios)
- skip intro logos
- fix camera (disables the camera reset when trying to lock-on with no target in range)

> All features are Tested with Dark Souls 3 version 1.15.2

> working with and without all the DLCs

## Dependencies
- Python >= 3.8

## Usage

1. Copy the file `ds3-patcher` to the game directory or specify the path to the game via the `--gamepath` option.
2. In steam, set the game launch options to `python ds3-patcher ARGS -- %command%` or use permanent patch option. See [Features](#features) for available options.
  - Example for the Steam Deck for one (permanent) patch:

    `python ds3-patcher --all -p`
    
  - Example:

    `python ds3-patcher --all -- %command%`

  - Example using [MangoHud](https://github.com/flightlessmango/MangoHud) and wine fullscreen FSR:

    `python ds3-patcher -all -res 1280x800 -- env WINE_FULLSCREEN_FSR=1 MANGOHUD=1 MANGOHUD_CONFIG=histogram %command%`

  - Example for enabling HDR using gamescope on Linux (reported to work on Plasma 6.1):

    `ENABLE_GAMESCOPE_WSI=1 DXVK_HDR=1 gamescope -W 3440 -H 1440 -f -r 60 --hdr-enabled -- python ds3-patcher --all -- %command%`
    
3. Launch the game through steam. `ds3-patcher` automatically launches a patched version of `DarkSoulsIII.exe`.

Note: There might be some distros (e.g. older Ubuntu releases) that launch python 2 instead of 3 when running `python`. In that case you'll need to replace `python` with `python3` in the launch option line. 

## Troubleshooting
If you have issues, verify your game files and make sure that no other patch is applied to Elden Ring.

## Options

| Argument                                | Description                                                                                               |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `-x EXE` or `--executable EXE`          | The executable to launch, relative to the games folder. Mutually exclusive with `--with-eac`.             |
| `--all`                                 | Enable all options.                                                                                       |
| `-res` or `--resolution`                | Set a custom resolution.                                                                                  |
| `-s` or `--skip-intro`                  | Skip intro logos at game start.                                                                           |
| `-p` or `--permanent`                   | Make the patches permanent.                                                                               |
| `-e` or `--player-camera`               | Always center camera to player.                                                                           |
| `-y` or `--fix-camera`                  | Disables the camera reset when trying to lock-on with no target in range.                                 |
| `-g path/to/game` or `--gamepath path/to/game`| Specify path to game.                                                                               |

## Windows Support

The patcher works just as well on windows. The following launch option line works in case you e.g. installed Python from Microsoft Store:

> `python ds3-patcher --all -- %command%`

Note: This spawns a python console which will close by itself after the game has finished running. If you find this annoying you can try using `pythonw` instead. In any case `python` needs to be in PATH for windows to find it.

## How it works

When the game is launched through steam, the tool creates a patched version of `DarkSoulsIII.exe` in a temporary subdirectory while leaving the original intact. After the game is closed, the patched executable is removed.

## Credits
- [er-patcher](https://github.com/gurrgur/er-patcher) by gurrgur, they did the most work, I just changed some things in their project
- [DarkSouls3RemoveIntroScreens](https://github.com/bladecoding/DarkSouls3RemoveIntroScreens): intro logo skip
- [ds3-uw](https://github.com/JRWickham/ds3-uw) + [WSGF](https://www.wsgf.org/dr/dark-souls-iii/en)
  - Resolution change
- [Fix camera](https://www.nexusmods.com/darksouls3/mods/142)
- let me know if I forgot your contribution
