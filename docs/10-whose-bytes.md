# 10 — whose bytes: five hundred and sixty-one shapes that are ninety-two addresses, a hundred and three machines that are fifty-six, and two thousand three hundred paths of which none is this one

*Measure: `python tools/sift.py rpgmakermv-steam --group personal` and `--group
buildpath`, in `notes/sift-personal.txt` and `notes/sift-buildpath.txt`; `python
_work/addrcount.py`, in `notes/addrcount.txt`; `python _work/drivepaths.py`, in
`notes/drivepaths.txt`; `python tools/uuidscan.py rpgmakermv-steam`, in
`notes/uuidscan.txt`; `python tools/pathcheck.py`, in `notes/pathcheck.txt`.*

---

## The rule and its four amendments, which are not reopened

| | |
|---|---|
| `pc-rpgmaker95-doc/docs/10` | publish what claims credit, redact what routes a message |
| `pc-rpgmaker2000-doc/docs/10` | where it cannot be established that an address has stopped routing, redact |
| `pc-rpgmaker2003-doc/docs/12` | a device identifier is neither credit nor routing, and is redacted anyway |
| `pc-rpgmakerxp-doc/docs/11` | an address a linker wrote into a version resource is the most deliberate publication there is |
| `pc-rpgmakervxace-doc/docs/10` | what the owner of a copy made is not the object; it is measured where it changes a measurement and it is not read |

**All five are applied below and none is argued again.** What is new here is
scale — thirty times the previous object's e-mail population and fifty times its
machine identifiers — and the question scale raises is whether it changes
anything beyond the arithmetic.

**The fifth rule's first re-application returns the empty set**, and
[03](03-the-shop.md) records it: `projects\` holds one 51-byte file and Steam
wrote it. The two `debug.log` were measured as byte counts and line counts
because they change the shop's arithmetic, and were read only far enough to
count their lines and read their dates.

---

## Five hundred and sixty-one shapes are ninety-two addresses

```
python tools/sift.py rpgmakermv-steam --group personal
                                              (notes/sift-personal.txt)

blobs searched      : 9641   (9641 of 9641 -- nothing was filtered out)
e-mail shape        : 561 hits in 30 blobs
P.O. Box            :   6 in 6
telephone shape     :  38 in 8
home dir            :   2 in 2       /home/ : 1 in 1
Copyright <name>    :  62 in 4
positive control fired : YES     negative control quiet : YES
```

**561 occurrences is not 561 addresses**, and the previous object's session
proved that: 19 hits were three addresses. `_work/addrcount.py` is that script
re-aimed, and it keeps both of its rules — **exactly `sift.py`'s own pattern**,
because a looser one found 50 where the box found 19 with **thirty-one of them
inside compressed payloads** and this tree carries 1.4 GB of PNG and Ogg; and
**it never prints an address**, only a hash, so that two occurrences can be seen
to be one address without publishing it.

```
python _work/addrcount.py                          (notes/addrcount.txt)

occurrences          : 561
DISTINCT addresses   : 92
distinct domains     : 64
addresses in exactly one file  : 13
addresses in more than one     : 79

the ten commonest domains:
   openssl.org 105   cryptsoft.com 76   mips.com 45   openbsd.org 30
   courtesan.com 30  webkit.org 26      freebsd.org 19  gmail.com 16
   nongnu.org 12     thawte.com 11
```

**Ninety-two distinct addresses over sixty-four domains, and the domains name
the population.** OpenSSL, Cryptsoft, MIPS Technologies, OpenBSD, sudo's
maintainer, WebKit, FreeBSD, the GNU project, Thawte — **these are the licence
blocks of the open-source components inside Chromium and Qt**, and every one of
them is an address the component's own author wrote into the component's own
licence text and published to the world.

**`pc-rpgmakerxp-doc/docs/11`'s amendment governs and needs no extension**: an
address a third party published in its own copyright notice is the most
deliberate publication there is, and it is a finding rather than a leak. **This
chapter does not reproduce any of the ninety-two**, because reproducing them is
not what makes them findings — the count and the domains are.

**Sixteen occurrences are at `gmail.com`**, which is the one row that is not a
project domain, and they are inside DLC packs' readme files where individual
artists claim credit for their own work. **Credit is published under the 95's
rule and these are not reproduced either**, because publishing a private
person's address in a document is not the same act as that person publishing it
in a readme they wrote — and where the two rules point in different directions
this pipeline has always taken the quieter one.

**And 38 telephone shapes in 8 files and 6 post-box shapes in 6** are new
categories for this family. They are in the same licence blocks: a company's
switchboard and a company's mailing address, printed in a legal notice, and the
same reasoning applies.

---

## A hundred and three machines are fifty-six

```
python tools/uuidscan.py rpgmakermv-steam           (notes/uuidscan.txt)
version-1 UUIDs : 731 in 258 files
distinct node fields : 103        with a plausible date : 638 of 731

python _work/addrcount.py                           (notes/addrcount.txt)
node fields in exactly one file   : 47
node fields in more than one file : 56
   Mae87   59 uuids across 35 files
   M8d29   34 uuids across 34 files
   M31cc   32 uuids across 20 files
```

**A version-1 UUID's node field is the generating machine's MAC address, and
`uuidscan.py` redacts it by program without being asked.** The 2003's amendment
already covers it — a device identifier is neither credit nor routing and is
redacted anyway — and this chapter's only job is to say whether 103 changes
anything.

**It does not change the rule and it does change the reading.** 103 is not 103
machines each touching one file: **56 of the 103 appear in more than one file
and 47 do not**, and the largest single machine accounts for 59 identifiers
across 35 files. A build farm produces a handful of identifiers in very many
files; **this is the opposite shape**, which is what a decade of individual
artists' image tools writing UUIDs into PNG metadata looks like. Most of the
258 files are under `Generator\`, which is 2,738 files of character-generator
parts.

**And the arithmetic is the only thing that changed.** Two node fields on the
previous object and 103 here, and both are redacted the same way by the same
program with no session deciding anything.

---

## Two thousand three hundred and fourteen paths, and none of them is this machine

```
python tools/sift.py rpgmakermv-steam --group buildpath
                                             (notes/sift-buildpath.txt)
drive-letter path   : 2,314 in 44 files
unix build path     : 15,529 in 411 files
```

**The Unix half is settled by `pc-rpgmakerxp-doc/docs/11`** — a third party's
build path published by that third party is a finding — and 15,529 in 411 files
is what ELF binaries, Mach-O binaries and JavaScript source maps look like.

**The drive-letter half is the one nobody had settled**, and it is settled here
by walking:

```
python _work/drivepaths.py                        (notes/drivepaths.txt)

files carrying a drive-letter path : 70     occurrences : 2,361
by drive letter : {'C': 1508, 'E': 808, 'V': 8, 'Q': 7, 'T': 5, …}

the twelve files with the most:
   Qt5WebEngineCore.dll                     1410
   nwjs-win/node.dll                         397
   nwjs-win-test/node.dll                    397
   plugins/qtwebengine/ffmpegsumo.dll         19
   Qt5Core.dll                                16
   Help/page/01_11_05.html                    13

the twenty commonest roots:
   c:\work\build                1427     e:\build\nw27_win32          319
   e:\build\nw27_sdk_win32       319     e:\build\nw29_win32           67
   e:\build\nw29_sdk_win32        67     E:\Qt\Qt5.4.2                 14
   C:\Qt\Qt5.4.2                  14     C:\foo\bar                    12

FILES CARRYING A PATH OF **THIS** MACHINE : 0
```

*(2,361 in 70 files against `sift.py`'s 2,314 in 44 is a difference of pattern,
not of object: this script's shape admits a space inside a path and `sift.py`'s
does not. Both numbers are printed; neither is quoted as the other.)*

**Every root that occurs more than a dozen times names a third party's build
machine.** `c:\work\build` at 1,427 occurrences is Qt's; `e:\build\nw27_win32`
and `e:\build\nw27_sdk_win32` at 319 each are NW.js's — and
[07](07-the-runtime.md) uses them to answer a question the version resources
would not, because **the directory name carries the release number and the word
`sdk`**. `C:\foo\bar` and `C:\orandea\test` are documentation examples inside
Chromium's own help pages.

**Zero of the 2,361 is a path of this machine.** The check builds its needles
from the running environment and **does not print them**, which is the repair
`pc-rpgmakervxace-doc/docs/13` C.3 made to `pathcheck.py` after that tool
published its own needles into the file that proves it publishes none — the same
hazard, so the same precaution.

---

## Rule 7, over the repository

`pathcheck.py` asks the different question: not whether the *object* carries
this machine's layout, but whether the *documents* do.

```
python tools/pathcheck.py                          (notes/pathcheck.txt)
```

The run and its result are in that file, with the positive control firing and
the negative control quiet. **Where an absolute path appears in this repository
it is a third party's, published by that third party, and it is a finding**;
this machine's own layout appears nowhere, including inside any traceback
captured into `notes\`.

**And one path was withheld on purpose.** `steamacf.py`'s full dump prints
`LauncherPath`, which names a directory on this machine; `notes/steamacf.txt`
carries the `--check` output, which does not. [03](03-the-shop.md) says so
where the field would otherwise have been quoted, which is the same decision
`pc-rpgmakervxace-doc/docs/03` made and the reason it is a decision and not an
omission.
