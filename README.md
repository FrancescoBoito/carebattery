# ThinkPad Battery Aliases

Two simple Bash aliases for managing laptop battery charge thresholds with [TLP](https://linrunner.de/tlp/).

Created for a **Lenovo ThinkPad L14 Gen 1 running Linux Mint**, these aliases may also work on other laptops that support charge thresholds through TLP.

## Why use charge thresholds?

Lithium-ion batteries gradually lose capacity over time. Keeping a battery at a high state of charge for extended periods, especially at high temperatures, can contribute to battery aging.

If you mostly use your laptop plugged in, limiting its charge to around **60%** can reduce the time it spends fully charged. When you need more battery life, you can temporarily charge it to **100%**.

The trade-off is that a battery limited to 60% provides less runtime if you need to unplug unexpectedly.

## What the aliases do

| Alias | Action |
| --- | --- |
| `carebat` | Sets the charging start threshold to 55% and the stop threshold to 60%. |
| `fullbat` | Temporarily allows the battery to charge to 100%. |

With `carebat` enabled, charging starts below the lower threshold and stops at the upper threshold. If the battery is already above 60%, it will not be discharged automatically.

Support and exact behavior depend on the laptop's hardware and firmware.

## Requirements

- Linux with Bash.
- [TLP](https://linrunner.de/tlp/) installed.
- A laptop that supports charge thresholds through TLP.
- A battery identified as `BAT0`.
- Administrator privileges for `sudo`.

On Linux Mint or Ubuntu, install TLP with:

```bash
sudo apt update
sudo apt install tlp
```

Check your battery information and threshold support:

```bash
sudo tlp-stat -b
```

If your battery identifier is different from `BAT0`, edit the aliases accordingly.

## Installation

Clone this repository and enter its directory:

```bash
git clone https://github.com/FrancescoBoito/thinkpad-battery-aliases.git
cd thinkpad-battery-aliases
```

Load the aliases for the current terminal session:

```bash
source battery-aliases.sh
```

To make them available automatically in future Bash sessions, add the following line to your `~/.bashrc`, replacing the example path with the actual path to the file:

```bash
source "$HOME/thinkpad-battery-aliases/battery-aliases.sh"
```

Then reload your Bash configuration:

```bash
source ~/.bashrc
```

## Usage

### Enable battery care mode

```bash
carebat
```

Sets the charging thresholds to **55–60%**. This is useful when the laptop is connected to a charger for long periods.

### Allow a full charge

```bash
fullbat
```

Temporarily allows the battery to charge to **100%**. This is useful before travelling or when you need more runtime.

### Check battery status and thresholds

```bash
sudo tlp-stat -b
```

## Persistence

The aliases are available in new Bash sessions when their file is sourced from `~/.bashrc`.

The charge thresholds set by the aliases are temporary. TLP may restore its configured thresholds when it starts or after a restart. Use `sudo tlp-stat -b` to check the active values.

To configure persistent thresholds, see the [TLP battery care documentation](https://linrunner.de/tlp/settings/bc-vendors.html).

## Notes

- These are Bash aliases that call TLP, not a standalone application.
- Charge thresholds require compatible hardware and firmware.
- The examples use `BAT0`; your battery identifier may be different.
