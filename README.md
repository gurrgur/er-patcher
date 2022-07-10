# Elden Ring Proton Patcher
A tool aimed at enhancing the experience when playing the game on Linux through Proton or natively on Windows.
## Warning
**It is based on patching the game executable through hex-edits, but it is done safely & non-destructively, ensuring the patched executable is never run with EAC enabled (unless explicity told to do so). Use it at your own risk!**
## Dependencies
- Python ≥ 3.8
## Usage
1. Copy the file `er-patcher` to the game directory.
2. Set the game launch options to `python er-patcher ARGS -- %command%` in Steam. See [Features](#features) for available options.
- Example: `python er-patcher --all --rate 30 --fix-camera -- %command%`
- Example using [MangoHud](https://github.com/flightlessmango/MangoHud) & Wine fullscreen FSR: `python er-patcher --rate 144 -uvca -- env WINE_FULLSCREEN_FSR=1 MANGOHUD=1 MANGOHUD_CONFIG=histogram %command%`
3. Launch the game with Steam. `er-patcher` automatically launches a patched `eldenring.exe` version with EAC disabled.

Note: There might be some distros (older Ubuntu releases e.g.) that launch python 2 instead of 3 when running `python`. You will need to replace `python` by `python3` in the launch option line in that case.  
## Features
| Argument                                | Description                                                                     |
| --------------------------------------- | ------------------------------------------------------------------------------- |
| `--all`                                 | Enable all options but `--rate` &<br>gameplay changes, like `--fix-camera`.      |
| `--fix-camera`                           | Remove camera auto-rotation.                                                    |
| `-r RATE` or `--rate RATE`              | Set a custom frame rate limit (default: 60).                                    |
| `--with-eac`                            | Run game with EAC (Use it at your own risk).                                    |
| `-u` or `--ultrawide`                   | Remove black bars.                                                              |
| `-v` or `--disable-vignette`            | Remove the vignette overlay.                                                    |
| `-c` or `--disable-ca`                  | Remove chromatic aberration.                                                    |
| `-a` or `--increase-animation-distance` | Fix low frame rate animations at screen<br>edges or for distant entities.       |
| `-s` or `--skip-intro`                  | Skip intro logos on startup.                                                    |
| `-f` or `--remove-60hz-fullscreen`      | Remove the 60 Hz limit in fullscreen<br>mode (unneeded with Proton).            |
## Windows support
It works on Windows as well. The following launch option line works in case you installed Python from Microsoft Store, e.g.:
> `python er-patcher --rate 165 --all -- %command%`

Note: It spawns a python console which will close by itself after the game has stopped running. You can try using `pythonw` instead if you find it annoying. `python` needs to be in PATH for Windows to find it in any case.
## How it works
It creates a patched  `eldenring.exe` version in a temporary subdirectory while leaving the original intact when the game is launched with Steam. It modifies Steam's launch command to launch the patched executable instead of `start_protected_game.exe` if the flag `--with-eac` is not set, thefore ensuring that the patched exe is never run with EAC enabled. The patched executable is removed after the game is closed.
## Credits
- [EldenRingFpsUnlockAndMore](https://github.com/uberhalit/EldenRingFpsUnlockAndMore)
  - Frame time limit adjustment
  - Black bar removal
- [Flawless Widescreen](https://www.flawlesswidescreen.org)
  - Vignette & ca removal
  - Animation distance increase
- [DarkSouls3RemoveIntroScreens](https://github.com/bladecoding/DarkSouls3RemoveIntroScreens): intro logo skip
- [EldenRingMods](https://github.com/techiew/EldenRingMods) + [EldenRingFpsUnlockAndMore](https://github.com/uberhalit/EldenRingFpsUnlockAndMore): camera fix
