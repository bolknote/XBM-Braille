# XBM to Braille

Convert XBM (X BitMap) images to Unicode Braille characters for terminal display.

## Example

<img width="500" height="250" src="https://github.com/user-attachments/assets/adfffc78-66ce-49ff-a780-9a2af798f273" />

## How It Works

Unicode Braille patterns (U+2800–U+28FF) form a block of 256 characters. Each character represents a 2×4 grid of dots:

```
┌───┬───┐
│ 1 │ 4 │  ← bit 0, bit 3
│ 2 │ 5 │  ← bit 1, bit 4
│ 3 │ 6 │  ← bit 2, bit 5
│ 7 │ 8 │  ← bit 6, bit 7
└───┴───┘
```

The codepoint is simply `U+2800 + dots`, where `dots` is an 8-bit value with each bit corresponding to a dot position.

The script:
1. Parses XBM file to extract width, height, and pixel data
2. Groups pixels into 2×4 blocks
3. Maps each block to the corresponding Braille character
4. Outputs UTF-8 encoded result

## Usage

```bash
./xbm2br image.xbm
```

## Sample Images

The `xbm/` folder contains example XBM files from the [ViolaWWW](https://github.com/bolknote/violawww) browser — one of the earliest web browsers (1992).

## Requirements

- Bash 3.2+
- A terminal with Unicode/UTF-8 support

## XBM Format

XBM is a simple monochrome image format using C array syntax:

```c
#define image_width 32
#define image_height 20
static char image_bits[] = {
   0xe0, 0x03, 0x00, 0x00,
   ...
};
```

Pixels are stored LSB-first (least significant bit = leftmost pixel).

## License

MIT

