# 03 — the shop: four depots that close to the byte, one of them sixteen, and a total that is short by three lines of a log file

*Measure: `python tools/steamacf.py --path <steamapps>/appmanifest_363890.acf
--root rpgmakermv-steam --check`, in `notes/steamacf.txt`; `python
tools/depotsplit.py --root rpgmakermv-steam --path 363896=…` for the eight
files, in `notes/depotsplit.txt`; `python _work/logbytes.py` for the residue, in
`notes/shop-2243.txt`; `python _work/wavesum.py` for the independent check, in
`notes/waves-sum.txt`.*

---

## The manifest

```
python tools/steamacf.py --path <steamapps>/appmanifest_363890.acf \
    --root rpgmakermv-steam --check                 (notes/steamacf.txt)

SizeOnDisk declared      : 2925487466
the tree, counted        : 2925489709 over 9641 files
residue                  : -2243

installed depots:
   363891         1466881351   manifest 3230861250424737476
   363894         1449233791   manifest  407257531944929161
   363895            9372308   manifest 8638420274259944741
   363896                 16   manifest 6136102577301405121
   sum          2925487466
   residue against SizeOnDisk : 0
```

**The previous object had a depot sum that did not close and a `SizeOnDisk`
that did not either. This one has a depot sum that closes exactly and a
`SizeOnDisk` short by 2,243 bytes — one part in 1.3 million.** Two consecutive
objects, two different failures, and this one is small enough to be decomposed.

`buildid` **12244690**. `LastUpdated` **1695877036**, which is **2023-09-28
04:57:16 UTC** — *the pre-briefing says 05:37:16 and is wrong by forty minutes;
19,628 × 86,400 = 1,695,859,200 and 1,695,877,036 − 1,695,859,200 = 17,836 s =
4 h 57 m 16 s. That is [13](13-corrections.md) A.1.* `LastPlayed`
**1775864950**, which is not `"0"` — **the second object in this collection
anybody has used**. `UserConfig` and `MountedConfig` both say `language
"english"`, where the previous object said `italian`.

`LastOwner` is a SteamID64 and `steamacf.py` redacts it by program without
being asked. **`LauncherPath` names a directory on this machine and is not
reproduced here**, which is rule 7 and is the same decision
`pc-rpgmakervxace-doc/docs/03` made.

**And two fields are absent.** There is no `BytesToDownload` and no
`BytesToStage`, so the staged-to-downloaded ratio that four objects reported —
1.1183, 1.5194, 1.3355, 1.0665 — **cannot be computed here and the series stops
at four.** `compratio.py --declared` has nothing to be given, and that is a
statement about this manifest and not about this product.

**And one field is new to this pipeline.** `SharedDepots` names **228985** and
**228986**, both belonging to app **228980** — Steamworks Common
Redistributables. They are referenced by this application and **not counted in
`SizeOnDisk`**, which the depot arithmetic above proves: the four installed
depots already sum to `SizeOnDisk` at residue 0, leaving no room for a fifth or
a sixth.

---

## Depot 363896 is eight files of two bytes

Sixteen bytes is smaller than the sentence that describes it. No file in the
tree is sixteen bytes long, so the depot is not one file — and
`depotsplit.py --path`, written on the previous object precisely so that a
single file could be its own group, answers it by walking.

```
python _work/locale8.py                              (notes/depot-16.txt)

  Locale                                               656e  'en'
  RPG Maker MV.app/Contents/MacOS/Locale               656e  'en'
  Scene Builder.app/Contents/MacOS/Locale              656e  'en'
  Tileset Builder.app/Contents/MacOS/Locale            656e  'en'
  Window Builder.app/Contents/MacOS/Locale             656e  'en'
  tool/GENE/Locale                                     656e  'en'
  tool/MADO/Locale                                     656e  'en'
  tool/SAKAN/Locale                                    656e  'en'

files of exactly 2 bytes : 8      their bytes, summed : 16
distinct contents        : [b'en']    all named `Locale` : True
depot 363896 declares    : 16     residue : 0
```

```
python tools/depotsplit.py --root rpgmakermv-steam \
    --path "363896=Locale" --path "363896=RPG Maker MV.app/…/Locale" … \
    --rest everything-else --declare 363896=16       (notes/depotsplit.txt)

  label        files      counted     declared   residue
  363896           8           16           16         0
  everything-else 9633   2925489693            -        -
  SUM           9641   2925489709

  every file claimed by exactly one group : True
  files no group claimed                  : 0
  groups whose counted bytes differ from the declared figure : 0
```

**Eight files, sixteen bytes, residue 0, and every figure produced by walking.**
No group's total is the tree's total minus another group's, which is the
property `depotsplit.py` exists to guarantee.

**The pre-briefing found five of the eight** — the root `Locale` and the four
macOS bundles — and missed `tool\GENE`, `tool\MADO` and `tool\SAKAN`. That is
[13](13-corrections.md) A.2.

**What the depot IS, is a language setting shipped as a separate downloadable
unit.** Eight copies of the two bytes `en`, in eight places: beside the editor,
inside four macOS application bundles that contain nothing else, and beside
each of the three asset builders. **Steam's depot mechanism exists so that a
different two bytes can be delivered to a Japanese customer without shipping
2.9 GB again**, and the smallest depot in this collection is the reason the
machinery exists.

---

## The 2,243 bytes, and the pre-briefing's arithmetic cannot be right

Three files postdate wave 15:

```
2025-10-19 23:39:09    1,340  nwjs-win-test/debug.log
2026-04-11 01:48:50       51  projects/steam_autocloud.vdf
2026-04-11 01:49:00    1,065  debug.log
                      ------
                       2,456
```

**2,456 − 2,243 = 213**, and the pre-briefing proposes that Steam shipped
`nwjs-win-test/debug.log` at 213 bytes and use grew it to 1,340. **That cannot
be true, and a log file says why.**

```
python _work/logbytes.py                            (notes/shop-2243.txt)

debug.log                1,065 bytes   15 lines  line lengths [71]
nwjs-win-test/debug.log  1,340 bytes   20 lines  line lengths [67]

213 / 71 = 3.0000  -- a whole number of lines
213 / 67 = 3.1791  -- NOT a whole number of lines, so this file
                      cannot have been 213 bytes
```

**Every line of each log is exactly one length**, because each is the same
Chromium warning repeated with a different timestamp. 15 × 71 = 1,065 and 20 ×
67 = 1,340, both at residue 0. **213 is three lines of the root log and is not
a whole number of lines of the other**, so the 213 belongs to `debug.log` and
the arithmetic is

```
(1,065 - 213) + 1,340 + 51 = 2,243        residue 0
```

**And the three lines are dated.** `debug.log`'s first three read
`[0915/174749…]`, `[0915/174750…]`, `[0915/174751…]` — **15 September, three
seconds apart, thirteen days before `LastUpdated` and the same date as the
newest COFF timestamp in the whole object (2023-09-15).** They are the
packager's own runs, shipped in the depot; the twelve after them are dated
1019, 0317, 0318, 0408 and 0411, and the last is `[0411/014900…]`, matching the
file's mtime to the second.

**And a second, independent route gives the same 213.**

```
python _work/wavesum.py                            (notes/waves-sum.txt)

waves Steam wrote     : 15, 9,638 files, 2,925,487,253 bytes
waves the owner wrote :  2,     3 files,         2,456 bytes

2,925,487,466 - 2,925,487,253 = 213
```

**`SizeOnDisk` exceeds the fifteen Steam waves by exactly 213 bytes** — the
part of `debug.log` Steam paid for, in a file whose mtime the owner's later runs
moved into wave 17. Two arithmetics that share no term arrive at the same
number, which is what a decomposition is supposed to look like.

---

## What the reading costs, said out loud

The reading requires that **`nwjs-win-test/debug.log` was not in `SizeOnDisk` at
all** — none of its 1,340 bytes. Its own contents make that uncomfortable: its
twenty lines are dated 0309, 0608 ×5, 0610, 0623 ×4, 0216, 0417 ×2, 0210, 0211
×3, 0215 and 1019, and a log is written in order, so the sequence needs at
least three calendar years. Anchored on the last line — 2025-10-19, its mtime —
the eleven earliest fall between **9 March and 23 June 2023**, which is before
`LastUpdated`.

**So either the owner ran a build of this program before 2023-09-28 and Steam's
update on that date left the file alone, or the file was shipped and
`SizeOnDisk` does not count it.** The arithmetic decides for the second only if
one is willing to let arithmetic settle a question about a date, and this
chapter is not. **The measurement that would settle it is the depot manifest's
own file list, which names every file a depot carries and which this pipeline
has never had**, and that is [14](14-leftovers.md)'s.

**What is settled is the 213 and the 2,243**, twice, and the refutation of the
pre-briefing's attribution, which needed one division.

---

## What is in `projects\`, and it is not the owner's work

```
projects/steam_autocloud.vdf    51 bytes    2026-04-11
```

**One file, and Steam Cloud wrote it.** The previous object carried 208,338
bytes of the owner's own project inside the game folder;
`pc-rpgmakervxace-doc/docs/10` wrote the rule that followed — *what the owner of
a copy made is not the object; it is measured where it changes a measurement and
it is not read.*

**Re-applied here, the rule returns the empty set.** The three files that
postdate the install are two Chromium logs and a cloud stub, none of them
creative work, and the two logs were measured **as byte counts and as line
counts** because they change a measurement — the 2,243 — and were read only far
enough to count their lines and read their dates.

**A rule whose first re-application finds nothing is a rule that has been put to
the test**, and it is the first rule in this pipeline to be re-applied at all.
