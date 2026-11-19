# WSSFlipperZero

Generates a Flipper Zero Sub-GHz file that pretends to be a 433 MHz weather station sensor. You set ID, channel, temperature and humidity, and the Flipper sends it to your weather station.

Based on [spoof_temp](https://github.com/rgerganov/spoof_temp) by rgerganov. The original writes raw IQ files for an SDR. This version writes a `.sub` file for the Flipper instead.

## Build

You only need a C++ compiler and make:

```bash
git clone https://github.com/d4v0l4p/WSSFlipperZero.git
cd WSSFlipperZero
make
```

## Usage

```bash
./spoof_temp -o <name> [-i ID] [-c channel] [-t temp] [-h humidity] [-f frequency]
```

| Option | Meaning | Default |
|---|---|---|
| `-o` | output file name, `.sub` is added automatically (required) | |
| `-i` | sensor ID (0-255) | 244 |
| `-c` | channel (1-3) | 1 |
| `-t` | temperature, one decimal | 26.3 |
| `-h` | humidity in % (0-100) | 20 |
| `-f` | frequency in Hz | 433920000 |

Example:

```bash
./spoof_temp -o fake_sensor -i 244 -c 1 -t 21.5 -h 45
```

That creates `fake_sensor.sub`.

## On the Flipper

1. Copy the `.sub` file to `/subghz/` on the SD card
2. Open Sub-GHz, go to Saved and pick the file
3. Send

Your station needs to be listening for the same ID and channel. Easiest way is to read the ID of your real sensor first (for example with the Flipper or rtl_433) and use that.

## License

MIT, see [LICENSE](LICENSE).
