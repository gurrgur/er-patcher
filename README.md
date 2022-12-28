# Elden Ring Proton Patcher

A tool aimed at enhancing the experience when playing the game on Linux via Proton or natively on Windows. It safely patches `eldenring.exe`, that is created in a temporary subdirectory and deleted on shutdown, via hex-edits, ensuring the patched executable is run without EAC if no `--with-eac` flag is set. Use it at your own risk.

## Dependencies

- Python ≥ 3.8

## Usage

1. Copy the file `er-patcher` to the game directory.
2. Set the game's launch options to `python er-patcher ARGS -- %command%` in Steam. See [Features](#features) for available options.
  - Example: `python er-patcher --all -r 30 --disable-rune-loss -- %command%`
  - Example with [MangoHud](https://github.com/flightlessmango/MangoHud) and Wine fullscreen FSR: `python er-patcher -r 144 -uvca -- env WINE_FULLSCREEN_FSR=1 MANGOHUD=1 MANGOHUD_CONFIG=histogram %command%`
  - Example with the [Seamless Co-op](https://www.nexusmods.com/eldenring/mods/510) mod: `python er-patcher --all -x launch_elden_ring_seamlesscoop.exe -- %command%`
3. Run the game on Steam. `er-patcher` automatically runs a patched `eldenring.exe` without EAC.

Note: Some distros (like old Ubuntu versions) run Python 2 instead of 3 when running `python`. You must use `python3` in that case.

## Features

| Argument | Description |
| --- | --- |
| `-r RATE` or `--rate RATE` | Set a custom frame rate limit (default: 60). |
| `-x EXE` or `--executable EXE` | The executable to run, relative to the game's folder.<br>Mutually exclusive with `--with-eac`. |
| `--with-eac` | Run game with EAC (use it at your own risk).<br>Mutually exclusive with `--executable`. |
| `--disable-rune-loss` | Disable rune loss upon death. |
| `--all` | Enable all options but `--rate` and gameplay changes like `--disable-rune-loss`. |
| `-u` or `--ultrawide` | Remove black bars on non-16:9 aspect ratios. |
| `-v` or `--disable-vignette` | Remove the vignette. |
| `-c` or `--disable-ca` | Remove chromatic aberration. |
| `-a` or `--increase-animation-distance` | Fix low frame rate animations for distant entities or at screen edges. |
| `-s` or `--skip-intro` | Skip intro logos on startup. |
| `-f` or `--remove-60hz-fullscreen` | Remove 60 Hz lock in fullscreen (unneeded on Proton). |

## Windows support

The tool works just as well on Windows. This launch option line works if you installed Python from Microsoft Store:

`python er-patcher -r 165 --all -- %command%`

Note: It opens a Python console that closes by itself on shutdown. Use `pythonw` if you find it annoying. `python` needs to be in PATH for Windows to find it.

## References

- [DarkSouls3RemoveIntroScreens](https://github.com/bladecoding/DarkSouls3RemoveIntroScreens)
  - Intro logo skip
- [EldenRingFpsUnlockAndMore](https://github.com/uberhalit/EldenRingFpsUnlockAndMore)
  - Black bars removal
  - Custom frame rate limit
- [EldenRingMods](https://github.com/techiew/EldenRingMods) + [EldenRingFpsUnlockAndMore](https://github.com/uberhalit/EldenRingFpsUnlockAndMore)
  - Disable rune loss
- [Flawless Widescreen](https://www.flawlesswidescreen.org)
  - Animation distance increase
  - Chromatic aberration and vignette removal
