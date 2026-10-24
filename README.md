# TCS decomp progress

Progress of a private rewrite of LEGO Star Wars: The Complete Saga (PC) in Rust and Bevy, made by porting the PC executable's gameplay code one function at a time. This repo holds numbers only (counts, sizes, percentages, function addresses and statuses). It contains no game files, no decompiled code and no game data.

Live page: https://drket.github.io/tcs-progress/

**1 of 36 story chapters plays end to end:** Negotiations (Episode I, chapter 1; Story and Free Play).

Of the code that level runs, **43.5% is ported** from the exe and 73.6% mapped, by bytes (12.6% confirmed against the real game). Of the whole exe: 36.4% ported.

## What works today

- Negotiations from the Story start to the status screen: the intro cutscenes, sections A, B and C, the doors between them, the outro cutscene and the status screen; and in Free Play.
- The HUD, the cutscenes, the status screen and the text crawl, from the exe's own rules.
- The lighting stage: every draw's colour comes from the PC's own shader formula (its lighting class, its light block and its blend), checked against the exe run offline (one factor, the doubled vertex colour, comes from reference footage: see below).
- Checked by: the owner's hand tests (a Free Play 100% run with every minikit, the red brick and True Jedi, 2026-10-21); the windowed smoke runs of the Story start, each section, a door, the outro and Free Play on every build (scripts/test-all).

## Not exact yet

- The Phong specular highlight (one exe function, FUN_00741690, is not mapped yet).
- Section C's directional lightmaps (their textures are not mapped).
- Blending is done on display values like the PC's, but in a float buffer, not the PC's 8-bit back buffer.
- The doubled vertex colour is taken from reference footage; where the exe does it is not found yet.
- The figures' lights use the section's light block, not the figures' own light query.

## Next

- The owner's hand test of the lighting work (one colour pipeline for the whole frame).
- Mapping what is still open in Negotiations: where the exe doubles vertex colours, the figures' lights, the specular.
- A second level only after Negotiations is approved.

## What the percentages mean

The percentages count functions of the PC exe that carry a PC 0x... cite in the Rust rewrite (ported) or are named in Ghidra (mapped). They do not measure how close the picture or the feel is. The engine layer that Bevy replaces is only partly recognised, so part of the unported share is code that is replaced rather than missing.

The level's set is the code its data reaches through the exe's tables (the call closure of every handler the level's scripts, gizmos and AI use) plus the rows of the level's maps; it includes shared code that every level needs.

![progress](progress.png)

Generated 2026-10-24T20:54:16Z from private repo commit `107daac` by `tools/progress/publish.py`.
