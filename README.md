# Elden Ring Proton Patcher


A tool aimed at enhancing the experience when playing the game on linux through proton or natively on windows.

## Warning

**This tool is based on patching the game executable through hex-edits. However it is done in a safe and non-destructive way, that ensures the patched executable is never run with EAC enabled. Use at your own risk!** 

## Features

- set custom frame rate limits (e.g. 30, 90, 165, ...)
- remove black borders when using resolutions with an aspect ratio other than 16:9 (e.g. ultrawide).
- remove vigniette overlay
- remove chromatic abberation filter
- increase animation distance / fix choppy animations at screen edges
- remove 60hz limit when using fullscreen mode

## Dependencies

- Python >= 3.9 

## Usage

1. Copy the file `er-patcher` to the game directory.
2. In steam, set the game launch options to `./er-patcher ARGS -- %command%` where ARGS is replaced with a combination of
  - `-r RATE` or `--rate RATE` for setting a custom framerate cap (default: 60)
  - `-u` or `--ultrawide` for removing black bars
  - `-v` or `--disable-vigniette` for removing the vigniette overlay
  - `-c` or `--disable-ca` for disabling chromatic abberation
  - `-a` or `--increase-animation-distance` for fixing low frame rate animations at screen edges or for distant entities.
  - `-f` or `--remove-60hz-fullscreen` for removing the 60Hz limit in fullscreen mode (only applies to windows and has no effect when running the game through proton due to fshack) 
  - Example: `./er-patcher --rate 30 -uavc -- %command%`
  - Example with mangohud and wine fullscreen fsr: `./er-patcher --rate 144 -uvca -- env WINE_FULLSCREEN_FSR=1 MANGOHUD=1 MANGOHUD_CONFIG=histogram %command%`
3. Launch the game through steam. `er-patcher` automatically launches a patched version of `eldenring.exe` with EAC disabled.

### Windows

It also work just as well on windows. The only difference is, that you need to run the script via your Python 3 installation. The following launch option line works in case you installed Python from Microsoft Store:

> `python er-patcher --rate 165 -uvcaf -- %command%`

Note: This spawns a python console which will close by itself after the game has finished running. If you find this annoying you can try using `pythonw` instead. In any case `python` needs to be in PATH for windows to find it.

## How it works

When the game is launched through steam, the tool creates a patched version of `eldenring.exe` in a temporary subdirectory while leaving the original intact. The tool then modifies the steam launch command to launch the patched executable instead of `start_protected_game.exe`. This ensures that the patched exe is never run with EAC enabled. After the game is closed, the patched executable is removed.

## Credits

- [EldenRingFpsUnlockAndMore](https://github.com/uberhalit/EldenRingFpsUnlockAndMore)
  - frame time limit adjustment
  - black bar removal
- [Flawless Widescreen](https://www.flawlesswidescreen.org)
  - vigniette and ca removal
  - animation distance increase
