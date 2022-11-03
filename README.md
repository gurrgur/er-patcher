# Elden Ring Proton Patcher
Elden Ring enhancement patches (custom frame rate limits, ultrawide support etc.) seamlessly integrated with Steam.

Elden Ring Proton Patcher aims to enhance the experience when playing the game on Linux via Proton and Windows. It safely patches `eldenring.exe`, that is created in a temporary subdirectory and deleted on shutdown, via hex-edits, ensuring the patched executable is not run with EAC if no `--with-eac` flag is set. Use it at your own risk.

## Dependencies
- Python ≥ 3.8

## Windows support
The tool works just as well on Windows. This launch option line works if you installed Python from Microsoft Store:
```
python er-patcher --all -r 75 -- %command%
```
Note: It opens a Python console that closes by itself on shutdown.  Use `pythonw` if you find it annoying. `python` needs to be in PATH for Windows to find it.

## Usage
1. Copy the file `er-patcher` to the game directory.
2. Set the game's launch options to `python er-patcher ARGS -- %command%` in Steam. See [Features](#features) for available options.
  - Example: `python er-patcher --all -l -r 90 -- %command%`
  - Example with [MangoHud](https://github.com/flightlessmango/MangoHud) and Wine fullscreen FSR: `python er-patcher -acvu -r 144 -- env WINE_FULLSCREEN_FSR=1 MANGOHUD=1 MANGOHUD_CONFIG=histogram %command%`
  - Example with the [Seamless Co-op](https://www.nexusmods.com/eldenring/mods/510) mod: `python er-patcher --all -x launch_elden_ring_seamlesscoop.exe -- %command%`
3. Run the game on Steam. `er-patcher` automatically runs a patched `eldenring.exe` without EAC.

Note: Some distros (e.g., old Ubuntu versions) run Python 2 instead of 3 when running `python`. You will need to use `python3` in that case.
 
## Features
| Argument | Description |
| --- | --- |
| `--all` | Enable all options but `--rate` and gameplay changes like `--disable-rune-loss`. |
| `-l` or `--disable-rune-loss` | Disable rune loss on death. |
| `-x EXE` or `--executable EXE` | Set the executable to run, relative to the game's folder. Mutually exclusive with `--with-eac`. |
| `-a` or `--increase-animation-distance` | Fix low frame rate animations for distant entities or at screen edges. |
| `-r RATE` or `--rate RATE` | Set a custom frame rate limit (default: 60). |
| `-f` or `--remove-60-hz-fullscreen` | Remove 60 Hz lock in fullscreen (unneeded in Proton). |
| `-c` or `--remove-ca` | Remove chromatic aberration. |
| `-v` or `--remove-vignette` | Remove the vignette. |
| `-s` or `--skip-intro` | Skip intro logos on startup. |
| `-u` or `--ultrawide` | Remove black bars in non 16:9 screens. |
| `--with-eac` | Run the game with EAC (use it at your own risk). Mutually exclusive with `--executable |

## References
- [DarkSouls3RemoveIntroScreens](https://github.com/bladecoding/DarkSouls3RemoveIntroScreens) - Intro logo skip
- [EldenRingFpsUnlockAndMore](https://github.com/uberhalit/EldenRingFpsUnlockAndMore) - Black bars removal and custom frame rate limit
- [EldenRingMods](https://github.com/techiew/EldenRingMods) and [EldenRingFpsUnlockAndMore](https://github.com/uberhalit/EldenRingFpsUnlockAndMore) - Disable rune loss
- [Flawless Widescreen](https://www.flawlesswidescreen.org) - Animation distance increase and chromatic aberration and vignette removal
