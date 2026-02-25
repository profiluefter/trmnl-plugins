# My TRMNL plugins

TRMNL is software for eInk displays that can show various panels with content. I want some custom panels, and they are
in this repository. For more infos about TRMNL, see [their website](https://trmnl.com/).

These plugins were tested locally with trmnlp but mainly developed for compatibility with the TRMNL BYOS Laravel
implementation. There seems to be some differences between the two: e.g. `trmnl.user.utc_offset` seems to be a different
unit and the dom structure is enforced stricter in the Laravel version. Additionally, some liquid template errors occur
with the Laravel version that work with trmnlp.

## Plugins

Only the full layout will be designed for now. I won't use half and quarter layouts for myself, so at the moment they
will not be developed.

### JKU Menu

Status: Prototype

Shows the current menus available at JKU Mensa and KHG Mensa.

Challenges:

* very verbose menu names at JKU mensa; they don't fit on the screen
* layout that looks nice

### JKU calendar

Status: Prototype

Shows the timetable of classes at JKU. Should include also the room number.

Challenges:

* fit the names of classes into a somewhat short format; possibly with custom abbreviations for classes
* how many days to show: more than e.g. the next 3 might be too much

## Dev Setup

A devcontainer including the `trmnlp` cli tool is available. Use the devcontainer or install the tool and run
`trmnlp serve` inside the folder of the plugin you want to develop.
