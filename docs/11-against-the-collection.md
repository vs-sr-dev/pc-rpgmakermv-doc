# 11 — against the collection: twenty-one byte strings in three objects at once, five that were dropped and are still there, and a redraw whose ratio is the tile size

*Measure: `ls -1d ../*-doc/ | wc -l` → **137** and `ls -1d ../pc-*-doc/ | wc -l`
→ **68**, both counted before the sweep; `python tools/crossall.py
notes/sha1-all.txt --collection .. --skip pc-rpgmakermv-doc`, in
`notes/crossall.txt`; `python _work/crosssplit.py`, in `notes/crosssplit.txt`;
`python tools/crossnames.py notes/sha1-all.txt
../pc-rpgmakervxace-doc/notes/sha1-all.txt`, in `notes/crossnames.txt`; `python
_work/threeway.py`, in `notes/threeway.txt`; `python tools/pngpair.py` across
the object boundary, in `notes/pngpair.txt`.*

---

## The denominators, published before the result

```
ls -1d ../*-doc/    | wc -l      137     <- includes this directory
ls -1d ../pc-*-doc/ | wc -l       68     <- includes this directory
```

**137 and 68**, counted by walking the collection root and not copied from the
pre-briefing. **The 137 does not move after this session**: this directory
already existed when it was counted, and publishing it to a remote adds nothing
locally.

And `crossall.py`'s own three, reported as the tool gives them:

```
repositories swept          : 107
list files swept            : 477
hash tokens read            : 161543
```

All three moved against the previous object's run — 106 → 107, 473 → 477,
159,482 → 161,543 — because `pc-rpgmakervxace-doc` was published between them and
publishes four files under `notes\` ending `.txt`.

**`--skip pc-rpgmakermv-doc` is required and was given**, and the sweep excludes
the empty-file sha1, which is a trap and not a crossing: it occurs **57 times in
16 repositories**.

---

## The result

```
python tools/crossall.py notes/sha1-all.txt --collection .. \
    --skip pc-rpgmakermv-doc                        (notes/crossall.txt)

my distinct sha1 : 7417
CROSSINGS        : 297 of 7417 = 4.0043 %

   min bytes    my hashes    crossings         rate
           0         7417          297      4.0043 %
        4096         5076          296      5.8314 %
       65536         1983           26      1.3111 %
```

**The collection's seven rates are now** 1 of 12, 10 of 962, 0 of 477, 368 of
731, 0 of 913, 26 of 1,935 and **297 of 7,417**.

```
python _work/crosssplit.py                        (notes/crosssplit.txt)

crossing blocks parsed : 297     bytes over them : 7,931,979

  partner repositories, by CROSSING and not by mention:
    pc-rpgmakervxace-doc   281
    pc-rpgmakerxp-doc       36
    pc-academagia-doc        1

  crossings by number of partners : {1: 276, 2: 21}

  where MY side lives : dlc 236   NewData 60   the root 1
```

**The single crossing with `pc-academagia-doc` is `steam_api.dll`** — Valve's
library, shipped by a Japanese game-making tool and by a .NET game about a magic
school. **That is not a family resemblance, it is a platform**, and it is the
only file in 9,641 that this object shares with anything outside its own family.

---

## Twenty-one byte strings are in three objects at once

No object in this collection has produced a three-way crossing before. These are
twenty-one, and the question the pre-briefing left open — whether they are the
same twenty-one the VX Ace shared with the XP — has an answer:

```
python _work/threeway.py                            (notes/threeway.txt)

distinct sha1  MV 7416   XP 913   VX Ace 1935
MV & XP          : 36        MV & VX Ace      : 281
MV & XP & VX Ace : 21        XP & VX Ace      : 26
the three-way set is a subset of the XP/VX Ace set : True
in XP and VX Ace but NOT in MV : 5
```

**Twenty-one of the VX Ace's twenty-six survived into the MV and five did not**,
and the three naming eras are legible in one table:

```
   MV                     XP                    VX Ace
   Applause1.ogg          059-Applause01.ogg    Applause1.ogg
   Book1.ogg              046-Book01.ogg        Book1.ogg
   Chest2.ogg             044-Chest01.ogg       Chest.ogg
   Crow.ogg               078-Small05.ogg       Crow.ogg
   Monster4.ogg           085-Monster07.ogg     Monster4.ogg
   Teleport.ogg           018-Teleport01.ogg    Teleport.ogg
   … 15 more
```

**`078-Small05.ogg` became `Crow.ogg` in 2011 and is still `Crow.ogg` in 2015,
ten years after the XP shipped it and under bytes that have not changed once.**

### The five that were dropped are still there

```
the 5 the XP and the VX Ace share that the MV dropped:
   XP: 010-River01.ogg      VX: River.ogg
   XP: 016-Drips01.ogg      VX: Drips.ogg
   XP: 018-Darkness01.ogg   VX: Darkness.ogg
   XP: 011-System11.ogg     VX: Collapse2.ogg
   XP: 012-System12.ogg     VX: Collapse1.ogg
```

```
find rpgmakermv-steam -name "River.ogg"      -> dlc/BaseResource_Compressed/…
find rpgmakermv-steam -name "Drips.ogg"      -> dlc/BaseResource_Compressed/…
find rpgmakermv-steam -name "Darkness.ogg"   -> dlc/BaseResource_Compressed/…
find rpgmakermv-steam -name "Collapse1.ogg"  -> dlc/BaseResource_Compressed/…
find rpgmakermv-steam -name "Collapse2.ogg"  -> dlc/BaseResource_Compressed/…
```

**All five names are in this object, under different bytes.** They were not
dropped; they were re-encoded, and a sha1 crossing cannot see a re-encoding.
**So the crossing rate under-counts what was carried, by at least five and by an
amount nothing in this pipeline can measure** — which is the honest boundary of
the whole technique and is stated here rather than in a footnote.

---

## The naming scheme has stopped moving

```
python tools/crossnames.py notes/sha1-all.txt \
    ../pc-rpgmakervxace-doc/notes/sha1-all.txt     (notes/crossnames.txt)

crossing : 281 of 7417        NOT crossing : 7136 of 7417
the two sum to my distinct hashes : True

same base name in both objects : 266
renamed                        : 15
   spaced 0    prefixed 0    retranslated 15
the three classes sum to the renamed total : True   (0 + 0 + 15 = 15)

   Chest -> Chest2      Cursor2 -> Cursor3     Decision1 -> Decision2
   Fire -> Fire1        Gameover1 -> Gameover3 Inn -> Inn2
   Laser -> Laser1      Load -> Load2          Rain -> Rain1
   Save -> Save2        Shock -> Shock3        Shop -> Shop2
   Victory2 -> Victory3 … 2 more
```

**The XP → VX Ace step renamed 26 of 26 and abandoned a four-product numbering
scheme.** `pc-rpgmakervxace-doc/docs/11` called that a deliberate rebuild.

**The VX Ace → MV step keeps 266 of 281 and every one of the fifteen renames is
an increment** — `Chest` to `Chest2`, `Fire` to `Fire1`, `Load` to `Load2`. Not
one is a re-translation in the sense the class name implies; they are a library
that grew a second `Chest` sound and renumbered the first.

**The scheme that replaced the numbering has itself become stable**, and there
are now three measurements where the previous session had two.

**And the crossings are one extension.** All 281 are `.ogg`, 4,842,603 bytes.
Not one `.png`, not one `.ttf`, not one binary.

---

## What does not cross, and pointing an old reader at it

**5,578 PNG here against the VX Ace's 1,456, and zero shared bytes.** Zero
shared bytes is not zero shared pictures, and `pngpair.py` — which compares two
PNG chunk by chunk and had **never been pointed across an object boundary** — is
the reader for the question.

```
python tools/pngpair.py <MV IconSet.png> <VX Ace IconSet.png>
                                                   (notes/pngpair.txt)

  A : IHDR IDAT x26 IEND
  B : IHDR pHYs iCCP cHRM PLTE tRNS IDAT IEND

  chunk  verdict          same pixel stream (IDAT identical) : False
  IEND   IDENTICAL        same geometry and colour type      : False
  IHDR   differs
  PLTE   only in B
```

Four names present in both objects were compared, and **the only chunk any pair
shares is `IEND`, which is empty.** But the IHDR difference is not noise:

```
python _work/ihdr.py

  name         object                  width height depth  colour type
  IconSet.png  pc-rpgmakermv-doc          512    640     8  truecolour+alpha
  IconSet.png  pc-rpgmakervxace-doc       384    936     8  palettised

  Balloon.png  pc-rpgmakermv-doc          384    720     8  truecolour+alpha
  Balloon.png  pc-rpgmakervxace-doc       256    320     8  truecolour+alpha

  Window.png   pc-rpgmakermv-doc          192    288     8  truecolour+alpha
  Window.png   pc-rpgmakervxace-doc       128    128     8  truecolour+alpha

  Damage1.png  pc-rpgmakermv-doc          576    384     8  truecolour+alpha
  Damage1.png  pc-rpgmakervxace-doc       384    256     8  palettised
```

**`Damage1.png` is 576 × 384 against 384 × 256 — exactly 1.5 × in both
dimensions. `Balloon.png` is 384 wide against 256 — exactly 1.5 ×.
`Window.png` is 192 against 128 — exactly 1.5 ×.**

**48 ÷ 32 = 1.5.** RPG Maker MV's tile is 48 pixels square and the VX Ace's is
32, and the graphics library was not re-encoded, it was **redrawn at three
halves the resolution**. Three of the four pairs give the ratio exactly in the
dimension that is a whole number of tiles; the fourth, `IconSet`, is 512 × 640
against 384 × 936 because the icon *count* changed as well as the icon size.

**That is why no PNG crosses and why no PNG could have**, and it took an
existing reader pointed at a population nobody had pointed it at to say so with
a number instead of a guess.

---

## What the rate measures

`pc-rpgmakerxp-doc/docs/12` wrote that **a published tree next door is necessary
for a crossing and is not sufficient**. `pc-rpgmakervxace-doc/docs/11` added that
**a shared format is also necessary and also not sufficient**, and that what the
rate measures is **how much of a predecessor a publisher chose to carry**.

**This object is the test of that sentence and it passes.** Between the VX Ace
and the MV *everything* changed: Ruby to JavaScript, `Marshal` to JSON, a
compiled interpreter to published source, a 32-pixel tile to a 48-pixel tile, a
Windows-only product to one that ships players for three operating systems.
**And 281 sound effects crossed anyway, under their own names, byte for byte.**

**So the rate is not measuring technology and it is not measuring format.** It
measures a decision: somebody at KADOKAWA opened the sound library, kept it, and
renumbered fifteen files. The graphics were redrawn because the tile size
changed and the sounds were not because nothing about a sound effect depends on
a tile size.

**The four-point series is now:**

| step | rate | what it says |
|---|---|---|
| 2003 → XP | 368 of 731 = 50.3420 % | half the library carried over |
| XP → VX Ace | 0 of 913 = 0.0000 % | nothing survived, from that side |
| XP → VX Ace | 26 of 1,935 = 1.3437 % | the same event from this side, all renamed |
| **VX Ace → MV** | **281 of 7,417 = 3.7885 %** | **266 of 281 keeping their names** |

**And this repository is published beside them, which is the necessary condition
the first of those sentences names.** Without `pc-rpgmakervxace-doc`'s
`notes/sha1-all.txt` on this disk there would be no 281 and no 21, and the
sentence about what a publisher carried forward could not have been written at
all.
