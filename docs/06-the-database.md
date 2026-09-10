# 06 — the database: a convention that survived a change of serialisation, five records that are not the five the join names, and an engine that reads all but seventeen of its own fields

*Measure: `python _work/jsonprobe.py`, in `_work/jsonprobe.txt`; `python
tools/jsondiff.py rpgmakermv-steam/NewData_FantasyEN/data
rpgmakermv-steam/NewData_FantasyJP/data --expect-agreeing 8`, in
`notes/jsondiff-fantasy.txt`; `python _work/itemseries.py`, in
`notes/item-series.txt`; `python _work/enginejs.py`, in `notes/engine-js.txt`;
`python _work/keysjoin.py`, in `notes/keys-join.txt`. `jsondiff.py`'s selftest
is 15 checks, 0 failures, run with `PYTHONIOENCODING` unset.*

---

## The format, and there is nothing to recover

```
python _work/jsonprobe.py

JSON files in the tree : 129        bytes : 4,286,178
parse cleanly as JSON  : 128 of 129       refuse : 1
root types             : {'list': 83, 'dict': 45}
arrays whose element 0 is null : 83 of 83
```

**`pc-rpgmakerxp-doc/docs/07` inflated ninety Deflate streams out of an
encrypted archive to recover 538,811 bytes of commented Ruby.
`pc-rpgmakervxace-doc/docs/05` wrote a `Marshal` 4.8 reader to get at a map.
Here the equivalent operation is `json.load`, and the equivalent of reading the
scripts is `cat`.**

That is worth saying once and not building a chapter on. **What is worth a
chapter is what the openness lets you check**, and there are three things.

---

## The convention survived a complete change of serialisation

**Every one of the 83 JSON arrays has `null` at index 0.**

`pc-rpgmakerxp-doc/docs/06` counted **twelve of thirteen** Ruby `Marshal` arrays
doing exactly that, and `pc-rpgmakervxace-doc` found the same. Those were binary
dumps of Ruby objects. **These are UTF-8 text produced by a different program in
a different language a decade later, and the convention is unbroken.**

It is not an encoding artefact and cannot be: JSON has no notion of a 1-based
array, and writing `null` at index 0 costs four bytes and a comma in every one
of the 83 files. **It is a statement about the object model** — records are
numbered from 1, the id equals the index, and index 0 is reserved so that 0 can
mean *none*. The engine agrees: `jsondiff.py` checks that `id` equals the index
rather than assuming it, and reports where it does not.

---

## The two Fantasy databases, and eight files of nine agree

`NewData_FantasyEN\data\` and `NewData_FantasyJP\data\` are one database in two
languages, nine files each under the same nine names.

```
python tools/jsondiff.py …FantasyEN/data …FantasyJP/data --expect-agreeing 8
                                              (notes/jsondiff-fantasy.txt)

  file             A recs B recs   same A only   B only   differ
  Actors.json           8      8    yes      0        0        8
  Armors.json         100    100    yes      0        0       86
  Classes.json          8      8    yes      0        0        8
  Enemies.json         20     20    yes      0        0       11
  Items.json           35     30 **NO**      5        0       25
  Skills.json         235    235    yes      0        0      149
  States.json          30     30    yes      0        0       27
  Troops.json          20     20    yes      0        0       14
  Weapons.json         50     50    yes      0        0       40

files whose record COUNT agrees : 8 of 9
records, A 506   B 501   difference 5
```

**The pre-briefing says 36 and 31 and the counts are 35 and 30.** It counted the
array length, and every one of these arrays carries `null` at index 0 — so its
two figures are each one too large. **The difference of five is unchanged**, and
that is [13](13-corrections.md) A.3.

**And the tool splits the differences by field type, which is the only way the
table means anything.** These are two *languages* of one database, so almost
every record differs in `name` and `description` by construction:

```
  file               differ    numeric string only  commonest fields
  Actors.json             8          0          6   name 8, equips 2
  Armors.json            86          0         85   name 86, description 82
  Skills.json           149          0        147   name 149, description 146
  Weapons.json           40          0         40   description 40, name 40
```

**Not one record in any of the nine files differs only in a numeric or
structural field.** Every difference the join finds is a translation or a
translation plus something; there is no record whose price or damage formula
was changed between the two language editions. That is a statement about how
the two were made — **one database, translated, and not two databases** — and it
is a count and not an impression.

---

## The five records are not the five the id join names

The id join says the English-only ids are **31, 32, 33, 34 and 35**, at the tail
of the array. That is the correct output of an id join and **the wrong answer to
the question**, and the object says so itself:

```
python _work/itemseries.py                          (notes/item-series.txt)

EN, effect code 42 (permanent parameter growth):
  id 28  icon 32  price 3000  dataId 0 (MHP)  value 50  'Life Increase'
  id 29  icon 33  price 3000  dataId 1 (MMP)  value 10  'MP Increase'
  id 30  icon 34  price 3000  dataId 2 (ATK)  value  3  'Power Increase'
  id 31  icon 35  price 3000  dataId 3 (DEF)  value  3  'Guard Increase'
  id 32  icon 36  price 3000  dataId 4 (MAT)  value  3  'Magic Increase'
  id 33  icon 37  price 3000  dataId 5 (MDF)  value  3  'Resistance Increase'
  id 34  icon 38  price 3000  dataId 6 (AGI)  value  3  'Speed Increase'
  id 35  icon 39  price 3000  dataId 7 (LUK)  value  3  'Luck Increase'

JP, the same:
  id 23  icon 32  price 3000  dataId 0 (MHP)  value 50  'ライフアップ'
  id 24  icon 33  price 3000  dataId 1 (MMP)  value 10  'マナアップ'
  …
  id 30  icon 39  price 3000  dataId 7 (LUK)  value  3  'ラックアップ'
```

**The eight-item growth series exists complete in both files** — the same eight
parameters, the same eight icons, the same eight prices and the same eight
values — **at ids 28 to 35 in English and 23 to 30 in Japanese.** The two
databases are offset by exactly five from id 23 onwards.

**So the five extra English records are earlier in the array, and everything
after them is displaced.** The id is a positional index; an insertion shifts it;
and a join on an index that moves answers a question nobody asked.

**The right join is by the fields a translator does not touch.** Aligning on
every field except `name`, `description` and `note` puts the eight-item series
in one-to-one correspondence across the two files and leaves the five genuinely
unmatched records where they actually are. **This chapter reports the
displacement rather than the five ids**, because the displacement is the finding
and the five ids are an artefact of the tool — and `jsondiff.py`'s docstring
names this as the thing it would not notice, in advance, per P19.

---

## One file called `.json` is two documents

```
python _work/jsonbad.py

REFUSED : dlc/KadokawaPlugins_New/additional/animations.json
  bytes : 31938
  the error : Extra data: line 1 column 7012 (char 7011)
  parses under utf-8 / utf-16 / cp932 / latin-1 : no, four times
```

**The first document ends at byte 7,011 and another begins.** It is
concatenated JSON in a file whose extension says one document, shipped inside a
DLC. `jsondiff.py` refuses it and prints the parser's own reason rather than
guessing at a delimiter, and its selftest asserts that refusal.

---

## The engine, and it names 266 of the 283 fields its database uses

```
python _work/enginejs.py                            (notes/engine-js.txt)

  file                     bytes    lines  comment   blank  classes  methods
  rpg_core.js             235076     9321     3343     826       28      458
  rpg_managers.js          81146     2839       50     377       10      330
  rpg_objects.js          293675    10641      294    1477       30     1376
  rpg_scenes.js            78715     2689      265     391       21      343
  rpg_sprites.js           77867     2691       78     360       18      318
  rpg_windows.js          176619     6024      191     932       46      834
  TOTAL                   943098    34205     4221    4363      153     3659
```

**943,098 bytes, 34,205 lines, 4,221 of them comment, 153 class names and 3,659
methods**, plus 1,378,836 bytes of libraries of which `pixi.js` is 1,295,220.
The first line of `rpg_core.js` is `// rpg_core.js v1.6.2`, and `RPGMV.exe`'s
version resource says **1.6.3** — see [09](09-the-programs.md).

**And the openness supports a join nothing else in this collection has
supported.** The engine is text and the database is text, so the two can be
asked whether they agree about what a record contains:

```
python _work/keysjoin.py                            (notes/keys-join.txt)

distinct object keys, over 128 parsed documents and at every depth : 283
database keys the engine source names : 266 of 283
keys the engine never names           : 17
   armorTypes chromium-args editMapId elements expanded icon js-flags
   main order parallaxShow parentId releaseByDamage scrollX scrollY
   toolbar weaponTypes window
```

*(The pre-briefing's 153 is a count of keys at the record's own level; 283
counts every depth. Two denominators, both correct, and the chapter uses the
deeper one because the question is about fields the engine reads.)*

**The seventeen split cleanly into two groups and neither is a gap in the
engine.** `chromium-args`, `js-flags`, `main`, `toolbar`, `window` and `icon`
are **NW.js manifest keys** and belong to `package.json`, which is not a
database file at all — the census swept every `.json` in the tree and these came
with it. The other eleven — `armorTypes`, `weaponTypes`, `elements`,
`editMapId`, `expanded`, `order`, `parentId`, `parallaxShow`, `scrollX`,
`scrollY`, `releaseByDamage` — **are the editor's**: they describe how a map
looked in the editing window and what the drop-down lists offer, and the runtime
has no reason to read them.

**So the database carries fields the engine does not, and 266 of 283 is the
measure of the overlap.** On the previous object this question could only be
asked in one direction — `pc-rpgmakervxace-doc/docs/06` matched 75 instance
variables against a manual — and here both sides are open at once. **That is
what an object that stops hiding actually buys**, and it is one join and not a
smaller amount of work.
