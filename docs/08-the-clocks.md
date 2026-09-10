# 08 — the clocks: seventeen waves that falsify the pipeline's oldest claim, a link timestamp in 2047 that is not a date, and a year cell with nothing to argue against

*Measure: `python tools/mtimes.py rpgmakermv-steam --waves`, in
`notes/mtimes-waves.txt`; `python _work/wavesum.py`, in `notes/waves-sum.txt`;
`python tools/pecensus.py rpgmakermv-steam --by-magic`, in
`notes/pecensus.txt`; `python tools/stampcheck.py rpgmakermv-steam`, in
`notes/stampcheck.txt`; `python tools/uuidscan.py rpgmakermv-steam`, in
`notes/uuidscan.txt`; `find rpgmakermv-steam -iname "*.chm" | wc -l` → **0**.*

---

## Seventeen waves, and the claim four objects confirmed does not survive

```
python tools/mtimes.py rpgmakermv-steam --waves   (notes/mtimes-waves.txt)

wave  1  2017-05-07 09:32:26 .. 09:43:22  6945 files  1,598,692,892  54.65%
wave  2  2017-06-09 17:58:19 .. 17:58:20     9            916,721     0.03%
wave  3  2017-06-23 21:30:59 .. 21:31:21    35          4,557,628     0.16%
wave  4  2017-06-28 19:42:36                 1             16,645     0.00%
wave  5  2018-02-21 05:56:36                 3          2,152,781     0.07%
wave  6  2018-02-21 22:17:43                 7             10,617     0.00%
wave  7  2018-03-06 22:30:23 .. 22:31:50   166        114,545,302     3.92%
wave  8  2018-06-21 20:51:00 .. 20:54:02   639        579,904,376    19.82%
wave  9  2018-08-22 06:43:39                 1             48,320     0.00%
wave 10  2018-08-28 18:26:15 .. 18:26:21   616          7,122,179     0.24%
wave 11  2018-10-18 05:58:15                 8             96,472     0.00%
wave 12  2018-12-22 05:55:13 .. 05:55:48   687        164,462,064     5.62%
wave 13  2019-01-01 05:33:03                 3             63,710     0.00%
wave 14  2019-07-06 08:33:48                67            244,628     0.01%
wave 15  2023-09-28 06:56:06 .. 06:56:43   451        452,652,918    15.47%
wave 16  2025-10-19 23:39:09                 1              1,340     0.00%
wave 17  2026-04-11 01:48:50 .. 01:49:00     2              1,116     0.00%
```

```
python _work/wavesum.py                            (notes/waves-sum.txt)

waves parsed : 17    files summed : 9641    bytes summed : 2925489709
against the tree's 9641 / 2925489709, residue : 0 / 0
waves Steam wrote    : 15, 9,638 files, 2,925,487,253 bytes
waves the owner wrote:  2,     3 files,         2,456 bytes
```

**`pc-rpgmaker2000-doc/docs/08` established that a delivery mechanism which
verifies the bytes destroys the dates**, and three objects confirmed it with one
wave each. `pc-rpgmakervxace-doc` found a two-file exception and called it a
fourth confirmation with an exception.

**Here Steam wrote fifteen waves over six years and three months, and the claim
does not survive.** Not one exception; fifteen distinct writing events, the
largest of them 6,945 files in eleven minutes and the smallest a single file.

**What the four earlier objects demonstrated was a property of how those four
trees were built, not of Steam.** Each of them was installed once, in one
operation, and had never been updated; every file's mtime was therefore the
moment of that one operation. This copy was installed and then **patched** —
waves 2 through 15 are Steam replacing some files and leaving the rest alone,
which preserves the untouched files' original dates. **A delivery mechanism that
verifies the bytes does not destroy the dates. An installation that has never
been patched does.** That is the corrected claim and it is
[13](13-corrections.md) B.1.

**And wave 15 is the one the shop confirms.** `LastUpdated` is **1695877036** =
2023-09-28 04:57:16 UTC = 06:57:16 local, and wave 15 runs from 06:56:06 to
06:56:43 local — **it ends thirty-three seconds before the manifest's
timestamp**, which is what writing 451 files and then recording that you did
looks like. *(The pre-briefing converts 1695877036 to 05:37:16 UTC and is wrong;
19,628 × 86,400 = 1,695,859,200 and the remainder is 17,836 s = 4 h 57 m 16 s.
[13](13-corrections.md) A.1.)*

**The last two waves are the owner running the program**, and neither is
creative work: wave 16 is `nwjs-win-test/debug.log` and wave 17 is the root
`debug.log` and a Steam Cloud stub. [03](03-the-shop.md) accounts for all 2,456
of their bytes.

---

## The COFF stamps span thirty-four years and one of them is not a date

```
python tools/pecensus.py rpgmakermv-steam --by-magic  (notes/pecensus.txt)

binaries        : 102     by format : PE32 101, PE32+ 1
COFF range      : 2013-05-13 .. 2047-10-19
distinct COFF days: 17
  2013-05-13  2013-10-05  2014-09-03  2015-05-06  2015-05-31  2015-10-21
  2016-01-11  2016-05-26  2016-12-20  2017-05-15  2018-01-20  2018-01-27
  2018-02-27  2018-03-06  2018-03-07  2023-09-15  2047-10-19
Authenticode: 6 of 102 carry a certificate table
```

```
python tools/stampcheck.py rpgmakermv-steam       (notes/stampcheck.txt)

  nwjs-win/d3dcompiler_47.dll       3661112  2455089808  2047-10-19 09:23:28  T1
  nwjs-win-test/d3dcompiler_47.dll  3661112  2455089808  2047-10-19 09:23:28  T1

T1 IMPOSSIBLE (mtime precedes link time)   : 2 of 102
T2 COLLIDING  (a stamp shared across sizes): 6 of 102
T3 ROUND                                   : 0 of 102
FALSE by at least one test                 : 8 of 102
the same, by DISTINCT BINARY               : 5 of 78
```

**`stampcheck.py` was silent on the previous two objects and this repository
reports it speaking, which is its first non-silent run in three.** Eight hits.

**And what it catches is Microsoft's own signed `d3dcompiler_47.dll` carrying a
link timestamp twenty-one years in the future.** Both copies are byte-identical
at 3,661,112 bytes and both are among the six files carrying a certificate
table — a signature that would not verify if the bytes had been altered.

**2455089808 is not a lie about a date. It is a build hash written where a
timestamp goes.** Microsoft's deterministic-build toolchain replaces the COFF
`TimeDateStamp` with a hash of the build inputs, so that two builds of the same
source produce two identical files; the field stops being a clock and becomes an
identifier. **The instrument is right and the interpretation is this session's**,
and reporting the 2047 as a falsified date would be the easiest mistake on this
page.

**The other six hits are T2, a stamp shared across binaries of different
sizes.** That is what a build system that links many DLLs in one run produces,
and it is a property of the build and not of any file.

**And the object's own clocks are visible in the same table.** The graphics
libraries at 2018-01-20 and 2018-01-27; the NW.js core at 2018-03-06 and
2018-03-07; **2023-09-15, the newest real stamp, thirteen days before the last
Steam update and the same date as the three lines of `debug.log` that Steam
shipped** ([03](03-the-shop.md)).

---

## The UUIDs, and 103 machines are not 103 machines

```
python tools/uuidscan.py rpgmakermv-steam            (notes/uuidscan.txt)

version-1 UUIDs : 731 in 258 files
distinct node fields : 103
carrying a plausible date : 638 of 731
earliest : 1995-08-30 23:40:58 UTC     latest : 2098-06-03 17:15:18 UTC
```

A version-1 UUID's node field is, by RFC 4122, the generating machine's MAC
address. **`uuidscan.py` never prints one**: it prints a hash, so that two
identifiers from one machine can be seen to be from one machine without the
machine being named, and it does that without being asked.

**103 distinct node fields, against the previous object's 2 and the one
before's 3.** The question the count leaves open is whether that is 103 machines
that each touched one file:

```
python _work/addrcount.py                           (notes/addrcount.txt)

node fields in exactly one file   : 47
node fields in more than one file : 56
   Mae87   59 uuids across 35 files
   M8d29   34 uuids across 34 files
   M31cc   32 uuids across 20 files
```

**Fifty-six of the 103 appear in more than one file and forty-seven do not.**
The largest is one machine in 35 files. **That is a long history rather than a
build farm**: a build farm produces a few identifiers in very many files, and
this distribution is the opposite shape — many identifiers, most of them in one
or two files each, which is what a decade of individual artists' tools writing
UUIDs into PNG metadata looks like. [10](10-whose-bytes.md) takes the personal-
data question.

**And 93 of the 731 carry a date the tool calls implausible**, the extremes
being 1995 and 2098. A version-1 UUID's timestamp is 100-nanosecond intervals
since 1582; a generator that seeds it badly produces exactly this. **93 is a
different population from the 638 and this repository does not claim to have
looked at it** — [14](14-leftovers.md).

---

## There is no `.chm`, and that is the answer to a standing question

```
find rpgmakermv-steam -iname "*.chm" | wc -l     ->  0
```

Five ITSF specimens over five objects had produced a derivation that never
missed and a question nobody could close:

| | locale | whole-hour term + seconds |
|---|---|---|
| `RPGVXAce.chm` | 0x0411 | **17 h** + 7.891813 s |
| `RPGXP.chm` | 0x0411 | **16 h** + 3.953125 s |
| `rpg2003.chm` | 0x0C07 | 17.478706 s |
| `rpg2000.chm` | 0x0C07 | 8.443916 s |
| `SLPEI.chm` | 0x0407 | 8.157558 s |

`pc-rpgmakervxace-doc/docs/08` asked **what varies by exactly one hour between
two Japanese-locale help compiles** and named the measurement that would settle
it: **a sixth 0x0411 specimen compiled between late March and late October whose
whole-hour term is sixteen**, which would make the answer daylight saving in the
compiling machine's timezone rather than anything about the locale.

**This object cannot provide it.** The help is **139 loose HTML pages and 349
PNG under `Help\`**, 47,622,147 bytes, with no container at all — and 39 of the
139 HTML files carry a byte-order mark, which is why 190 files were misfiled
([04](04-the-magic-table.md)).

**The thread does not close. It runs out of specimens, and since there is no
seventh object it runs out here.** The measurement that would close it is
written down in [14](14-leftovers.md) so that somebody with a sixth `.chm` can
make it, and that sentence is what remains of five sessions' work on the
question.

---

## Every clock this object carries

```
2013-05-13   the earliest COFF stamp
2015         'Copyright (C) 2015 KADOKAWA CORPORATION / YOJI OJIMA'
2017-05-07   mtime wave 1, 6,945 files -- more than half the object
2017-06-28   the Sangokushi EULA, a .docx, and the whole of wave 4
2018-01-20 / 2018-01-27   the two NW.js graphics builds, seven days apart
2018-03-06 / 2018-03-07   the NW.js core, and mtime wave 7
2018-06-21   mtime wave 8, 639 files, 580 MB
2018-12-22   mtime wave 12, 687 files, 164 MB
2019-07-06   mtime wave 14, the last content wave before 2023
2023-09-15   the newest real COFF stamp, and debug.log's first three lines
2023-09-28   mtime wave 15, and LastUpdated 1695877036
2025-10-19   wave 16: a Chromium log
2026-04-11   wave 17: a Chromium log and a Steam Cloud stub
2047-10-19   a link timestamp that is a build hash
```

---

## The year cell, and what kind of argument it is

`pc-gamelist-doc` wants a `Year`. **The previous three rows of this family were
settled by a `.chm`'s compile clock agreeing with a copyright field, and there is
no `.chm`.**

The candidates:

| candidate | what it is | what is wrong with it |
|---|---|---|
| **2015** | `LegalCopyright` in `RPGMV.exe` | a vendor's own assertion, with nothing independent behind it |
| 2017-05-07 | when 6,945 files of 9,641 were written | that is when *this copy's* depot was built, not when the product was made |
| 2023-09-28 | `LastUpdated`, the newest content | the date of a patch |
| 12244690 | the Steam build id | a counter, not a date |
| 1.6.3 / v1.6.2 | a version the object states twice and differently | not a date either |

**The cell is 2015**, and the argument for it is different in kind from the three
before it, which is the thing worth saying.

`pc-rpgmakervxace-doc/docs/08` argued **2012** *against* a 2011 copyright field,
because three independent artefacts — a help compile, an executable's link time
and a resource — clustered inside twenty-one days of 2012. **That was a
disagreement resolved by counting witnesses.**

**Here the copyright field has no rival**, and an argument with nothing to argue
against is a weaker thing wearing the same clothes. It is not confirmed by the
mtimes (2017, the depot build), not by the COFF stamps (2013–2018, the
components' own build dates), and not by the manifest (2023). **It is confirmed
by nothing, and it is contradicted by nothing.**

**So the cell reads 2015 on the vendor's authority alone**, and this chapter
records that as an *attribution* rather than a *derivation* — the same
distinction `pc-rpgmakervxace-doc/docs/06` drew when it wrote ATTRIBUTED where a
looser tool would have written the answer. **A number nobody can check is still
the best number available; what it is not is a measurement, and the difference
is the whole content of this section.**
