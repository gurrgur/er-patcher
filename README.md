# Elden Ring Proton Patcher


A tool aimed at enhancing the experience when playing the game on linux through proton or natively on windows.

## Warning

**This tool is based on patching the game executable through hex-edits. However it is done in a safe and non-destructive way, that ensures the patched executable is never run with EAC enabled (unless explicity told to do so). Use at your own risk!**

## Dependencies

- Python >= 3.8

## Usage

1. Copy the file `er-patcher` to the game directory.
2. In steam, set the game launch options to `python er-patcher ARGS -- %command%` See [Features](#features) for available options.
  - Example:

    `python er-patcher --all --rate 30 --disable-rune-loss -- %command%`

  - Example using the [Seamless Co-op](https://www.nexusmods.com/eldenring/mods/510) mod:

    `python er-patcher --all --executable ersc_launcher.exe -- %command%`

  - Example using [MangoHud](https://github.com/flightlessmango/MangoHud) and wine fullscreen FSR:

    `python er-patcher --rate 144 -uvca -- env WINE_FULLSCREEN_FSR=1 MANGOHUD=1 MANGOHUD_CONFIG=histogram %command%`

  - Example for enabling HDR using gamescope on Linux (reported to work on Plasma 6.1):

    `ENABLE_GAMESCOPE_WSI=1 DXVK_HDR=1 gamescope -W 3440 -H 1440 -f -r 165 --hdr-enabled -- python er-patcher --all --rate 165 -- %command%`

3. Launch the game through steam. `er-patcher` automatically launches a patched version of `eldenring.exe` with EAC disabled.

Note: There might be some distros (e.g. older Ubuntu releases) that launch python 2 instead of 3 when running `python`. In that case you'll need to replace `python` with `python3` in the launch option line.

## Features

| Argument                                | Description                                                                                               |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `-r RATE` or `--rate RATE`              | Set a custom framerate limit (default: 60).                                                               |
| `-x EXE` or `--executable EXE`          | The executable to launch, relative to the games folder.<br>Mutually exclusive with `--with-eac`.          |
| `--with-eac`                            | Run game with EAC (Use it at your own risk).<br>Mutually exclusive with `--executable`.                   |
| `--disable-rune-loss`                   | Disable losing runes upon death.                                                                          |
| `--all`                                 | Enable all options except `--rate`, `--executable`, and<br>gameplay changes like `--disable-rune-loss`.   |
| `-u` or `--ultrawide`                   | Remove black bars.                                                                                        |
| `-v` or `--disable-vignette`           | Remove the vignette overlay.                                                                             |
| `-c` or `--disable-ca`                  | Disable chromatic abberation.                                                                             |
| `-a` or `--increase-animation-distance` | Fix low frame rate animations at screen<br>edges or for distant entities.                                 |
| `-s` or `--skip-intro`                  | Skip intro logos at game start.                                                                           |
| `-f` or `--remove-60hz-fullscreen`      | Remove the 60Hz limit in fullscreen<br>mode (not needed with proton).                                     |
| `--disable-camera-reset`                | Disable camera reset on target lock input when no target in frame.                                        |


## Windows Support

The patcher works just as well on windows. The following launch option line works in case you e.g. installed Python from Microsoft Store:

> `python er-patcher --rate 165 --all -- %command%`

Note: This spawns a python console which will close by itself after the game has finished running. If you find this annoying you can try using `pythonw` instead. In any case `python` needs to be in PATH for windows to find it.

Note 2: Ensure Vertical Sync is turned off for Elden Ring in Nvidia Control Panel / AMD Radeon Software / Intel Graphics Command Center, otherwise the custom framerate limit feature won't work.

## How it works

When the game is launched through steam, the tool creates a patched version of `eldenring.exe` in a temporary subdirectory while leaving the original intact. As long the flag `--with-eac` is not set, the tool modifies the steam launch command to launch the patched executable instead of `start_protected_game.exe`, thefore ensuring that the patched exe is never run with EAC enabled. After the game is closed, the patched executable is removed.

## Credits

- [EldenRingFpsUnlockAndMore](https://github.com/uberhalit/EldenRingFpsUnlockAndMore)
  - frame time limit adjustment
  - black bar removal
- [Flawless Widescreen](https://www.flawlesswidescreen.org)
  - vignette and ca removal
  - animation distance increase
- [DarkSouls3RemoveIntroScreens](https://github.com/bladecoding/DarkSouls3RemoveIntroScreens): intro logo skip
- [EldenRingMods](https://github.com/techiew/EldenRingMods) + [EldenRingFpsUnlockAndMore](https://github.com/uberhalit/EldenRingFpsUnlockAndMore)
  - disable rune loss
  - disable camera reset
