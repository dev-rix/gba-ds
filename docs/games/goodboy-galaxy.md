# Goodboy Galaxy

| | |
|---|---|
| Releases | `2GBP` World (the 2023 cartridge: English, French, German, Spanish, Portuguese, Japanese, Chinese, Arabic and Korean) |
| Dumps | `2GBP` none known |
| Profile | `src/profiles.c`: the `2GBP` entry |
| Tests | `tests/regress/goodboy-galaxy.json` (`tools/regress.py goodboy-galaxy`) |
| Status | supported |

What GBA DS does with this game. Each rule is a promise the profile keeps; the regression tests check them (the cases citing a rule are listed by `tools/regress.py --list goodboy-galaxy`). Change a rule here first when the behaviour is meant to change, then the profile, then the tests and goldens. Rule numbers are never reused: a dropped rule stays, marked *retired*.

Every game also follows the [general rules](README.md#general-rules) (GEN-1 to GEN-7).

## Rules

**GG-1. Logo.** The logo is the title's lettering (GOODBOY GALAXY with the paw in its O), without the stars under it, the file box or NEW GAME / OPTIONS.

**GG-2. Planet map.** While Maxwell is out exploring a planet (he can be moved), the second screen shows the pause screen's Planet Map page (START, the first of its three pages), opened on the hidden copy and taken again about once a second: the map window round where Maxwell is, with his marker and the place's name, as the game draws it, in whatever language the game is set to. The page's bottom row (the bar of pages with its L and R buttons, the START button and the MAPPED percentage) is black instead: the second screen is for looking at, not for pressing, and the gem counter goes there (GG-6). With `map_crop = 0` (gba-ds.cfg), the whole page is shown, that row too. The map window's own arrows (the blue tabs round it) stay: they're part of its frame.

**GG-3. Logo elsewhere.** The second screen shows the logo before the first map picture and whenever no planet is being explored: on the language list, the title and its file menu, and the scenes between planets (flying through space), and from the title on after leaving a game.

**GG-4. Conversations.** While someone is talking (a line of text along the bottom with their portrait, or a scene played in the middle of a planet), no map picture is taken: the second screen keeps its last one.

**GG-5. The game's own pause screen.** While the pause screen opened in the game is up (on the game screen, on any of its pages), the second screen shows the logo, so the map isn't on both screens at once; the last map picture comes back as it closes, and is taken again within a second.

**GG-6. The gem counter.** The counter the game slides into the game screen's top left corner for a second as Maxwell picks up a gem (the spinning gem and the number collected) isn't drawn there while he can be moved; it's on the second screen instead, centred in the black row below the map, as it was once it had slid into place, and it stays there showing the last count until he picks up another gem. Until the first gem after starting the game or loading a state, the row is empty. In a conversation and while the game's own pause screen is up, the game draws its own sprites as usual and the row has nothing (the map is kept, GG-4, or the logo shown, GG-5). With `map_crop = 0` the counter isn't on the second screen (the page's bottom row is there instead), but it's still left off the game screen.

## How it was checked

A new game played from the language list to the Outpost (Planet Dookee, the first planet) in English and in French, the pause screen opened from each of its pages (it opens on the page it was left on, so the hidden copy presses L twice to reach the map), and a few minutes of random play there (the Outpost, the caves to its right): the map was taken every time Maxwell could move; the conversations at the Outpost took none.

## Not covered yet

- Only the first planet was reached. The other planets, the boss fights, the ship and the end of the game are untested: a state from any of them (from State Saver, or a bug report) would show whether the map is taken there and the logo shown where it should be.
- The counter is found by its sprites (palettes 12 and 14 at priority 0, its own tiles) in the top left corner; if the game shows other messages in the same row of sprites, they'd move to the second screen too. None was seen on the first planet.
- Going from one map cell to the next doesn't start a capture at once (GEN-6): the map is taken again within a second as usual.

## For the merge

The changelog line (under the open version's "New games"):

- **Goodboy Galaxy** (the 2023 cartridge, every language): while Maxwell explores a planet, the second screen shows the game's own Planet Map (the pause screen's first page) with the place's name, kept up to date about once a second, without the page bar, START button and MAPPED percentage below it (`map_crop = 0` shows them). The gem counter that pops up as you collect gems moves there, below the map, and stays showing your last count. Conversations keep the last map; the game's own pause screen, the title, the menus and the scenes between planets show the logo. Known limitation: only the first planet has been tried so far.

The wiki's table row (wiki/Supported-games.md):

| Goodboy Galaxy | `2GBP` (one release, nine languages) | the planet map, with the gem counter below it |

And its section:

## Goodboy Galaxy

The 2023 cartridge (one release, in English, French, German, Spanish, Portuguese, Japanese, Chinese, Arabic and Korean). Only the first planet has been tried so far.

- **While you explore a planet,** the second screen shows the game's own **Planet Map** (the first page of the pause screen): the map round where Maxwell is, with his marker and the place's name. It's opened in the background on a silent copy of the game about once a second; your game is never paused. The page bar (with its L and R buttons), the START button and the MAPPED percentage below the map are left out (`map_crop = 0` shows them).
- **The gem counter** that slides in at the top left as you pick up gems leaves the game screen and goes below the map, where it stays with your last count.
- Conversations keep the last map on the second screen; pausing in the game shows the logo there (the map is on the game screen then), and the map comes back as you unpause.
- The title, the menus and the scenes between planets show the logo.
