# 14 — leftovers: what is closed, what was settled somewhere else, and what runs out of specimens because there is no seventh object

*Measure: every item names what would close it. Where the answer is "a specimen
this family will never supply", that is said and the measurement is written down
anyway, because the sentence is what remains.*

**This is the last object of six.** The owner is not buying MZ. A last chapter of
this kind is written badly in two opposite ways — pretending to close threads
that do not close, and not saying that they end — and this one tries to do
neither.

---

## §1 — Closed here

| | how |
|---|---|
| **which sixteen bytes depot 363896 is** | eight files named `Locale`, two bytes each, `65 6e`, residue 0 by walking ([03](03-the-shop.md)) |
| **what the 2,243 bytes are** | (1,065 − 213) + 1,340 + 51, twice over, and the pre-briefing's 213 refuted by a division ([03](03-the-shop.md)) |
| **whether the 1,341 `.m4a` and `.ogg` are the same music** | 1,341 pairs, MPEG-4 longer in 1,341 of 1,341, the overshoot fitted exactly to a 2,112-sample encoder delay on 1,069 of 1,075 same-rate pairs ([05](05-the-audio.md)) |
| **what the 222 `.pak` hold** | 868,459 resources, 862,722 of them UTF-8, 3,928 PNG among the rest, the index closing on 222 of 222 ([07](07-the-runtime.md)) |
| **whether the 222 `.pak` are two versions** | yes: 54 at v4, 168 at v5 ([07](07-the-runtime.md)) |
| **whether the three NW.js runtimes are one build** | the two Windows ones are, and the build machine's own directory names say `nw27_win32` and `nw27_sdk_win32` ([07](07-the-runtime.md)) |
| **how many of the 561 e-mail shapes are distinct** | 92 over 64 domains, 79 of them in more than one file ([10](10-whose-bytes.md)) |
| **whether the 103 UUID node fields cluster** | 56 in more than one file, 47 in one; a long history and not a build farm ([08](08-the-clocks.md)) |
| **whether any drive-letter path is this machine's** | none of 2,361 ([10](10-whose-bytes.md)) |
| **what `BaseResource_Compressed` compresses** | audio at about a fifth, pictures at about a third — and it holds 766 files the other pack does not ([13](13-corrections.md) A.6) |
| **what `Ace to MV Converter.rb` says about the previous object's format** | below |
| **the claim that a verifying delivery mechanism destroys the dates** | falsified, and restated ([08](08-the-clocks.md), [13](13-corrections.md) B.1) |

### The converter, since it was promised

```
python _work/converter.py                          (notes/converter.txt)

Ruby files in this object : 3, at 2 distinct sha1
   52,298  dlc/parallax_Resource_Pack/sample_project/js/plugins/…
   52,298  dlc/RPGmakerWeb_plugins/Shaz/Ace to MV Converter.rb
   50,618  dlc/RPGmakerWeb_plugins/Shaz/Ace  MV Converter.rb
the three files' encodings : {cp932: 2, utf-8: 1}

RPG:: classes the converter names               : 17
RPG:: classes pc-rpgmakervxace-doc/docs names   : 21
in both                                          : 10
only the converter                               :  7
only the previous session's                      : 11

MV `.json` names the converter writes            : 14
`.json` names in NewData\data                    : 15
names it writes that the object ships            : 14 of 14
```

**The only Ruby in 9,641 files is a third party's script for converting the
previous product's projects into this one's**, shipped inside two DLC packs, in
two versions of which one has a double space in its file name. It is
`module DEGICA::CONVERT`, so it is the western publisher's own.

**It names ten of the twenty-one classes `pc-rpgmakervxace-doc` documented, and
seven that session never named** — `RPG::Animation`, `RPG::Armor`,
`RPG::Class`, `RPG::CommonEvent`, `RPG::Item`, `RPG::Map::Encounter`,
`RPG::State`. **The reason is that that session opened the maps and not the
database**, and the converter had to open both. **It is an independent witness to
a model this pipeline read out of a binary `Marshal` dump**, and it agrees on
every class the two have in common.

**And its output side closes at 14 of 14**: every `.json` file name it writes
exists in `NewData\data`, and the fifteenth name there is `Map001.json`, which
is a map and not a database table.

---

## §2 — Settled somewhere else, and not by this object

| | where |
|---|---|
| the personal-data rule and its four amendments | the 95, the 2000, the 2003, the XP and the VX Ace; applied here unchanged, and its fifth part re-applied to the empty set ([10](10-whose-bytes.md)) |
| whether a third party's build path is a leak | `pc-rpgmakerxp-doc/docs/11`; 15,529 Unix paths and 2,361 drive-letter ones are findings under it |
| the four coverage buckets | `pc-rpgmaker2000-doc/docs/09`; the DECODED test applied to a new format ([04](04-the-magic-table.md)) |
| the ordering rule for the magic table | `pc-rpgmakervxace-doc/docs/04`; five magics added above the line and the rule's own check still firing |
| what a crossing rate measures | `pc-rpgmakerxp-doc/docs/12` and `pc-rpgmakervxace-doc/docs/11`; tested here and confirmed ([11](11-against-the-collection.md)) |

---

## §3 — Stranded: no seventh object, and the measurement that would close each

### The sixteen and seventeen hours

**Five ITSF specimens, one derivation that never missed, and one question.** Two
help files compiled at Japanese locale 0x0411 differ by exactly one whole hour —
`RPGXP.chm` at 16 h, `RPGVXAce.chm` at 17 h — and three specimens at other
locales carry no whole-hour term at all.

**The measurement that would close it: a sixth 0x0411 specimen compiled between
late March and late October whose whole-hour term is sixteen.** That would make
the term daylight saving on the compiling machine and not anything about the
locale. **This object ships no `.chm` at all** — the help is 139 loose HTML pages
— **so the thread does not close; it runs out of specimens, and there is no
seventh object.**

**It is stranded and it is not unanswerable.** Any RPG Maker help file compiled
at 0x0411 in the northern summer would settle it, and `chmclocks.py` is in the
box and takes one.

### The `.bind` section

`pc-rpgmakervxace-doc` left open what the `.bind` section of the RGSS runtime
holds. **This object has no RGSS runtime and no Ruby**, so it cannot look.
**The measurement is a section dump of `RGSS300.dll` against a Ruby build of the
same vintage**, and it needs an object with an RGSS DLL — which is the XP, the
VX Ace, or a product this pipeline is not going to see.

### The Winsock ordinal

`pc-rpgmakervxace-doc/docs/09` recorded an import of `ws2_32` by ordinal #116
and could not say why a game-making tool wanted a socket. **This object imports
nothing of the kind**, because its network layer is Chromium's. **The measurement
is a disassembly of the calling site**, which is beyond what this pipeline does
to a binary and is stranded for that reason rather than for lack of a specimen.

### The 93 implausible UUID dates

731 version-1 UUIDs, **638 with a plausible date and 93 without**, the extremes
being 1995 and 2098. **93 is a different population from the 638 and nobody has
looked at it.** The measurement is a histogram of the 93 by generating tool,
which means reading the PNG metadata around each of them — one afternoon's work
on an object nobody will open again.

### Which depot each file belongs to

`SizeOnDisk` closes against the four depots and the tree does not close against
`SizeOnDisk`, and [03](03-the-shop.md)'s reading requires that
`nwjs-win-test/debug.log` was shipped in no depot while its own contents suggest
it predates the last update. **The measurement is the depot manifest's file
list**, which Steam holds and this pipeline has never had. **Nothing in the tree
can settle it.**

### What is inside the ELF and Mach-O

20 ELF files and 19 Mach-O, 211,473,328 bytes, **classified and not read**.
The measurement is a section and symbol dump; the reader does not exist in this
box and writing one would have been a chapter about Chromium.
`nwjs-lnx/lib/libnw.so` at 119,504,256 bytes is the largest unread thing in the
object.

### The NW.js version of the Linux and macOS runtimes

The two Windows ones name `nw27` and `nw29` in their build paths. **The Linux
one's build paths are Unix and are among the 15,529; the macOS one is inside a
205 MB ZIP this session chose not to extract.** The measurement is a string
search of `libnw.so` for the same shape, and it is five minutes' work that this
session ran out of.

### The four ICU `.dat` and the twenty-four Qt `.qm`

40,494,112 + 4,873,554 bytes, **still opaque**, and both formats are documented
by their producers. **They are the only two families in the object that are
SPECIFIED in the world and OPAQUE in this table**, which is a gap in the table
and not in the world. Two magics would close it and this session added five and
stopped.

---

## §4 — Questions this object raised and did not answer

* **why three of 1,341 audio files were written by a different muxer**, when the
  other 1,338 came off one encoder run;
* **why the MPEG-4 side of 266 pairs was resampled up** from 22,050 to 44,100,
  which costs bytes and adds nothing;
* **what the four libVorbis encoder builds correspond to** — 20120203 on 826
  files, 20050304 on 321, 20030909 on 76 and 20070622 on 62 — which is the
  audio library's own history and is legible in it;
* **which five records `Items.json` has in English and not in Japanese**, by the
  structural alignment rather than by the id join. [06](06-the-database.md)
  establishes that the id join answers a different question and that the
  eight-item series is complete in both; **it does not name the five**, and the
  measurement is one more pass with the alignment key;
* **why `nwjs-win-test`'s `resources.pak` is 13,088,130 bytes against
  `nwjs-win`'s 4,624,843** — presumably the developer tools, and presumably is
  not a measurement;
* **whether the 1,805 resources inside the `.pak` that no signature identifies
  are one format or many.**

---

## §5 — The initialisms, split four ways

```
python _work/initialisms.py                       (notes/initialisms.txt)
735 text files searched
```

**Thirty-four terms. Demonstrated 12, derived 4, attributed 13, not
demonstrated 5. 12 + 4 + 13 + 5 = 34.**

### Demonstrated by the object — 12

The object spells these out in its own bytes:

| | where |
|---|---|
| **MV** | *RPG Maker MV*, in `RPGMV.exe`'s `ProductName` and in DLC readmes |
| **PIXI** | `pixi.js`, in the `<script>` tag of every sample project |
| **V8** | named in `pixi.js`'s comments |
| **SDK** | *Software Development Kit*, in a Steamworks plugin's readme |
| **LLC** | in a company name in `Help/page/01_11_14.html` |
| **EULA** | *END USER LICENSE AGREEMENT*, in a DLC licence in full capitals |
| **POSIX** | in a bundled library's comments |
| **RFC** | *RFC 3…*, in a bundled library's comments |
| **TP** | the engine's own parameter, `tpGain`, in the database and the source |
| **SE** | *sound effect*, in `rpg_managers.js` |
| **PE** | via `MZ`/`PE\0\0` in 102 binaries, which is the format naming itself |
| **JSON** | used throughout and expanded in `pixi.js`'s comments |

### Derived by this session — 4

| | from what |
|---|---|
| **M4A** | ISO/IEC 14496-14's brand `M4A ` in 1,338 `ftyp` boxes, read here |
| **PAK** | the container's own version field and index arithmetic, closing 222 of 222 |
| **BOM** | U+FEFF at the head of 190 files, counted here |
| **ASC** | the AudioSpecificConfig read out of 1,341 `esds` descriptors |

### Attributed to a public source — 13

Expanded from a specification or a project the object ships but does not itself
spell out: **AAC** (Advanced Audio Coding, ISO/IEC 14496-3), **ELF** (Executable
and Linkable Format, the System V ABI), **PNaCl** (Portable Native Client,
Google), **ICU** (International Components for Unicode), **QM** (Qt Message,
Digia), **NW.js** (formerly node-webkit), **COFF** (Common Object File Format),
**UUID** (RFC 4122), **CRC** (cyclic redundancy check), **ABI** (application
binary interface), **HTML**, **CSS**, **ISO/IEC**.

### Not demonstrated — 5

**IRT** — the object ships `nacl_irt_x86_64.nexe` and never says what the three
letters are; **MAC**, in the sense of the address inside a version-1 UUID, is
nowhere in the tree; **DOCX** appears only as an extension on one file;
**RGSS** occurs in a plugin comment and is never expanded; **GPU** is used and
never expanded.

### Against the previous object

`pc-rpgmakervxace-doc/docs/14` split thirty-three terms **9 demonstrated, 5
derived, 13 attributed, 6 not demonstrated**. This object's split is **12, 4,
13, 5** over thirty-four.

**The demonstrated column grew from 9 to 12 and that is smaller than it should
be.** This object publishes 139 HTML help pages, 943,098 bytes of commented
JavaScript and thirteen third parties' licence texts, and the previous one
published a compiled help file and no source at all. **A tenfold increase in
readable prose bought three terms.**

**The reason is worth having**, because it is a fact about documentation rather
than about this object: **a manual explains what a user does, not what a format
is.** `Help\`'s 139 pages tell somebody how to place an event on a map; they have
no reason to expand ELF, and they do not. **The prose that would demonstrate an
initialism is a specification, and a vendor that ships its engine's source still
does not ship the standards its engine reads.**
