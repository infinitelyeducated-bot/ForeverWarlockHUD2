<p align="center"><img src="media/banner.jpg" alt="Warlock header art" width="100%"></p>

<img src="media/crest.png" alt="Warlock crest" width="96" align="left">

# ForeverWarlockHUD2

A warlock HUD for **World of Warcraft: Forever** (Interface 16001). This is the "2" build: everything in [ForeverWarlockHUD](../../../ForeverWarlockHUD) plus text fonts and formats, player / target / target-of-target frames and minimap options.

<br clear="left">

> **Status: version 2.0.0, not yet verified in the game client.** It passes a mocked-client test
> suite and boots cleanly in a simulated UI, but nobody has confirmed it in the real game. Expect
> rough edges and please report them.

## Install

1. Download this repository (Code -> Download ZIP) or clone it.
2. Put the folder in `World of Warcraft/_forever_/Interface/AddOns/` and make sure it is named exactly `ForeverWarlockHUD2`.
3. Restart the game or `/reload`. Type `/fwl2` to open the menu.

**It only starts on a warlock.** On a character of any other class it stays completely off: nothing
on screen, no events, nothing saved, and `/fwl2` just says which class it is for. So you can
leave every class's HUD enabled and only the right one runs.

Optional companions (the HUD works without them):
- **ForeverArt** - menu artwork: a painted backdrop, a header picture and a class crest.
- **ForeverFonts** - extra typefaces for the Text options.

Do not enable `ForeverWarlockHUD` at the same time: you would get two HUDs.

## How you use it

Open the menu with `/fwl2`. **While the menu is open** (and Lock is off), point at any bar or icon:

| Do this | Result |
|---|---|
| Hold **CTRL**, then hold the **left** mouse button | The item sticks to the cursor until you let go |
| Hold **CTRL** and roll the **mouse wheel** | Bigger or smaller |
| Hold **CTRL**, then hold the **right** mouse button and drag | Turns the item; it stays as you leave it |
| **Double-click the right** mouse button | Back to its original orientation |

Icons turn to any angle. Bars and the recent-actions row turn in quarter turns, because the
client cannot draw a status bar at an angle. With the menu closed nothing can be clicked or moved.
Because the mouse does all of this, the menu has no position, scale or orientation controls.
The **Help** tab in the menu explains all of it in game.

## What it shows

- **Mana bar** - mana. Its number has its own on/off switch.
- **Regeneration bar** - what is actually arriving per second.
- **Swing timer** - with its own Show switch, colour, spark, text mode, ticks and ready flash.
- **Combo points** - present but off by default; this class has none.
- **Recent actions** - the last four spells you cast, newest first.
- **Ability icons** - 33 abilities, switched on one by one. On cooldown an icon goes dark and
  grey, a clock sweep runs round it, and the time left counts down to the hundredth of a second in
  its bottom-right corner, drawn above everything else. It also flashes when ready, glows while its
  effect is on you, and dims or turns red when you cannot use it. Every one of these has a switch.
- **Unit frames** - player, target and target-of-target, with cast bar, buffs and debuffs. Opening
  the menu puts all three on screen (switched-off ones dimmed) so each can be moved and sized.
- **Text** - typeface, size, place and number format for each text, beside the thing it labels.
- **Map** - minimap shape, size and clutter.

On by default: Death Coil, Howl of Terror, Soul Fire, Shadow Ward.

## Look

- **40 colour skins**, plus **custom colours**: on the Skins tab click any colour in the strip for a
  colour wheel (with an Opacity slider for the see-through parts), then save your set under a name.
- **Menu artwork** (needs ForeverArt): High resolution, Low resolution or Off, and a choice of header picture.
- **Named profiles**: save, load and delete whole setups. Reset to default keeps them.

## Commands

| Command | What it does |
|---|---|
| `/fwl2` | Open or close the menu |
| `/fwl2 help` | Open the Help tab |
| `/fwl2 abilities`, `skins`, `profiles`, `text`, `frames`, `map` | Open that tab |
| `/fwl2 show` / `hide` | Whole HUD on or off |
| `/fwl2 energy|regen|swing|combo|trail on|off` | One element on or off ("energy" is the resource bar) |
| `/fwl2 cooldown on|off` | Countdown numbers |
| `/fwl2 lock` / `unlock`, `sticky`, `grid` | Editing aids |
| `/fwl2 skin <name>`, `save <name>`, `load <name>`, `reset` | Skins and profiles |

## Abilities

IDs are rank 1 and only a fallback: at login the addon asks the client for the ID behind each
spellbook name, so an icon follows the rank you actually know.

| Ability | Fallback ID | Default |
|---|---|---|
| Death Coil | 6789 | on |
| Howl of Terror | 5484 | on |
| Soul Fire | 6353 | on |
| Shadow Ward | 6229 | on |
| Fear | 5782 | off |
| Life Tap | 1454 | off |
| Banish | 710 | off |
| Inferno | 1122 | off |
| Curse of Agony | 980 | off |
| Curse of the Elements | 11723 | off |
| Curse of Shadow | 402791 | off |
| Corruption | 172 | off |
| Immolate | 348 | off |
| Drain Life | 689 | off |
| Drain Soul | 1120 | off |
| Searing Pain | 5676 | off |
| Rain of Fire | 5740 | off |
| Hellfire | 1949 | off |
| Incinerate | 412758 | off |
| Bane of Havoc | 1225228 | off |
| Wrack | 1316697 | off |
| Shadowburn | 17877 | off |
| Conflagrate | 17962 | off |
| Siphon Life | 18265 | off |
| Amplify Curse | 18288 | off |
| Fel Domination | 18708 | off |
| Shadow Bolt | 686 | off |
| Demon Armor | 706 | off |
| Demon Skin | 687 | off |
| Summon Imp | 688 | off |
| Summon Voidwalker | 697 | off |
| Summon Succubus | 712 | off |
| Summon Felhunter | 691 | off |

## How it stays within the client's rules

Public API only. No protected calls, no combat automation, no combat log, nothing written outside
its own SavedVariables. Values the client marks secret are handed to widgets and never compared or
calculated with; a cooldown the addon may not read simply shows no number.

## Known limits

- Not verified in game (see Status).
- Bars turn in quarter turns only; a turned icon's border, sweep and number stay upright. Unit frames move and size but do not turn.
- Glow, dim and red tint depend on what the client will tell an addon; in combat it may withhold
  those answers and the icon then stays plain.
- A few fallback spell IDs are unconfirmed on this client; the name lookup normally corrects them.

## How it is built

This file and the addon are generated: one generator produces all nine class HUDs from a single
reference, so they stay identical in behaviour. A mocked-client suite (722 assertions for this
class), a Lua 5.1 limits check and a simulated UI run are part of every build.
