# 07 — the runtime: a quarter of the object belongs to Google, the bucket that was empty for four objects, and two Windows players that are one build a week apart

*Measure: `python tools/chpak.py census rpgmakermv-steam`, in
`notes/chpak-census.txt`; `python tools/zipdir.py
rpgmakermv-steam/nwjs-osx-unsigned.zip`, in `notes/zipdir.txt`; `python
_work/nwver.py`, in `notes/nwjs-versions.txt`; `python _work/stamps2.py`, in
`notes/nwjs-stamps.txt`; `python _work/nwbuild.py`, in `notes/nwjs-build.txt`;
`python _work/nwjoin.py`, in `notes/nwjs-join.txt`. `chpak.py`'s selftest is 19
checks, 0 failures, run with `PYTHONIOENCODING` unset.*

---

## Four runtimes, and this is the first object in the collection that ships code for three operating systems

| | files | bytes | what it is |
|---|---:|---:|---|
| `nwjs-win` | 125 | 159,791,316 | the Windows player |
| `nwjs-win-test` | 152 | 232,540,106 | a second Windows build, with PNaCl, chromedriver and `nwjc` |
| `nwjs-lnx` | 122 | 202,552,945 | the Linux player, ELF |
| `nwjs-osx-unsigned.zip` | 1 | 205,182,933 | the macOS player, in a ZIP |
| | **400** | **800,067,300** | **27.3 % of the tree** |

**None of it is KADOKAWA's.** It is NW.js, which is Chromium plus Node, and the
`CompanyName` fields say so: `The NWJS Community` on five binaries, `Digia Plc`
on forty-nine, `The ICU Project` on six.

---

## The `.pak`, and the bucket that was empty for four objects

222 files and 89,662,863 bytes are Chromium's resource container. It has no
specification; it has a published reader in Chromium's own source; and
[04](04-the-magic-table.md) argues from that to **DECODED**, the bucket ITSF went
into and the first entry it has had since `pc-rpgmaker2003-doc`.

`tools/chpak.py` walks it. **The index is not a signature, it is an equation** —
the first entry's offset must be exactly where the header ends, and the sentinel
entry's offset must be the file length:

```
python tools/chpak.py census rpgmakermv-steam       (notes/chpak-census.txt)

files whose .pak header arithmetic closes : 222
index walks that close on the last byte   : 222 of 222

  by version : {4: 54, 5: 168}
  bytes      : {4: 19506192, 5: 70156671}     total 89662863

  resources, summed  : 868459
  aliases,   summed  : 127790
  index bytes        : 5723246
  payload bytes      : 83937115
  duplicate ids inside one index : 0

  resource sizes : min 0  median 34  max 1711525  mean 96.7
  zero-length resources : 164
  resources that decode as UTF-8 : 862722 of 868459
  resources that do not          : 5737
     3928  PNG (W3C / ISO 15948)
     1805  not identified by any signature this tool knows
        2  JPEG / JFIF (ITU-T T.81; ISO/IEC 10918)
        1  RIFF WAVE (Microsoft and IBM)
        1  Windows icon
```

**The accounting closes twice.** 54 × 9 + 168 × 12 = **2,502** header bytes, and
2,502 + 5,723,246 + 83,937,115 = **89,662,863** at residue 0 — the same total
`treecensus.py` reports for the `.pak` extension, arrived at from inside the
files instead of from the directory entries.

**And the pre-briefing's third unverified claim is confirmed**: the 222 are two
versions and only two, 4 and 5.

**What they hold is Chromium's own user interface.** The locale files carry
strings — *About Chromium*, *Get help with Chromium*, *Updating Chromium* — and
`qtwebengine_resources.pak` carries the browser's internal pages: JavaScript
and HTML beginning `// Copyright (c) 2010 The Chromium Authors`, and 3,928 PNG.
**868,459 resources across 222 files, and 862,722 of them are text.**

**This census counts and sizes resources; it does not read them.** What a
resource *means* is not in the container, and `chpak.py`'s docstring names that
in advance: a reader that skipped what it could not decode would be publishing a
census of its own competence, so the 5,737 non-text resources are classified by
`coverage.py`'s own magic table and counted rather than dropped.

**159 files exist to describe 159 locales and 106 of them are byte-identical.**
`nwjs-win/locales/*.pak.info` is one 403,711-byte file under 106 names and
`nwjs-lnx`'s is the same thing under 53 — the largest repetition in the object
and 63,826,999 bytes of `.info` in total.

---

## The macOS player, in a ZIP nobody had opened

The refusal harness declared *there is no ZIP in this object* over a
205,182,933-byte ZIP. That is [12](12-the-tools.md)'s defect; the tool that
actually walks an arbitrary ZIP is **`zipdir.py`**, which had never been pointed
at this object and is on P22's list.

```
python tools/zipdir.py rpgmakermv-steam/nwjs-osx-unsigned.zip
                                                      (notes/zipdir.txt)

file size        : 205182933 bytes
EOCD at offset   : 205182911  (22 bytes from the end)
entries          : 564 on this disk, 564 total
central directory: 96136 bytes at offset 205086775
ZIP64 locator    : absent
members parsed   : 564  (header said 564)

directory entries: 219      file entries : 345
compressed total : 204997407 bytes
uncompressed tot : 504651796 bytes
whole-archive ratio: 2.4617 : 1  (saves 59.38 %)

compression methods:
  deflate ( 8)  337 files   504647100 -> 204992711   2.462:1
  stored  ( 0)    8 files        4696 ->      4696   1.000:1

version made by: 0x031e  host 3 Unix   zip spec 3.0   x345
```

**564 entries, 219 of them directories, walked to residue 0 without extracting a
byte.** The archive holds **168 more `.pak`** (61,993,122 bytes uncompressed),
**3 ICU `.dat`** (30,513,744), **5 `.dylib`** (24,409,168) and 105 `.nib`. So
the object's true Chromium `.pak` count is 222 on disk and **390 including the
ZIP**, and its ICU data is 4 files on disk and **7** including it — figures
[02](02-the-technical-sheet.md) does not carry, because the tree census counts
the ZIP as one file and that is the right denominator for a tree census.

**`host 3 Unix` on all 345 file entries** is the archive saying it was made on a
Unix, which is what a macOS build machine is.

---

## Are the runtimes one version built four ways?

The version resources do not say. Five patterns were tried — `nw/x.y.z`,
`Chrome/…`, `node.js/…`, the UTF-16 forms, and the generic `FileVersion` value —
and **none matched in `nw.dll`, `libnw.so` or `Game.exe`**. So the question was
asked of something else.

### The two Windows runtimes are one build with a test harness added

```
python _work/nwver.py                          (notes/nwjs-versions.txt)

nwjs-win : 125 files    nwjs-win-test : 152 files
names in both        : 123
byte-identical       : 114
differing            : 9
only in nwjs-win     : 2   Game.exe, package.json
only in nwjs-win-test: 29  chromedriver.exe, nacl64.exe, nwjc.exe,
                           nacl_irt_x86_32.nexe, nacl_irt_x86_64.nexe, …

the differing names:
   ffmpeg.dll                 win   2058240   test   2058240
   libEGL.dll                 win     78848   test     78848
   libGLESv2.dll              win   3730944   test   3730944
   swiftshader/libEGL.dll     win    101888   test    101888
   swiftshader/libGLESv2.dll  win   2246144   test   2246144
   node.dll                   win   5749248   test   5750784
   nw.dll                     win  84381696   test  85221888
   nw_elf.dll                 win    450048   test    449536
   resources.pak              win   4624843   test  13088130
```

**114 of 123 shared names are byte-identical.** Five of the nine that differ are
**the same size and different bytes**, which is the shape of one source compiled
twice — and the COFF header says so:

```
python _work/stamps2.py                          (notes/nwjs-stamps.txt)

  file                        win stamp             test stamp
  ffmpeg.dll                  2018-02-27 15:52:17   2018-02-27 16:54:38
  libEGL.dll                  2018-01-27 12:07:33   2018-01-20 12:03:33
  libGLESv2.dll               2018-01-27 12:07:22   2018-01-20 12:03:21
  swiftshader/libEGL.dll      2018-01-27 12:16:42   2018-01-20 12:10:48
  swiftshader/libGLESv2.dll   2018-01-27 12:18:02   2018-01-20 12:12:01
  node.dll                    2018-03-06 05:54:27   2018-03-06 10:52:17
  nw.dll                      2018-03-07 06:26:31   2018-03-07 07:21:27
  nw_elf.dll                  2018-03-07 03:01:36   2018-03-07 03:51:50
```

**The four graphics libraries are exactly seven days and a few minutes apart —
20 January against 27 January 2018 — and the three NW.js libraries are the same
day, hours apart.** `ffmpeg.dll` is the same day, sixty-two minutes apart. A
byte-level difference confirms it from the other side: `ffmpeg.dll`'s 2,058,240
bytes differ in **611 bytes over 81 runs**, and **the first run is at offset 280,
which is where that file's COFF `TimeDateStamp` sits.**

**And the build machine names the version out loud, in a place nobody was
looking:**

```
python _work/nwbuild.py                            (notes/nwjs-build.txt)

  nwjs-win        {'nw27_win32': 319, 'nw29_win32': 76}
  nwjs-win-test   {'nw27_sdk_win32': 319, 'nw29_sdk_win32': 80}
```

**`e:\build\nw27_win32` and `e:\build\nw27_sdk_win32`, at 319 occurrences each.**
`sdk` is NW.js's own name for the build that carries the developer tools, and
the number is the NW.js release. **The two Windows trees name the same two build
roots, differing by exactly the four characters `_sdk`, at exactly the same
count.** They are the normal and SDK builds of one thing, and the answer came
out of [10](10-whose-bytes.md)'s 2,314 drive-letter paths rather than out of a
version resource.

### The Linux and macOS runtimes cannot be compared the same way

```
python _work/nwjoin.py                             (notes/nwjs-join.txt)

the three on disk, `.pak` basenames compared pairwise:
  nwjs-win  vs nwjs-win-test  identical  55   different   1
  nwjs-win  vs nwjs-lnx       identical   0   different  56
  nwjs-win-test vs nwjs-lnx   identical   0   different  56
```

**55 of 56 resource files identical between the two Windows builds and 0 of 56
across platforms.** The second figure is **not** evidence of a different
version: a Chromium resource pack is built per platform, so byte identity across
platforms is not expected even from one release. **The measurement answers the
Windows question and does not answer the Linux or macOS one**, and saying so is
the honest end of it.

**What would answer it** is the `nw27`/`nw29` string in the Linux and macOS
binaries' own build paths, which are Unix paths and therefore live among
[10](10-whose-bytes.md)'s 15,529 rather than among the 2,314 — and extracting
205 MB to look inside the macOS ZIP is a thing this session chose not to do
under rule 4. That is [14](14-leftovers.md)'s.

---

## What this chapter is actually about

**28.2166 % of this object was opaque on arrival and none of it was the
vendor's.** After the repair and the magics the figure is 1.6978 % over 35 files,
and those 35 are ICU's, Digia's and Google's too.

**A coverage percentage measures who assembled the object, not who published
it.** The previous object closed at 98.0644 % because a Japanese company shipped
a Japanese program and a help file and a runtime it wrote itself. This one opens
at 71.7834 % because the same kind of company shipped a browser inside its
product — and a browser is 800 MB of somebody else's build.

**The vendor's own bytes** — `NewData\`, `Generator\`, `Help\`, `RPGMV.exe`, the
three asset builders and the editor's Qt front end — **are readable to the last
file, and the engine among them is source.** The percentage went down because
the denominator grew, and the part of the denominator that grew is Chromium.
