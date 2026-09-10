# 04 — the magic table: a byte-order mark that refused a hundred and ninety files, four formats new to this collection, and a signature that is an equation

*Measure: `python tools/coverage.py selftest`, **95 checks, 0 failures**, run
with `PYTHONIOENCODING` unset, in `notes/selftest-coverage.txt`; `python
tools/coverage.py tree --root rpgmakermv-steam` before and after, in
`notes/coverage-tree-before.txt` and `notes/coverage-tree.txt`; `python
_work/bomcheck.py` for the defect itself.*

---

## The defect, and this pipeline shipped it seven days ago

`coverage.py`'s UTF-8 probe was written on `pc-rpgmakervxace-doc`. It decodes
the head of a file and then requires every character to be printable:

```python
return all(c.isprintable() or c in "\t\r\n　" for c in s)
```

**U+FEFF is not printable.**

```
python _work/bomcheck.py                            (_work/bomcheck.txt)

'﻿'.isprintable()                          : False
the probe accepts BOM-less UTF-8                : True
the probe accepts the SAME text with a mark     : False

files beginning EF BB BF in this tree
  filed OPAQUE            : 190 files, 1,108,362 bytes
  filed as something else : 0 files, 0 bytes
    .txt 150 / 738,171     .html 39 / 352,747     .css 1 / 17,444
```

**Zero of 190 got through.** It is not a partial failure; for a file carrying a
byte-order mark the probe fails on the first character, every time, and the
population is 190 of 190.

**It was found by pointing the tool at the next object, which is the only way a
defect of this shape is ever found.** `pc-rpgmakervxace-doc/docs/15` wrote P19
about exactly this — *name the one thing a new tool would fail to notice, and
write the check before pointing the tool at the object* — and that session named
**four** blind spots for `coverage.py`. This was not one of them. **P19's
mechanism is sound and its coverage was four out of at least five**, and
[15](15-prediction-scoring.md) scores it that way rather than burying it in a
table of inherited defects.

### The repair, which is one line and two of comment

```python
# U+FEFF is a byte-order mark ... A leading byte-order mark is a
# signature and not a character: it is removed before the text is
# judged, and a U+FEFF anywhere else still counts against the file.
if s[:1] == "﻿":
    s = s[1:]
```

**And it is proved by subtraction and not by assertion.** The two committed
coverage tables differ on the UTF-8 row by exactly the population:

```
before   plain text, UTF-8   104 files    2,182,962 bytes
after    plain text, UTF-8   294 files    3,291,324 bytes
         104 + 190 = 294        2,182,962 + 1,108,362 = 3,291,324
```

Both at residue 0.

### The checks, and the first one fails without the repair

Eight were added, and they are in `coverage.py selftest`:

| check | what it stops |
|---|---|
| `'﻿'.isprintable() is False` | the defect's cause, asserted so nobody has to remember it |
| **UTF-8 text WITH a mark is SPECIFIED** | **fails without the repair** |
| and it is still *named* UTF-8 | a repair that reclassifies is not a repair |
| a mark followed by ASCII is UTF-8 and not ASCII | the mark is a high byte; the ASCII probe must not take it |
| the same text without a mark still passes | the repair does not break the case that worked |
| a mark followed by **binary** is still refused | the repair strips a signature, it does not excuse a file |
| a lone mark and nothing else is **not** text | an empty document is not a document |
| a U+FEFF **in the middle** still counts against the file | the repair is about position 0 and says so |

---

## Five magics, and the ordering rule that governs them

`pc-rpgmakervxace-doc/docs/04` established the rule and `_ordering_ok()`
enforces it: **every binary signature is tested before every text codec.** The
rule exists because a 328,733-byte PDF was once filed as Shift-JIS text, and the
selftest asserts both that the rule holds and that a violation of it is
detected.

The five added here go **above** that line:

| probe | bucket | what makes it a signature and not a guess |
|---|---|---|
| **MPEG-4 / ISO base media** | specified | `ftyp` at offset 4 **and** a plausible box size in front of it: 16 ≤ size ≤ 1024. Four letters alone is the weakest entry in the table and the size word is what makes it an entry |
| **ELF** | specified | `7F 45 4C 46`, then `EI_CLASS` in {1,2}, `EI_DATA` in {1,2}, `EI_VERSION` = 1 |
| **Mach-O** | specified | four thin magics, plus the two fat ones — see below |
| **Unix `ar`** | specified | `!<arch>\n`, all eight bytes including the newline |
| **Chromium `.pak`** | **decoded** | an equation, and it is argued below |

### The four-byte hazard, and it is tested

**`CA FE BA BE` is a Mach-O universal binary and it is also a Java class file.**
Nothing in the first four bytes separates them. The next four do:

* Mach-O puts `nfat_arch` there — the number of architectures in the archive,
  which is one or two in practice and has never been twenty;
* a class file puts `minor_version` then `major_version`, read together as one
  big-endian word. **`major_version` has been at least 45 since Java 1.0 in
  1996**, so the smallest value a class file can show is 45.

**20 < 45 and the ranges do not touch.** The probe accepts 1..20 and the
selftest asserts that a class file at major 52 and a class file at major 45 are
both refused. **A classifier that filed a Java class file as an executable would
be wrong in a way no byte count would reveal**, which is why this is three
checks and not a comment.

### The `.pak` signature is an equation

There is no byte string to match. The whole header is a small integer, and what
makes it a signature is that the header declares how many entries follow, so the
entry table's first offset **must** be exactly where the header ends:

```
v4   9 + (resources + 1) * 6
v5  12 + (resources + 1) * 6 + aliases * 4
```

Both layouts end in a sentinel entry, which is the `+ 1`. **On this object the
equation holds on 222 of 222 files.** A four-byte little-endian 5 followed by
nothing structural is refused, and so is a file whose first offset is anything
else — and both refusals are checks.

---

## The bucket decision, which is the second of this session's two

`pc-rpgmaker2000-doc/docs/09` defines the four buckets. **SPECIFIED** is a
format whose producer published a description. **DECODED** is a format that can
be read and whose producer published none — the bucket ITSF went into, and it
has been **empty since `pc-rpgmaker2003-doc`, four objects ago**.

**The Chromium `.pak` goes in DECODED, and the case is not quite ITSF's.**

| | ITSF | Chromium `.pak` |
|---|---|---|
| a specification document | none | **none** |
| the producer's own reader, published | no | **yes** — `ui/base/resource/data_pack.cc` is open source |
| independent third-party readers | yes | yes |
| a versioned, stable grammar | no | **no** — the version field has gone 1, 2, 3, 4, 5 and none of the changes is described anywhere but in a diff |

**Published source is not a specification, and the distinction is the one this
pipeline has been making since the 2000.** A specification is a promise to a
reader: it says what the format is, it survives the implementation, and it can
be checked against. Source code is a description of one implementation at one
commit; it can be read, and reading it produces a decoding rather than a
warrant.

**So the test `pc-rpgmaker2000-doc/docs/09` wrote — "no such document exists" —
is met, and the bucket is DECODED.** What would move it to SPECIFIED is a
published document from Google describing the layout and its version history,
and naming that is the honest way to hold the position.

**And a bucket that has been empty for four objects is worth one sentence more
than the decision.** DECODED exists to mark the difference between *somebody
worked this out* and *the producer told us*. Four consecutive objects had
nothing in it because four consecutive objects were either fully documented or
fully opaque. **This one has 222 files and 89,662,863 bytes in the middle**, and
the middle is where the bucket earns its keep.

---

## The table, before and after

```
                          before                  after
specified     7,806 / 2,100,016,569    9,384 / 2,786,158,378
decoded             0 /           0      222 /    89,662,863
derived             0 /           0        0 /             0
opaque        1,835 /   825,473,140       35 /    49,668,468
              9,641 / 2,925,489,709    9,641 / 2,925,489,709   residue 0
```

**1,800 files and 775,804,672 bytes moved out of OPAQUE**, of which 190 files
and 1,108,362 bytes moved because of a defect this pipeline wrote.

**What remains opaque is 35 files in four families**, and every one of them
belongs to a third party: **4 ICU data archives** (40,494,112 bytes, the Unicode
consortium's), **24 Qt translation catalogues** (4,873,554, Digia's), **6 V8
snapshot blobs** (4,300,802, Google's), and **one zero-byte file**. 4 + 24 + 6 +
1 = 35 and the bytes sum to 49,668,468 at residue 0.

**The zero-byte file is the first this pipeline's coverage table has had to
classify.** It is `tutorial-osx/TutorialGui.app/Contents/Resources/empty.lproj`,
and it is opaque because a file with no bytes has no signature — which is the
correct answer and not a gap. A classifier that guessed at it would be guessing
at nothing.

---

## The selftest

```
python tools/coverage.py selftest            (notes/selftest-coverage.txt)
95 checks, 0 failures
```

**Fifty checks were added**, of which **eight assert a refusal or a
non-confusion** — the Java class file twice, the absurd box size, the malformed
ELF twice, `!<arch>` without its newline, a `.pak` whose arithmetic fails, and a
byte-order mark in front of binary. The selftest was run with
`PYTHONIOENCODING` unset, which is the condition
`pc-rpgmakervxace-doc/docs/12` established after a Japanese file name killed
four tools that had passed under it.
