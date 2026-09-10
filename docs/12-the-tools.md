# 12 — the tools: a defect this pipeline shipped seven days ago, a harness carrying a sentence about a different object, and two hundred and twenty-seven readers nobody has aimed

*Measure: `python tools/toolsdiff.py ../pc-rpgmakervxace-doc/tools`, in
`notes/toolsdiff.txt` and `notes/toolsdiff-before.txt`; `python
tools/toolscan.py`, in `notes/toolscan.txt`; `python tools/refusals.py
rpgmakermv-steam` and `python tools/refusalclass.py notes/refusals.txt`, in
their notes and their `-before` counterparts; `python tools/dirguard.py --survey
--tools tools` and `python tools/nameguard.py --survey --tools tools`, in theirs;
`python _work/p22list.py`, in `notes/p22-list.txt`; the nine selftests in
`notes/selftests.txt`.*

---

## The box, before and after

```
python tools/toolsdiff.py ../pc-rpgmakervxace-doc/tools --expect-differing 0
                                              (notes/toolsdiff-before.txt)
mine : 562 .py   theirs : 562 .py   common : 562   differing : 0

python tools/toolsdiff.py ../pc-rpgmakervxace-doc/tools
                                                   (notes/toolsdiff.txt)
mine : 568 .py   theirs : 562 .py
only mine   : audiopair.py, chpak.py, jsondiff.py, mp4box.py,
              predmeasure.py, regcheck.py
only theirs : none
common      : 562    differing   : 4
   coverage.py   oggcensus.py   refusals.py   vendorhash.py
```

**Six written, four modified, 558 inherited unchanged.**
`toolscan.py`: **568 files, 0 forbidden control bytes, all three positive
controls firing.**

| tool | checks | what it is for |
|---|---:|---|
| `coverage.py` | **95** | +50: the byte-order-mark repair and five magics |
| `vendorhash.py` | **42** | +16: nine vendors and the coverage survey |
| `mp4box.py` | **31** | the ISO base media box tree and its sample table |
| `regcheck.py` | **20** | P20's register membership, as a program |
| `chpak.py` | **19** | Chromium's `.pak`, walked by its own arithmetic |
| `audiopair.py` | **15** | one recording in two containers |
| `jsondiff.py` | **15** | two directories of JSON, joined by key |
| `oggcensus.py` | 15 | +0 checks, but its file selection repaired |
| `predmeasure.py` | **13** | P21's measurement count |
| **total** | **265** | **0 failures** |

**Every selftest was run at least once with `PYTHONIOENCODING` unset**, which is
the condition `pc-rpgmakervxace-doc/docs/12` established after a Japanese file
name killed four tools that passed under it. **Every new name was checked
against `tools/` before the file was written** — `mp4box.py` because `mp4.py`
and `m4a.py` were candidates, `chpak.py` because `pak.py` would have collided
with nothing but reads worse. **Every tool that selects files selects them by
magic**, and where an inherited one did not, that is a repair below.

---

## The defect this pipeline shipped seven days ago

`coverage.py`'s UTF-8 probe, written on the previous object, **refused 190 UTF-8
files because U+FEFF is not printable**. [04](04-the-magic-table.md) has the
repair and the arithmetic that proves it; what belongs here is what it says
about P19.

**`pc-rpgmakervxace-doc/docs/15` named four blind spots for `coverage.py` in
advance and this was not one of them.** The one it named for that tool — *a text
codec accepting a binary header* — fired, and produced the `ambiguity` mode and
the PDF repair. **So P19's mechanism worked on the blind spot it named and was
silent on the one it did not**, which is what a prescription of that shape can
be expected to do and is not a failure of it.

**What it is, is the best case P19 has produced**, because it is a defect that
existed for exactly one object and was found the only way a defect of that shape
can be: **by pointing the tool at the next object.** A tool that classifies
2,026 files correctly and 190 of 9,641 incorrectly cannot be caught by any
amount of staring at the tool. **The check that would have caught it is one line
long and now exists**, and the repair's selftest fails without it.

---

## The harness carried a sentence about a different object

`refusals.py`'s row for `zaccount.py` read:

```python
("zaccount.py", ["%ROOT%"], "a ZIP walked structurally; there is no ZIP "
                            "in this object"),
```

**`rpgmakermv-steam/nwjs-osx-unsigned.zip` is 205,182,933 bytes.**

The sentence was true of `pc-rpgmaker2000-doc` and was frozen into a harness that
is pointed at a different object every session. **It is the `%RXDATA%` defect
`pc-rpgmakervxace-doc/docs/12` repaired, in a different row of the same table**:
there, a placeholder resolved by extension named a file that did not exist and
two readers were reported as refusing when they were being aimed wrong; here, a
*description* carried an assertion about a tree the harness is no longer looking
at.

**The repair is the same in kind.** The row now uses a `%ZIP%` placeholder
**resolved by magic**, and its description says what the tool is for and nothing
about what the object contains. Two more magic placeholders were added — `%MP4%`
and `%PAK%` — and **their first run resolved to "no file of that magic in this
tree" over a tree full of both**, because the resolver read eight bytes and a
File Type Box needs twelve and a `.pak` header twenty. That is
[13](13-corrections.md) C.3 and the read is now 32 bytes.

**And `zaccount.py` turned out to be the wrong tool for the job.** It is a
four-layer accounting bound to one object's InstallShield structure and needs a
directory of extracted members; **the tool that walks an arbitrary ZIP is
`zipdir.py`**, which was in the box, had never been pointed at this object, and
is on P22's list. [07](07-the-runtime.md) uses what it found.

---

## `oggcensus.py` selected by extension, and a check written for a new tool caught it

`audiopair.py`'s selftest asserts, before the tool is ever pointed at the object,
that **a file named `.ogg` which is not an Ogg is not collected**. It failed —
not in `audiopair.py` but in `oggcensus.ogg_files`, which filtered on `.ogg`.

**That is `mzcensus.py`'s thirteenth-appearance defect living inside a tool
written in the session that catalogued it**, and it is the shape P22 describes
exactly: an existing tool, a check written for a new one, and a defect that
nothing else would have found.

**The repair selects by magic** — `OggS` and a zero version byte, RFC 3533 —
and costs five bytes of every file in the tree. **On this object it changes
nothing: 1,341 of 1,341 both ways.** A repair that changes no number is still a
repair, because what it changes is what the number means.

---

## The refusal harness

```
python tools/refusals.py rpgmakermv-steam        (notes/refusals-before.txt)
readers pointed : 85    refused : 56    exited 0 : 29

python tools/refusalclass.py notes/refusals-before.txt
  argparse   23     oserror   17     format   15     exception   1
  the four classes sum to the refusal total : True
```

**`argparse` is 23 for the seventh time** in the pre-briefing's own run. A
reader whose command line does not accept a bare path reports an `argparse`
error and **reads no byte of the object**, so 23 of 56 refusals are statements
about a command line. Nobody has repaired it, including this session, and the
reason is that repairing it means editing 23 tools' argument parsers to agree on
a convention none of them was written to.

```
python tools/refusals.py rpgmakermv-steam               (notes/refusals.txt)
readers pointed : 92    refused : 54    exited 0 : 38

python tools/refusalclass.py notes/refusals.txt    (notes/refusalclass.txt)
  argparse   23     oserror   17     format   13     exception   1
  the four classes sum to the refusal total : True
  argparse share of the refusals : 23 of 54 = 42.5926 %
```

**Seven readers were added to the table — the six written here and `zipdir.py`
— and all seven exit 0 as the table says they must.** The denominator moves from
85 to 92 and the refusals fall from 56 to 54.

**`argparse` is 23 for the EIGHTH time**, on the eighth population, over a
denominator that has now moved three times without moving it. **Twenty-three is
not a property of any object**; it is the number of readers in this box whose
argument parser will not accept a bare path, and it has been constant since it
was first counted.

**And `format` falls from 15 to 13.** `chpak.py`, `mp4box.py` and
`predmeasure.py` were in that bucket on the run before the placeholders were
repaired — they were refusing because the harness handed them a path that did
not exist — and `zaccount.py` left it because the row now points it at its own
selftest. **Four rows moved out of `format` and not one of them was a fact about
the object**, which is the same lesson `pc-rpgmakervxace-doc/docs/12` drew from
`%RXDATA%` and is why that lesson needed repeating in a different row.

**And two refusals are the tool working and are reported as such:**

```
python tools/marshal48.py walk rpgmakermv-steam       (notes/marshal48.txt)
marshal48: no file under 'rpgmakermv-steam' begins with the Marshal 4.8
signature -- refusing to report a clean table over an empty population

python tools/chmx.py check rpgmakermv-steam                (notes/chmx.txt)
chmx: rpgmakermv-steam is a directory; this reader wants one .chm file
```

**Both are correct and both say why.** `marshal48.py` refuses because it selects
by magic — the repair `pc-rpgmakervxace-doc` made — and there is no Ruby
`Marshal` in 9,641 files. `chmx.py` refuses through `dirguard.py` because it
wants one file and there is no `.chm` to hand it. **A reader that returned an
empty table for either would be worse than one that refuses**, and these two are
the evidence that the repairs of the last two sessions hold.

**Eight readers have no population here and that is one line and not eight**:
`chmclocks.py`, `itsf.py`, `lzx.py`, `rgssjoin.py`, `rvmap.py`, `tiletable.py`,
`rgssdb.py` and `rxscripts.py` are for `.chm`, LZX, RGSS3 maps and tileset
tables, and this object has none of those things.

---

## The guards, and two of this session's own tools failed one

```
python tools/dirguard.py --survey --tools tools
  before : 561 surveyed, 216 raised          (notes/dirguard-survey-before.txt)
  after  : 567 surveyed, 216 raised               (notes/dirguard-survey.txt)
```

**216 was the number to beat and the number to hold.** The first run after the
six new tools were written reported **218**, and the two extra were
`regcheck.py` and `predmeasure.py`, both raising `PermissionError` on a
directory — **the 217th and 218th instances of the class `dirguard.py` exists to
close, written by the session that ran the survey that caught them.**

Both now take `dirguard.want_file()` and the figure is back to 216. That is
[13](13-corrections.md) C.4, and it is worth stating plainly: **a survey run as a
P17 register entry, for the purpose of having a before-figure, caught a defect
in code that did not exist when it was run.**

```
python tools/nameguard.py --survey --tools tools
  before : 7 raised, 3 printed safely, 551 not tested   (7 of 10 = 70.0000 %)
  after  : 7 raised, 3 printed safely, 557 not tested
```

**Unchanged, and the denominator moved from 561 to 567 without the numerator
moving.** Every new tool that prints a recovered name calls `nameguard.guard()`;
none of them is in the tested ten because none of them emits a file name in the
survey's conditions — they refuse first, which is `dirguard` working.

---

## P22's list, enumerated and published with its length

P22 asks for **every tool in the box that could be pointed at this object and
has not been**, published with its length, *before* a reader is written.
**Four readers were written before the list was enumerated, and that is a
breach** — [00](00-predictions.md) records it and
[15](15-prediction-scoring.md) scores it. **The list is enumerated anyway.**

"Could be pointed at this object" has to be mechanical or the list is
unfalsifiable. The definition used is: **a tool is pointable when a format
keyword it names in its own first forty lines matches a family the object's
magic census actually contains** — the keywords read out of the tools, the
families read out of `coverage.py`'s table.

```
python _work/p22list.py                            (notes/p22-list.txt)

tools in the box                      : 568
POINTABLE at this object              : 260
  of those, run this session          :  33
  **NOT RUN -- P22's list**           : 227
naming only formats this object lacks : 106
unclassified (no format keyword)      : 202
260 + 106 + 202 = 568, residue 0

by family : text 132  png 32  zip 28  tree 17  pe 17  steam 16
            jpeg 12  ogg 12  html 6  pak 5  json 4  mpeg4 4  elf 3  font 2
```

**227 of 568.** *(The first run of this program reported 335, because the
keyword `elf` matched inside `self` and `selftest` and put 152 tools on the list
that have nothing to do with the System V ABI. A membership test that loose
makes the list worthless, and the repair is word boundaries —
[13](13-corrections.md) C.6.)*

### P22's falsification, evaluated

The condition is: *if the enumerated list is run and produces nothing a chapter
uses, then the box's unused tools are unused because they are irrelevant and not
because nobody aimed them.*

**Three tools were taken off the pointable list and pointed, and all three
produced something a chapter uses.**

| tool | population nobody had pointed it at | what it produced |
|---|---|---|
| `zipdir.py` | the 205,182,933-byte macOS ZIP | 564 entries walked to residue 0, 168 more `.pak`, [07](07-the-runtime.md) |
| `pngpair.py` | a picture in this object against a picture in the previous one | the 1.5 × ratio, which is the tile size, [11](11-against-the-collection.md) |
| `jstore.py` | the 129 JSON and the 222 `.pak` | eight predictions, eight right, below |

**P22's falsification does not fire**, and the claim is small and specific:
three tools, three chapters. **What P22 cannot claim is the other 224**, which
were not run, and the honest reading of that is that a list of 227 is too long
to be a work plan and is only useful as a denominator.

---

## `jstore.py`, seventh object, and eight predictions written first

The predictions are in `notes/jstore-prediction.txt`, **written before the tool
was run**, as the last three sessions have done. The population chosen is the
129 JSON documents, because their `0xFF` density is predictable **from the
format** rather than from a measurement — 0xFF is not a legal byte in UTF-8 at
any position.

```
python _work/jstorerun.py                          (notes/jstore-run.txt)

=== the 129 JSON documents ===
  closing at residue 0       : 129 of 129
  claiming ZERO GUIDs        : 129
  TOTAL GUIDs claimed        : 0
  0xFF bytes over the family : 0

=== the 222 Chromium .pak ===
  closing at residue 0       : 222 of 222
  claiming at least one      : 19
  TOTAL GUIDs claimed        : 990115
  0xFF per 1,000 bytes       : 1.4219
  GUIDs per 1,000 bytes      : 11.0426

the running total of empty closures : 138 + 129 = 267
```

**Eight of eight.** All 129 close; the `0xFF` count is zero; the claim is zero;
the running total reaches 267; the one file that does not parse as JSON behaves
like the other 128; the `.pak` claim is large; none of the claims is a GUID; and
the ratio between the two populations is unbounded rather than merely tenfold.

**The previous three sessions scored 5 of 7, 7 of 8 and now 8 of 8**, and the
improvement is not skill: it is that the diagnosis those sessions arrived at —
**the false-positive rate tracks the density of the byte `0xFF`, not the file's
length** — is now strong enough to predict a population from its *encoding*
rather than from a sample of it.

**And the defect is at its seventh appearance and is unchanged.** `jstore.py`
closes at residue 0 by construction because it counts everything it does not
understand as filler. **990,115 GUIDs in 222 files is the number a tool produces
when its closure test cannot fail.**

---

## The defects carried, with their counts

| tool | defect | appearance |
|---|---|---|
| `dircensus.py` | a full table over zero, exit 0 | twenty-fifth |
| `namecensus.py` | `ZeroDivisionError` | twenty-fourth |
| `protscan.py` | pre-2010 optical markers | **twentieth** |
| `mzcensus.py` | filters by the `.EXE` extension | **thirteenth**, 9 of 102 |
| `kfaccount.py` | exits 0 printing its usage | eighth |
| `refusals.py` | counts an `argparse` error as a refusal | **eighth**, 23 of 54 |
| `jstore.py` | residue 0 by construction | **seventh object** |
| `ispkg.py` | refuses without reading a byte | fifth |
| `buildroot.py` | `--root` does not aim it | fourth |
| `pdbpaths.py` | CodeView only | fourth |
| `oggtime.py` | hard-coded to another object's subcommands | third |
| `coverage.py` | **the byte-order mark** | **first — and it is ours** |
| `vendorhash.py` | **a fixed marker table, 0 of 9 vendors** | **first — repaired** |
| `refusals.py` | **a stale claim in its own harness** | **first — repaired** |
| `oggcensus.py` | **selects by extension** | **first — repaired** |

**Four of the fifteen were repaired here and eleven were not**, and the eleven
are inherited, catalogued, and left alone because repairing them is not this
object's work. **The four that were repaired are the four this object could
falsify**, which is the only reason any of them was found.

---

## P16, which is still not a clause

```
python tools/rule0hook.py --report                        (notes/rule0.txt)
```

`tools/rule0hook.py` was registered in `.claude\settings.local.json` **before
the first line of the predictions document and before the first tool was
touched**, and its first live test was a `python -c` that it refused. There is
deliberately no clause about rule 0 in [00](00-predictions.md), because P16 says
the clause is not the instrument.

```
python tools/rule0hook.py --report                        (notes/rule0.txt)
shell calls seen by the hook : 231
  allowed                    : 227
  REFUSED as rule-0          : 4
      heredoc 2     inline program 1     in-place edit script 1
```

**It refused four times. One was the deliberate probe and three were reflexes** —
a heredoc reached for to print one line, a `sed -i` pointed at `/dev/null` while
checking for an import, and a second heredoc. **None reached the shell.** The
denominator is a running count that only grows and the numerator is complete;
the four refusals are the measurement, and 231 is the figure at the moment
`notes/rule0.txt` was last regenerated.
