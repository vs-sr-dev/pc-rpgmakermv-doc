# 01 — the object: a tool that stopped hiding, and the quarter of it nobody can read belongs to somebody else

*Measure: `python _work/copyverify.py`, in `notes/copyverify.txt`; `python
tools/hashall.py rpgmakermv-steam`, in `notes/sha1-all.txt`; `python
tools/treecensus.py rpgmakermv-steam`, in `notes/treecensus.txt`; `python
tools/coverage.py tree --root rpgmakermv-steam` before and after this session's
repairs, in `notes/coverage-tree-before.txt` and `notes/coverage-tree.txt`.*

---

## What it is

**RPG Maker MV**, Steam app **363890**, a Japanese game-making tool published by
**KADOKAWA CORPORATION** and credited to **YOJI OJIMA**. It is the **sixth and
last** object of one product family in this collection, and **the first of the
six not built on RGSS**.

There is no Ruby interpreter, no `Marshal` serialisation, no RGSS DLL and no
compiled help file. **The engine is six JavaScript files, 943,098 bytes, with
their comments intact. The database is JSON.** What four previous sessions of
this pipeline worked to recover — a scripting language behind an encrypted
archive, an object model behind a binary serialisation, a manual behind an
undocumented container — this object hands over.

**The owner is not buying MZ.** Whatever question this repository leaves open
stays open, and [14](14-leftovers.md) says of each one whether it is closed,
settled somewhere else, or stranded.

---

## The copy, on four axes

```
python _work/copyverify.py                        (notes/copyverify.txt)

source files       : 9641
source directories : 406, of which empty 10
bytes                   : 2925489709
size agrees             : 9641 of 9641
mtime agrees to 100 ns  : 9641 of 9641
sha1 agrees             : 9641 of 9641
directories, source     : 406   copy : 406   agree : True
empty directories       : 10    copy : 10    agree : True
size, mtime, sha1 and the directory tree all agree : True
the original was opened read-only and nothing was written to it
```

**Ten empty directories, where the previous object had none.** A directory
holding only subdirectories is not an empty directory; the tree has **406
directories, 324 of which carry a file and 83 of which do not**, and ten of
those 83 hold nothing at all.

---

## The nine denominators, and the second one is the finding

Rule 3 of this pipeline says every figure names its denominator. There are nine
here.

| | denominator | what it counts |
|---|---:|---|
| 1 | **9,641 files / 2,925,489,709 bytes** | the tree, walked |
| 2 | **2,925,487,466 bytes** | **what the shop thinks the tree weighs — short by 2,243** |
| 3 | **406 directories**, 10 empty, 83 carrying no file | the shape |
| 4 | **7,417 distinct sha1**, 2,224 extra copies, 659,123,163 bytes | how much of it is itself |
| 5 | **149 binaries in four formats**; `pecensus.py` reads 102 | the code |
| 6 | **129 JSON documents**, 128 of which parse | the database |
| 7 | **1,341 audio stems, each shipped twice** | the music |
| 8 | **5,578 PNG**, 91,607 chunk CRCs of 91,607 | the pictures |
| 9 | **4,612 files in `dlc\`** — 1,458,606,099 bytes, half the object | the extras |

**The second is the finding**, and [03](03-the-shop.md) decomposes it to the
byte: the shop's total is short by exactly the bytes the object grew after
Steam last wrote it, less the 213 bytes of a log file Steam shipped with three
lines already in it.

---

## The coverage, which fell and then rose, and what that means

`coverage.py` classifies every file by magic into four buckets defined in
`pc-rpgmaker2000-doc/docs/09`. On arrival:

```
python tools/coverage.py tree --root rpgmakermv-steam
                                          (notes/coverage-tree-before.txt)

specified  7806 files   2100016569 bytes    71.7834 %
decoded       0 files            0 bytes     0.0000 %
derived       0 files            0 bytes     0.0000 %
opaque     1835 files    825473140 bytes    28.2166 %
SUM        9641 files   2925489709 bytes   100.0000 %   residue 0
```

**71.7834 % is the lowest opening figure since `pc-rpgmaker2003-doc`, and the
previous object closed at 98.0644 % with nothing opaque at all.** The obvious
reading — that this object hides more — is wrong, and [04](04-the-magic-table.md)
shows why: of the 1,835 opaque files, **190 were a defect this pipeline shipped
one session ago** and the other 1,645 are formats that are published, that this
box simply had no signature for, and **that belong to Chromium, to Qt, to
Apple, to the ISO and to Google rather than to KADOKAWA.**

After a one-line repair and five new magics:

```
python tools/coverage.py tree --root rpgmakermv-steam
                                                (notes/coverage-tree.txt)

specified  9384 files   2786158378 bytes    95.2373 %
decoded     222 files     89662863 bytes     3.0649 %
derived       0 files            0 bytes     0.0000 %
opaque       35 files     49668468 bytes     1.6978 %
SUM        9641 files   2925489709 bytes   100.0000 %   residue 0
```

**95.2373 % specified plus 3.0649 % decoded, and 35 files opaque.** The DECODED
bucket has been empty since `pc-rpgmaker2003-doc` and [07](07-the-runtime.md)
argues what went into it and why.

**The thirty-five that remain are four families and one accident**: 4 ICU data
files at 40,494,112 bytes, 24 Qt translation catalogues at 4,873,554, 6 V8
snapshot blobs at 4,300,802, and one zero-byte file —
`tutorial-osx/TutorialGui.app/Contents/Resources/empty.lproj`, the first
zero-byte file this pipeline's coverage table has had to classify. 4 + 24 + 6 +
1 = 35 and 40,494,112 + 4,873,554 + 4,300,802 + 0 = **49,668,468** at residue 0.

**Not one of the thirty-five is the vendor's format.** The percentage, on this
object, measures the assembler and not the publisher — and that is
[07](07-the-runtime.md)'s argument and the question this repository closes on.

---

## Why there are sixteen documents

The constraint is to stay under twenty. The last ten sessions wrote 17, 18, 19,
17, 16, 16, 16, 17, 18 and 16, and this one writes **sixteen**, of which two are
the predictions and the scoring.

**Fourteen chapters for an object eight and a half times the previous one's
weight is a decision and it is this**: the object's own formats are two — JSON
and JavaScript — and both are read by the standard library, so no chapter is
spent recovering them. What needed a reader was **one** format, MPEG-4 audio,
and it earns [05](05-the-audio.md). What needed an argument rather than a
reader was the Chromium `.pak`'s bucket, and it shares [07](07-the-runtime.md)
with the three-and-a-half runtimes it belongs to. **The PNG, Ogg, MPEG-4 and
font censuses are rows of [02](02-the-technical-sheet.md) and evidence inside
arguments; none of them is a chapter, because a census of a resource family for
its own sake is a table and not a finding.**

---

## The family, measured

| | files | bytes | mean file |
|---|---:|---:|---:|
| 95 (1999) | 1 | 7,120,053 | — |
| 2000 (2017) | 477 | 23,518,308 | 49,304 |
| 2003 (2017) | 737 | 33,578,445 | 45,561 |
| XP (2017) | 913 | 26,915,383 | 29,480 |
| VX Ace | 2,026 | 342,722,404 | 169,162 |
| **MV** | **9,641** | **2,925,489,709** | **303,442** |

**475.9 % of the previous object's files and 853.6 % of its bytes.** Half of it
is downloadable content and **1,157,743,244 bytes of that — 39.6 % of the whole
object — is 1,341 recordings shipped twice**, once as Ogg Vorbis and once as
MPEG-4 AAC.

And it repeats itself in a second way: **7,417 distinct sha1 over 9,641 files,
1,351 hashes appearing more than once, 2,224 extra copies, and 659,123,163
bytes — 22.5 % of the tree — that are a byte string already somewhere else in
it.** The extreme case is `nwjs-win/locales/*.pak.info`: **one 403,711-byte file
under 106 names**, one per locale, all byte-identical.
