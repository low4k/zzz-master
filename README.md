# zzz

<p>
	<b>Animated truecolor ASCII for your terminal.</b><br/>
	Render image frames once, then play them back fast.
</p>

<p>
	<img alt="python" src="https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white" />
	<img alt="rock" src="https://img.shields.io/badge/Runtime-Rock-0E1117?style=flat-square" />
	<img alt="format" src="https://img.shields.io/badge/Format-.zzz-0B8F4D?style=flat-square" />
	<img alt="color" src="https://img.shields.io/badge/Color-24--bit%20ANSI-F28C28?style=flat-square" />
</p>

<p>
	<span style="color:#0B8F4D;"><b>render</b></span> ->
	<span style="color:#F28C28;"><b>store</b></span> ->
	<span style="color:#1F6FEB;"><b>play</b></span>
</p>

## Quick Start

```bash
zzz render in.png out.zzz
zzz play out.zzz
zzz loop out.zzz
```

## What It Does

1. Loads an image (GIF/APNG/static).
2. Splits into frames and optionally removes background (chroma key).
3. Converts pixels into block characters plus 24-bit ANSI colors.
4. Writes pre-rendered frames to a plain-text `.zzz` file.
5. Plays frames in terminal at source timing (or forced FPS).

`.zzz` is optimized for playback speed: precomputed ANSI means playback is mostly read, print, and sleep.

## Install

Requires Python 3, Pillow, and Rock.

```bash
pip install Pillow
```

Run from this checkout with `./zzz` (Linux/macOS) or via Rock directly on Windows.

## Usage

```text
zzz render <image> <out.zzz> [-w 90] [-H 36] [-t 180] [--keep-bg] [--bg R,G,B]
zzz play   <file.zzz> [loops] [fps]
zzz loop   <file.zzz>
zzz pin    <file.zzz> <row> <col> [loops] [fps]
zzz info   <file.zzz>
```

## Render Flags

- `-w`, `-H`: output width and max height in terminal cells (default `90x36`)
- `-t`: chroma-key tolerance (default `180`)
- `--keep-bg`: disable background removal
- `--bg R,G,B`: force background color instead of corner sampling

## Playback Notes

- `loops` defaults to `1`; use `0` for infinite loop
- `fps` overrides source timing
- parser is newline-safe (`LF` and `CRLF` both supported)

## .zzz File Format

```text
ZZZ1
{"v":2,"src":"input.png","w":90,"h":36,"rh":36,"fps":12,"frames":1,"delays_ms":[80],"bg_removed":true}
\x1eFRAME
<ansi frame>
\x1eEND
```

## Tips For Better Output

- Use a dark terminal theme for stronger contrast.
- Keep source subject centered before rendering.
- If edge fringing appears, tune `-t` or set explicit `--bg`.
- For clean still images, PNG with transparency usually works best.
