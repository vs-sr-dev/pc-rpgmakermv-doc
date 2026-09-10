# 09 — the programs: a hundred and forty-nine binaries in four formats, a vendor list that found nothing in an object made of vendors, and the publisher's name coming back

*Measure: `python _work/native.py`, in `_work/native.txt`; `python
tools/pecensus.py rpgmakermv-steam --by-magic`, in `notes/pecensus.txt`; `python
tools/verres.py dump rpgmakermv-steam`, in `notes/verres.txt`; `python
tools/vendorhash.py rpgmakermv-steam` and `--survey`, in `notes/vendorhash.txt`
and `notes/vendorhash-survey.txt`; `python _work/vendorsplit.py`, in
`notes/vendorsplit.txt`; `python tools/mzcensus.py`, `tools/sigcount.py` and
`tools/protscan.py`, in their own notes. `vendorhash.py`'s selftest is 42
checks, 0 failures, run with `PYTHONIOENCODING` unset.*

---

## Four formats, and this box reads one of them

```
python _work/native.py                              (_work/native.txt)

  family           files          bytes
  PE / MZ            102      379120928
  ELF                 20      188948352
  Mach-O              19       22524976
  Unix ar              8         280588
  TOTAL              149      590874844
```

**ELF and Mach-O are new to this collection in seventy-nine objects, and so is
the Unix archive.** `pecensus.py` reads PE and NE; it reports 102 binaries and
is right, and **211,753,916 bytes of executable code in this tree are in formats
it has no reader for** — 35.8 % of the object's compiled code.

`nwjs-lnx/lib/libnw.so` alone is **119,504,256 bytes**, an ELF64 shared object
for x86-64, and it is the single largest file in the tree apart from the macOS
ZIP.

**The eight Unix archives are PNaCl's static libraries** —
`pnacl_public_x86_64_libgcc_a` and its siblings — a format published in 1978 and
in continuous use since, which no object in this collection has produced before.

**This session added magics for all four** ([04](04-the-magic-table.md)) **and
did not write readers for any of them**, which is a decision. A magic moves
188,948,352 bytes of ELF from OPAQUE to SPECIFIED because the System V ABI is a
published document; a reader would be a fifth chapter's worth of work to
discover that Chromium is Chromium. **The four formats are named, counted and
classified, and what is inside them is [14](14-leftovers.md)'s.**

---

## The PE census

```
python tools/pecensus.py rpgmakermv-steam --by-magic   (notes/pecensus.txt)

binaries        : 102     by format : PE32 101, PE32+ 1
COFF range      : 2013-05-13 .. 2047-10-19    distinct days : 17
Authenticode    : 6 of 102 carry a certificate table
  SIGNED  steam_api.dll
  SIGNED  dlc/RPG Maker Freebies/…/Archeia_Steamworks/js/libs/steam_api.dll
  SIGNED  nwjs-win/d3dcompiler_47.dll
  SIGNED  nwjs-win-test/d3dcompiler_47.dll
  SIGNED  tutorial-win/msvcp120.dll
  SIGNED  tutorial-win/msvcr120.dll

CompanyName, by count:
  Digia Plc and/or its subsidiary(-ies)   49      (none)   34
  The ICU Project                          6      The NWJS Community   5
  Microsoft Corporation                    4      Valve Corporation    2
  KADOKAWA                                 2
```

49 + 34 + 6 + 5 + 4 + 2 + 2 = **102** at residue 0.

**Two of the 102 name KADOKAWA and forty-nine name Digia.** The publisher of
this product contributes two binaries out of a hundred and two, and the rest is
Qt, ICU, NW.js, Microsoft and Valve.

**Six signed files, and all six are third parties'** — Valve's twice,
Microsoft's four times. **Nothing KADOKAWA ships is signed.**

`mzcensus.py` reports **9 of 102**, its extension filter's **thirteenth**
appearance: it selects on `.EXE` and this object's 93 other binaries are DLLs.
The nine it does see all show the same DOS stub — `cblp` 144, `cp` 3, header
paragraphs 64, `cs:ip` 0000:0000 — which is the standard Microsoft linker stub
and says nothing about the programs.

**`sigcount.py`'s two counts differ for the first time in this pipeline.**

```
python tools/sigcount.py rpgmakermv-steam --hex 4d5a5000
                                                 (notes/sigcount-mzp.txt)
files BEGINNING with the signature   : 0 of 9641
occurrences ANYWHERE                 : 1, in 1 files
   dlc/BaseResource/audio/bgm/Dungeon5.ogg                  1
```

**The single `MZP` occurrence is inside a compressed Vorbis stream.** The tool's
own note says a signature that begins no file and appears inside many is a
coincidence; here it appears inside exactly one, and the file is 24 minutes of
dungeon music. It is not a near miss, and the two counts are printed apart
precisely so that neither can be quoted as the other.

`protscan.py`, **twentieth appearance**: **0 of 11 pre-2010 optical-media
protection markers**, with the four-zero-bytes positive control firing on **102
of 102 binaries**. **The 102 is the control and not a result** — an error
`pc-rpgmakervxace-doc/docs/13` records itself making, which is why it is stated
that way here.

---

## The vendor list found nothing, and the refusal was right

```
python tools/vendorhash.py rpgmakermv-steam     (notes/vendorhash-before.txt)
vendorhash: no third-party marker found under rpgmakermv-steam --
refusing to publish an empty list as a finding
```

**On an object that is Qt, Chromium, NW.js, Node, V8, ICU, PIXI, PNaCl and
Steamworks.** The tool carries a fixed table of markers — Micco's LZH library,
Nullsoft, Borland, the HTML Help runtime, Scintilla, Ruby — and **not one of
this object's third parties is in it.** It found two components on the previous
object and zero here.

**The refusal is the tool working.** It is written not to publish an empty list
as a finding, and it did not. **The table is the defect**, and it is a defect of
the same shape as `refusals.py`'s stale sentence and `mzcensus.py`'s extension
filter: *a fixed list nobody updated.*

### Nine probes, and the repair that is not the nine probes

Nine were added — Qt, ICU, NW.js, Chromium, V8, Valve, PIXI, Xiph's Vorbis
encoder and zlib — each firing on a name **in the file's own bytes**, in both
encodings where a linker writes one, with the offset printed as evidence. Twelve
checks were added with them, of which **two assert a non-match**: `Xiph.Org`
alone without the `libVorbis` line fires nothing, and the word `chromium` in
lower case fires nothing.

```
python _work/vendorsplit.py                     (notes/vendorsplit.txt)

  vendor                                 files          bytes  versions
  Xiph.Org Foundation                     1341      684463713  20120203 x826,
                                                               20050304 x321,
                                                               20030909 x76,
                                                               20070622 x62
  The Chromium Authors                     195       94144314  -
  Digia Plc / The Qt Company               115       81656902  5.4.2.0 x44
  The ICU Project                            6       49734656  -
  the pixi.js authors                        6        5147998  4.5.4, 2.2.10,
                                                               2.2.9
  The NWJS Community                         5      173765120  -
  The V8 project authors                     2      130943872  -
  Jean-loup Gailly and Mark Adler            2       21885056  1.2.11, 1.2.8
  Valve Corporation                          2         406896  03.75.32.07,
                                                               03.04.27.90
  TOTAL                                   1674     1242148527
```

**1,674 files and 1,242,148,527 bytes — 42.5 % of the object — carry a third
party's name in their own bytes, against zero.**

**And two rows are findings in themselves.** Every one of the 1,341 Ogg files
names its encoder, and **the encoder is four different builds**: 20120203 on
826, 20050304 on 321, 20030909 on 76 and 20070622 on 62. That is the audio
library's history written into the audio library, and it says the recordings
were not encoded in one session. **`pixi.js` appears at three versions —
2.2.9, 2.2.10 and 4.5.4** — because different DLC packs ship their own copy, and
a sample project written for version 2 still carries version 2.

### The repair that is the repair

**Adding nine rows does not fix the class of defect**: the next object will ship
a tenth vendor nobody listed, and a fixed table will find zero again and be just
as confident. **What a session needs is not a longer table but a statement of
what its table is missing.**

```
python tools/vendorhash.py rpgmakermv-steam --survey
                                            (notes/vendorhash-survey.txt)

  CompanyName                                files   covered  state
  Digia Plc and/or its subsidiary(-ies)         49        49  COVERED
  The ICU Project                                6         6  COVERED
  The NWJS Community                             5         5  COVERED
  Microsoft Corporation                          4         0  **NO PROBE**
  CompanyShortName                               3         3  COVERED
  Valve Corporation                              2         2  COVERED
  KADOKAWA                                       2         0  the PUBLISHER

distinct companies       : 7
  of which the publisher : 1      third parties : 6
with no probe at all     : 1
the table's coverage     : 5 of 6 = 83.3333 %
```

**The tool now reports its own blind spot with a denominator.** The one company
it cannot see is Microsoft, whose four binaries are `d3dcompiler_47.dll` twice
and the two Visual C++ runtimes — and the reason is that the existing Microsoft
probe looks for `hhctrl.ocx`, the HTML Help runtime, which this object does not
ship. **A probe for the wrong Microsoft product is the same defect one level
down**, and the survey is what makes it visible instead of silent.

*(`CompanyShortName` is a template placeholder left in a version resource by
whoever built three of the Qt plugins. It is counted as a company because the
linker wrote it where a company goes, and dropping it would be the survey
deciding what counts.)*

---

## The version resources, and the publisher came back

```
python tools/verres.py dump rpgmakermv-steam          (notes/verres.txt)

RPGMV.exe    FileDescription    RPG Maker MV
             LegalCopyright     Copyright (C) 2015 KADOKAWA CORPORATION
                                / YOJI OJIMA
             ProductName        RPG Maker MV
             ProductVersion     1.6.3
icudt53.dll  CompanyName        The ICU Project
             Comments           http://icu-project.org
```

**The lineage, in three copyright fields written by three linkers, each taken
from that repository's own `docs\`:**

```
pc-rpgmakerxp-doc     Copyright (C) 2005 Enterbrain, Inc. / Yoji Ojima
pc-rpgmakervxace-doc  Copyright (C) 2011 Enterbrain, Inc. / Yoji Ojima
pc-rpgmakermv-doc     Copyright (C) 2015 KADOKAWA CORPORATION / YOJI OJIMA
```

**The company changed and the person did not, and his name went into capitals.**

```
python tools/namescan.py rpgmakermv-steam --name Kadokawa …
                                                   (notes/namescan.txt)

  name                8-bit    files   UTF-16    files
  Kadokawa               96       45        9        3
  Yoji Ojima             95       54        1        1
  Enterbrain              4        2        0        0
  Degica                 40       13        0        0
  Yukihiro Matsumoto      0        0        0        0
  Neil Hodgson            0        0        0        0
  Scintilla               0        0        0        0
  pixi                 8625       47        0        0
  Ruby                   81       10        0        0
```

**Three reversals in one table.** `Kadokawa` was **0 of 2,026 in both encodings**
on the previous object and 0 of 913 on the one before — both figures taken from
those repositories' `docs\` — and here it is in 45 files. `Yoji Ojima` was 9
occurrences that **only a sixteen-bit pass could see**, and here it is 95 at
eight bits in 54 files. `Enterbrain` was 24 + 17 in five files and here it is 4
in 2. **And Ruby and Scintilla, in every object of this family since 2005, are
at zero.**

**The reason for all three is the same and it is not a marketing decision: the
engine is now text.** A name in a JavaScript comment is eight-bit ASCII in a
file anyone can search; a name in a version resource is UTF-16 inside a binary.

**And the measurement confirms it rather than the story doing so.**
`namescan.py` runs both passes and reports which files only the sixteen-bit one
can see: **two, `nwjs-win/Game.exe` and `nwjs-win-test/game.exe`.**
`utf16sift.py`, which `pc-rpgmakerxp-doc/docs/11` had to write because an
eight-bit sweep was blind to a whole object, **has two files to find here.**

**And the editor disagrees with its own engine about the version.** The resource
says `ProductVersion` **1.6.3**; the first line of `rpg_core.js` says **v1.6.2**.
Both are the vendor's own declaration, written by different parts of the same
company, and neither is wrong about anything except the other.
