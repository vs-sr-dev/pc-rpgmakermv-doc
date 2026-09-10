# 15 — prediction scoring: P20's program worked and the document still came late, P21 gets its first point and cannot get a trend, and P22's falsification does not fire on three tools out of two hundred and twenty-seven

*Measure: `python tools/predcount.py` for the clause counts and the two
predicted totals; `python tools/predbands.py --expect-under 0.60 5` for the
three bands; `python tools/predmeasure.py` for P21's counts; `python
tools/regcheck.py` for P20's membership, exit 0; `python _work/calib3.py` for
the inherited series, in `notes/calibration.txt`. The verdicts below are counted
out of the tables on this page.*

```
58 clauses     inherited 31     open 27 (method 5, content 22)

inherited      31 clauses   predicted 27.51   obtained 30.00   delta  -2.49
open           27 clauses   predicted 20.67   obtained 24.00   delta  -3.33
  open method   5 clauses   predicted  4.52   obtained  5.00   delta  -0.48
  open content 22 clauses   predicted 16.15   obtained 19.00   delta  -2.85
                            (4.52 + 16.15 = 20.67 and 5.00 + 19.00 = 24.00)

and the three P11 bands:
  lands        6 clauses   predicted  5.10   obtained  6.00   delta  -0.90
  constructs  12 clauses   predicted  7.97   obtained  9.50   delta  -1.53
  nonnumeric   4 clauses   predicted  3.10   obtained  3.50   delta  -0.40
                                    ------  ------          ------
  the three bands                    16.15   19.00           -2.85

hit = 1, half = 0.5, miss = 0. The two totals are never added together.

the verdicts:
  hit           50      (inherited 29, open method 5, open content 16)
  half           8      (C08, C23, C42, C43, C48, C50, C55, C57)
  miss           0
  unresolved     0
  50 + 8 = 58, residue 0
  29 + 2 x 0.5 = 30.00   5 + 0 = 5.00   16 + 6 x 0.5 = 19.00
```

*This block is the third table in this repository to be wrong on its first
pass. It said `29.00` for the inherited total and listed four inherited halves
where the table below has two, and it counted C35 both ways at once — a hit in
the open-method total and a half in the verdict list. Adding the columns up
gives **30.00**, **50 hits and 8 halves**, and `constructs` at **9.50** rather
than 10.00. **A scoring chapter that gets its own arithmetic wrong is the fifth
in this collection and the third in this repository**, and it is left visible
here for the same reason as the other two ([13](13-corrections.md) C.9 and
C.11).*

**The calibration entry for this session is `−3.33`**, predicted minus obtained
on the open clauses. Ranked by absolute value it is **twenty-fourth of
thirty-eight**.

---

## Inherited — 29 hits, 2 halves, 0 misses

| | verdict | note |
|---|---|---|
| C01 | **hit** | 9,641 of 9,641 on all three axes, 406 directories of 406, 10 empty of 10, final agreement `True` |
| C02 | **hit** | 9,641 / 2,925,489,709 / 7,417 / 0; 7,417 + 2,224 = 9,641; 1,351 repeated; the byte total re-derived by `treecensus.py`, which is not `hashall.py`; **and the non-ASCII names counted rather than taken from the brief — 5 files, 4 distinct basenames, and the guard held on all five** |
| C03 | **hit** | every field exactly, both residues, the two absent fields named, `SharedDepots` reported, `LastOwner` redacted by the program and `LauncherPath` withheld |
| C04 | **hit** | 8 files, 16 bytes, residue 0 **by walking**, `depotsplit --path` closing over 9,641 files in two groups — and the brief's five corrected to eight |
| C05 | **hit** | the 213 refuted by a division, the decomposition closing, **a second independent route through the wave sums**, and the cost of the reading stated instead of hidden |
| C06 | **hit** | seventeen waves summing to 9,641 and 2,925,489,709 at residue 0 **with the sum checked**, and `LastUpdated` converted — which found the brief's conversion forty minutes wrong |
| C07 | **hit** | 324 rows carrying files over 407 nodes, 83 carrying none, 10 empty; **eleven top-level shares recomputed in exact decimal, 0 differing** |
| C08 | **half** | 34 rows summing to 9,641 and 2,925,489,709, every named row exact, and the absences confirmed — **and the six "new" extensions checked against all five predecessors' `sha1-all.txt` and absent from all five**, which the clause asked for. **The half is for something the clause did not notice**: `.so` at 5 files and 147,013,560 bytes is a seventh extension new to this collection and the brief's list of six is short |
| C09 | **hit** | the P17 clause; 7,806 / 2,100,016,569 / 0 / 0 / 1,835 / 825,473,140 at residue 0, from a file written before the classifier was touched |
| C10 | **hit** | 35,810 of 51,926, `.ZIP` 7.9970 and `.JSON` 3.8035, and both neighbours' figures — 2.0714 and 3.8587 — **taken from their own `docs\` and not from the brief** |
| C11 | **hit** | 102, PE32 101 and PE32+ 1, 17 days, 6 signed, 2 impossible, the seven `CompanyName` rows summing to 102 at residue 0 |
| C12 | **hit** | 8 of 102, T1 twice and T2 six times and T3 zero, both `d3dcompiler_47.dll` at 3,661,112 bytes and stamp 2455089808, **both confirmed to carry a certificate table**, and the 2047 reported as a build hash |
| C13 | **hit** | every field, the two versions disagreeing, and the three copyright lines quoted from three repositories' own `docs\` |
| C14 | **hit** | 9 of 102 and 0 / 1 — **and the one occurrence located at offset 3,455,871 of 4,474,408 inside a Vorbis packet**, which is what makes it a coincidence rather than a near miss |
| C15 | **hit** | 5,578 / 5,578, 91,607 of 91,607, five IHDR shapes summing to 5,578, 0 interlaced |
| C16 | **hit** | 1,341 / 1,341, 144,905 of 144,905, one stream each, EOS on all, 20,484.642 s |
| C17 | **hit** | 1,341 pairs at residue 0 both ways, longer in 1,341 of 1,341, **and the mechanism fitted exactly at D = 2,112 on 1,069 of 1,075**, with the band's floor and ceiling both attained |
| C18 | **hit** | 1,075 of 1,341 on rate with the direction one-sided, 1,341 of 1,341 on channels **once read from the authoritative field**, the `mp4a` box's 288 disagreements reported, and four independent measurements selecting the same three files |
| C19 | **hit** | 129 / 4,286,178 / 128 / 1, both root types, 83 of 83, 153 keys, the refusing file named with its parser error, and the XP's twelve-of-thirteen quoted from that repository |
| C20 | **hit** | 9 names in both, 8 of 9 agreeing, 35 against 30, and the brief's off-by-one traced to the `null` at index 0 |
| C21 | **hit** | the series complete in both at 28–35 and 23–30, the displacement of five identified, and **the id join named as answering a different question** |
| C22 | **hit** | 54 and 168, 19,506,192 and 70,156,671, 222 of 222 closing, 868,459 and 127,790, and 2,502 + 5,723,246 + 83,937,115 = 89,662,863 at residue 0 |
| C23 | **half** | 731 in 258 with 103 nodes and 638 of 731, redacted by the program — **but the two neighbours' figures were taken from the brief and not from their `docs\`**, which is what the clause promised and what rule 6 requires |
| C24 | **hit** | 561 in 30, 38 in 8, 6 in 6, 2, 1, both controls firing, 2,314 in 44 and 15,529 in 411 |
| C25 | **hit** | every row exact, the previous objects' zeros quoted from their `docs\`, **and `utf16sift.py` actually run** — 77 hits only a sixteen-bit pass finds, of which 0 are e-mail shapes and 75 are drive-letter paths |
| C26 | **hit** | 0 of 11 with the control firing on 102 of 102, and the control stated as a control |
| C27 | **hit** | the P17 clause; 562 / 562 / 0 / 0 / 562 / 0 and 562 files with three controls firing |
| C28 | **hit** | the P17 clause; 216 of 561 and 7 / 3 / 551, with the claim stated over 10 |
| C29 | **hit** | the P17 clause; 85 / 56 / 29 and 23 / 17 / 15 / 1 summing to 56 at residue 0 |
| C30 | **hit** | the P17 clause; 79 rows, 0 over budget, the five column budgets |
| C31 | **hit** | 37 terms and all eight of the prompt's claims checked one at a time, 0 wrong |

**Two halves in thirty-one, which is 6.5 %**, against last session's two in
thirty-three (6.1 %) and the session before's one in thirty-three (3.0 %).
**And they are different failures**: C08 missed a seventh new extension its own
census printed, and C23 quoted two neighbours' figures from the brief instead of
from their `docs\`, which is rule 6. **C23 is the one worth naming**, because
C10 and C25 did the same job correctly in the same document — so the rule was
understood and applied twice and dropped once.

---

## Open, method — 5 hits

| | verdict | note |
|---|---|---|
| C32 | **hit** | six tools written and four modified; **265 checks over nine tools, 0 failures**; every selftest run with `PYTHONIOENCODING` unset; every name checked against `tools/`; every file-selecting tool selecting by magic — **including one inherited tool repaired to obey it**; and the blind spots named in every docstring **with the check written first**, three of which fired ([13](13-corrections.md) C.1, C.3 and the `--expect-pairs` guard) |
| C33 | **hit** | every chapter opens with `*Measure:*`, `docs/02` carries a command on every row, `docs/01` tabulates **nine** denominators with the second named as the finding, and the documents are English |
| C34 | **hit** | **667 tracked files, 0 violations, positive control firing, negative control quiet** — and **its first run found two real violations**, both a captured `DeprecationWarning` carrying this machine's path into `notes\`, which is the hazard rule 7 names by name ([13](13-corrections.md) C.5) |
| C35 | **hit** | branch `master`; the `git ls-files` filter empty **with a positive control that fires and is then removed**; the six excluded paths checked one at a time and absent; **a 329-character description read back from the remote by `gh api` and not from the command that set it**; ten topics set and read back; and `pc-gamelist-doc` pushed on `main` at 80 rows, 0 over budget. **See the note at the end of this chapter**: this verdict was written after the push and the clause was scored a half until it happened |
| C36 | **hit** | sixteen documents, under twenty, the count justified in `docs/01` against the last ten sessions, and no chapter a census of a resource family for its own sake |

---

## Open, content — 16 hits, 6 halves, 0 misses

| | verdict | band | note |
|---|---|---|---|
| C37 | **hit** | `lands` | 104 + 190 = 294 and 2,182,962 + 1,108,362 = 3,291,324, both at residue 0 against a committed before-table; eight checks of which the second **fails without the repair** and four assert a refusal |
| C38 | **hit** | `lands` | five magics, the ordering rule enforced and falsifiable, **the Java class file refused at major 45 and at major 52**, and 9,384 / 222 / 0 / 35 at residue 0 with the 35 decomposed 4 + 24 + 6 + 1 |
| C39 | **hit** | `constructs` | the membership test quoted from `pc-rpgmaker2000-doc/docs/09` and applied, what would move it to SPECIFIED named, 868,459 resources with 862,722 UTF-8 and the 5,737 classified by `coverage.py`'s own table, and the four-object emptiness taken from the committed before-file |
| C40 | **hit** | `constructs` | nine probes with offsets, the split into 1,674 components and 1 carrier, **and `--survey` reporting 5 of 6 third-party companies covered with the publisher held apart** — and the one company it misses identified as Microsoft, with the reason |
| C41 | **hit** | `constructs` | the sentence replaced by a `%ZIP%` placeholder resolved by magic, two more magics added, seven readers added, and the difference reported: 85 → 92 pointed, 56 → 54 refusing, `format` 15 → 13 with all four departures shown to be harness artefacts |
| C42 | **half** | `constructs` | **P12 clause.** The ZIP was walked to residue 0 — 564 entries, 219 directories, 504,651,796 → 204,997,407 — by `zipdir.py` rather than `zaccount.py`, which the clause named and which turned out to be the wrong tool and is reported as such. **The half is the second half of the clause**: whether the macOS player is the same build as the three on disk is **not** answered, because the only key the four share is a basename and the macOS locale files are all called `locale.pak` |
| C43 | **half** | `constructs` | **P12 clause.** 561 shapes → **92 distinct addresses over 64 domains** with `sift.py`'s own pattern and the reason recorded; the domains named; the third parties' publication established; the rule applied without reopening; **and the 103 node fields counted at 56 in more than one file.** The half: the clause promised *which of them belong to third parties who published them* as a count, and the chapter gives the domains and an argument rather than a number |
| C44 | **hit** | `constructs` | 2,361 in 70 files by this script's pattern beside `sift.py`'s 2,314 in 44 **with the difference attributed to the pattern and both printed**, every root over a dozen occurrences attributed, **0 carrying a path of this machine**, the needles built and not printed, and the Unix half given the XP's rule |
| C45 | **hit** | `lands` | all five denominators published before the result — 137, 68, 107, 477, 161,543 — 297 of 7,417, the split 276 / 21, **and the 21 shown to be a subset of the VX Ace's 26 with the five that dropped out named and then found still present under other bytes** |
| C46 | **hit** | `nonnumeric` | the list enumerated by a program with a stated membership test, **227 of 260 pointable and of 568 in the box**, the breach reported, and the falsification evaluated on the three that were run |
| C47 | **hit** | `constructs` | eight numbered predictions written first, **eight right**, the running total reaching 267, and the contrast against the `.pak` in one table |
| C48 | **half** | `constructs` | **P12 clause.** `pngpair.py` pointed across the object boundary for the first time on four pairs, the chunk-level evidence reported, and **the 1.5 × ratio found and identified as 48 ÷ 32**. The half: the clause asked for the verdict *identical, or identical IDAT under different ancillary chunks, or different*, and all four came back *different* — so the reader's discriminating power was never exercised, and a finding that arrives through a tool without using the tool's discrimination is half of what was promised |
| C49 | **hit** | `constructs` | 526 paths in both, 116 and 766 on one side each at residue 0, **0 pairs identical in size**, and the byte ratios by extension pair — which turns one ratio into two facts |
| C50 | **half** | `constructs` | **P12 clause.** The two Windows runtimes settled from three directions — 114 of 123 identical, five same-size pairs differing first at their COFF stamp, and the build roots naming `nw27_win32` and `nw27_sdk_win32` at 319 each. The half: **the Linux and macOS runtimes are not settled**, the chapter says so, and it names the measurement — but the clause promised the question tested for all three and one third of it was not |
| C51 | **hit** | `nonnumeric` | the candidates set out, the absent witness named, the distinction between a confirmed field and an unrivalled one stated in as many words, and the cell named as **2015** and labelled an attribution |
| C52 | **hit** | `nonnumeric` | four stranded threads with the measurement that would close each, twelve closed here, five settled elsewhere, six new questions, and no thread reported closed that is not |
| C53 | **hit** | `lands` | both refusals quoted in the original, the repair that makes them honest named, and the eight readers with no population reported in one line |
| C54 | **hit** | `lands` | the three notes written under exactly those names, and `notes/vendorhash.txt` holding a list of 1,675 rows rather than an explanation |
| C55 | **half** | `constructs` | **P12 clause.** The converter read: 3 files at 2 distinct sha1, 17 classes, **10 of the previous session's 21**, 7 that session never named, and **14 of 14 on the output side**. The half: the clause asked for the number *as a fraction of that census*, and 10 of 21 is a fraction of what that session's documents happen to mention rather than of a census it published — the previous repository never published a class list as a list, and the clause assumed it had |
| C56 | **hit** | `lands` | **twenty** with the count first, all four flagged claims given verdicts, the split 13 to 7 = 1.86 to one with the caveat, and the four corrections that are the session misreading its own output separated out |
| C57 | **half** | `nonnumeric` | thirty-four terms split 12 + 4 + 13 + 5 = 34, the demonstrated column compared with the previous object's 9 and the growth explained. The half: **the explanation is an argument and the clause implied a measurement.** "A manual explains what a user does, not what a format is" is not tested against the 139 pages; it is inferred from the outcome |
| C58 | **hit** | `constructs` | the 35 decomposed by family with each producer named, the arithmetic closing, and the claim about what the percentage measures made with the byte counts that support it |

---

## P11, scored, and P8's mechanism survives a fifth time

> **P11.** For each open content clause, record whether the object supported
> **more** than the clause asked. **Falsification: if `lands` and `constructs`
> have the same over-delivery rate, P8's mechanism is dead.**

The strict test is used, as last session: the object over-delivered when it
supported something the clause did not name **and that something changed a
conclusion**.

| band | n | over-delivered | rate |
|---|---:|---:|---:|
| `lands` | 6 | **2** — C38, C45 | **33.3 %** |
| `constructs` | 12 | **7** — C39, C40, C41, C44, C47, C49, C58 | **58.3 %** |
| `nonnumeric` | 4 | **1** — C52 | **25.0 %** |

**Not a tie, and in the direction P8 predicted, for a fifth session.** The five
measurements are 6/10 against 5/8; 75.0 % against 42.9 %; 84.6 % against 55.6 %;
75.0 % against 42.9 %; and now **58.3 % against 33.3 %**.

**And the band splits along P12's line again.**

| | n | over-delivered | rate |
|---|---:|---:|---:|
| the five `constructs` clauses P12 governs | 5 | **0** | **0 %** |
| the seven `constructs` clauses P18 governs | 7 | **7** | **100 %** |

**This is the reverse of last session and it is the sharpest number on the
page.** Last session P12's five over-delivered five times out of five and P18's
eleven over-delivered seven times out of eleven. **Here P12's five over-delivered
zero times out of five — four of the five are the four halves — and P18's seven
over-delivered seven times out of seven.**

**The explanation is not that P12 stopped working.** It is that the five clauses
P12 governs on this object are the five whose subject matter this session had
the least time for, and four of them are half-hits for the same structural
reason: **each promised a measurement in two parts and only one part was made.**
A clause that asks for the most the object could conceivably support, on an
object where the session ran out of session, produces a half and not an
over-delivery.

---

## P12, scored, and its falsification does NOT fire for the first time in four sessions

> **P12.** Write, for at least five open content clauses, the strongest claim
> the object could conceivably support rather than the one you are confident of,
> and price those five below 0.60. **Falsification: if all five hit, the pipeline
> was under-claiming rather than under-pricing.**

| | priced | obtained | what happened |
|---|---:|---:|---|
| **C42** | 0.42 | **0.50** | the ZIP walked; the cross-platform build question not answered |
| **C43** | 0.48 | **0.50** | 561 → 92 distinct; the third-party count given as an argument |
| **C48** | 0.45 | **0.50** | the 1.5 × ratio found; the reader's discrimination never exercised |
| **C50** | 0.50 | **0.50** | the Windows pair settled; Linux and macOS not |
| **C55** | 0.45 | **0.50** | the converter read; the denominator the clause assumed does not exist |
| | **2.30** | **2.50** | |

**Four halves and one half — five halves — and the falsification does not fire
for the first time in four sessions.** Its condition is *if all five hit*; none
of the five hit.

**And the diagnosis inverts.** Three sessions running, five clauses written to
ask for the most the object could conceivably support were all satisfied, and
P12's own reading was *this pipeline is under-claiming, not under-pricing*.
**Here all five came back at exactly half**, and the cost is **−0.20 of the
−3.33, which is 6.0 % of the calibration term** against last session's 49.4 %.

**The honest reading is that P12's five are now priced almost exactly right and
that is not good news.** A band priced at 0.46 that returns 0.50 is calibrated;
what it is not is ambitious, and P12 exists to buy ambition rather than
calibration. **Five clauses that each got exactly half of a two-part promise are
five clauses that asked for one thing too many**, which is a different failure
from asking for too much.

---

## P18, which is not in force and is scored anyway

> **P18.** Price `constructs` at the observed over-delivery rate — a mean at or
> above 0.80 — and put the ambition where P12 wants it. **Falsification: if
> `constructs` priced at 0.80 still over-delivers above 75 %, the band is
> measuring something other than confidence.**

`docs/00` names P20, P21 and P22 as the prescriptions in force and does not name
P18, because `pc-rpgmakervxace-doc/docs/15` scored it and moved on. **It is
scored here anyway, because this document priced its band as though P18 were in
force and a number produced under a prescription should be reported against it.**

```
constructs  n=12  total 7.97  mean 0.6642
  of which the five P12 clauses   2.30 over  5   mean 0.4600
  the seven P18 would govern      5.67 over  7   mean 0.8100
```

**The seven were priced at 0.8100, above P18's floor, and they over-delivered 7
of 7 = 100 %.** Last session's eleven were priced at 0.8636 and over-delivered
63.6 %; the session before, the whole band was priced at 0.6908 and
over-delivered 84.6 %.

**P18's falsification fires, and it fires hard.** Its condition is *above 75 %*
and the rate is 100 %.

**And the honest reading is not that P18 is wrong.** Seven of seven is a small
sample, and every one of the seven is a clause whose subject matter this session
had already half-measured or had a tool for — the `.pak` bucket, the vendor
table, the refusal harness, the drive-letter paths, `jstore.py`, the two
`BaseResource` packs, the coverage argument. **A band priced at 0.81 that
over-delivers seven times out of seven on clauses the session was already
equipped for is measuring preparation and not confidence**, which is precisely
what P18's falsification says it would mean. **The prescription survives as a
pricing rule and fails as a diagnostic**, and its own condition says so.

---

## P14, scored, and the two sub-terms move apart again

> **P14.** Report the term over the clauses P12 governs separately from the term
> over the rest. **Falsification: if the two sub-terms move together over the
> next three sessions, they are one signal and splitting them was bookkeeping.**

| | this session | last session | the one before |
|---|---|---|---|
| the five P12 clauses | 2.30 − 2.50 = **−0.20** over 5 | −2.55 over 5 | −2.60 over 5 |
| everything else open | 18.37 − 21.50 = **−3.13** over 22 | −2.61 over 26 | −3.26 over 26 |
| per clause, the rest | **−0.1423** | −0.1004 | −0.1254 |

**They moved apart: the P12 term improved by 2.35 and the other worsened by
0.52.** That is P14's falsification **not** firing, and it is the second of
P14's three sessions.

**But the reason is not the one P14 was written to detect.** The P12 term
improved because five clauses stopped over-delivering, not because they were
priced better; the other term worsened because a session that spent its first
hours measuring instead of predicting had less left for twenty-two clauses.
**Two sub-terms moving apart for unrelated reasons is not evidence that they are
two signals**, and the third session decides P14 with two of its three data
points explained by something else.

**The number that measures calibration is −3.13 over twenty-two clauses**, or
**−0.1423 per clause**, against −0.1004, −0.1254 and −0.1768. It is the second
best that band has recorded and it is worse than last session's.

---

## P17, and the register was populated before anything moved

**Ten figures were registered in §C, two more than last session, and all ten
commands were run before the first clause was written and before the tool each
one measures was touched.** Two of the ten are new categories: **a tool's
refusal is a state** (`vendorhash.py`), and **a survey with a denominator of ten
is a state** (`nameguard.py`).

**Every clause citing a registered figure scored a full hit** — C09, C27, C28,
C29, C30, and the three that cite one in the open band, C37, C38 and C39.
**P17's falsification does not fire, for the second session running.**

**And the register did something nobody designed it for.** `dirguard.py
--survey` was run to have a before-figure; the after-run caught **two of this
session's own new tools** raising on a directory ([13](13-corrections.md) C.4).
A register entry exists to stop a figure being lost; this one caught a defect
that did not exist when it was written.

---

## P20, scored, and the program worked on exactly the thing it addresses

> **P20.** Derive §C's membership by a program: before writing a clause, run it
> through a check that asks whether any command it names reads state this
> session's own work plan will change, and refuse the clause until that
> command's output is committed. **Falsification: if a clause still cites an
> unregistered pre-change figure when the membership test is a program, then the
> problem is that the session does not know its own work plan in advance, and no
> register can fix that.**

**Implemented as `tools/regcheck.py` and `notes/workplan.txt`, and it worked.**

**On its first run against the finished document it refused seven clauses.**

| | verdict |
|---|---|
| **C38, C39, C40** | **the program was right.** Three clauses named a command whose figure depends on state this session changes and cited no committed before-file. All three now cite one. **C40 is the sharp case**: it says *the tool that found zero components*, which is a pre-change figure, in a clause about the change — exactly C29's failure from last session, caught by a program this time |
| **C34, C44, C45, C47** | **the plan was wrong.** `pathcheck.py` reports a state at the END of the session; `crossall.py` is run with `--skip` on this repository; `jstore.py`'s running total lives in six other repositories. A `final` line type was added for the first case and the other two were dropped from the `reads` table, each with a written reason |

**So P20's mechanism caught three real ones and three false positives that were
its own input's fault, and the input is the part P20 does not address.** A
membership test is only as good as the plan it is given, and this session
discovered mid-run that its plan conflated *reads a state that changes* with
*reports a figure from before the change*. **That distinction is now a line type
and it is also the obvious way to game the check**, which is why every `final`
line carries a justification in the plan's own prose.

**P20's falsification, in its literal wording, does not fire**: no clause below
cites an unregistered pre-change figure, because `regcheck.py` exits non-zero if
one does and it exits 0.

### And P20 addressed membership while the failure was order

**The predictions document was written after five pieces of content work.**
[00](00-predictions.md) says so first, [13](13-corrections.md) C.8 records it,
and the cost is visible on this page: **twenty-two open content clauses where
last session had twenty-six, and the five most interesting things this object
holds are inherited clauses.**

**Every instrument P20 asks for was in place.** The work plan was written before
the first clause. The register was populated before any tool was touched.
`regcheck.py` was written, selftested and run. **And the document still came
late**, because nothing in P20 says *when* the document is written — only which
clauses belong in a section of it.

**That is the finding about P20 and it is not a falsification.** P20's
falsification asks whether a session that does not know its own plan can be
saved by a register; this session **knew its plan, wrote it down first, and
broke a different rule.** The prescription below is what follows.

---

## P21, scored, and it gets one point and cannot get a trend

> **P21.** Record, for every open content clause, **how many separate
> measurements the clause requires**, and report that count by band.
> **Falsification: if a well-priced `constructs` band's mean measurement count
> is no lower than the under-priced band's was, pricing does not buy timidity
> and the dial is free.**

```
python tools/predmeasure.py                       (notes/predmeasure.txt)

open content clauses : 22     measurements declared, total : 74

  band          n   measures    mean   priced   mean price
  lands         6         17    2.83     5.10       0.8500
  constructs   12         49    4.08     7.97       0.6642
  nonnumeric    4          8    2.00     3.10       0.7750
  ALL          22         74    3.36

  INHERITED clauses that declare a count -- reported apart:
    C17=6 C18=5 C21=4 C22=4     4 clauses, 19 measurements, mean 4.75
```

**`constructs` at 4.08 measurements a clause against `lands` at 2.83 and
`nonnumeric` at 2.00.** The band that carries the ambition carries the work, and
the ordering is the one the band names would predict.

**And P21 cannot be scored on this session, which is the honest result.** Its
falsification compares a well-priced band's mean measurement count with **the
under-priced band's**, and nobody recorded the under-priced band's — the
measurement did not exist until this document. **This session establishes the
first point of the series and says so.** The number to compare against next time
is **4.08 for `constructs` at a band mean of 0.6642, with 0.8100 over the seven
P18 governs and 0.4600 over P12's five.**

**And the count is declared, not derived**, with a floor: a clause cannot need
fewer measurements than the distinct commands it names, and `predmeasure.py`
exits non-zero if one does. **The check binds from underneath only**, which is
in the tool's docstring and asserted in its selftest — a clause naming one
command and declaring nine passes, by design, and that hole is on the record
rather than in a footnote.

**The block held apart is the one to look at.** The four inherited clauses that
declare a count average **4.75 measurements**, above every open band. **They are
the five pieces of work this session did before the predictions document**, and
they are inherited by that document's own ruling. **A P21 figure computed over
the open band alone is computed over the lighter half of the session**, and
`predmeasure.py` prints the heavier half beside it so that nobody has to
discover that in scoring.

---

## P22, scored, and its falsification does not fire on three tools of two hundred and twenty-seven

> **P22.** Before writing a single reader, enumerate every tool in the box that
> could be pointed at this object and has not been, and publish that list with
> its length. **Falsification: if the enumerated list is run and produces
> nothing a chapter uses, then the box's unused tools are unused because they
> are irrelevant and not because nobody aimed them.**

**Half obeyed. Four readers were written before the list was enumerated**, and
that is the same breach as C.8 in a different dress. **The list was enumerated
anyway** — 227 of 260 pointable, of 568 in the box, by a program with a stated
membership test that somebody can disagree with.

**Three tools were taken off that list and pointed, and all three produced
something a chapter uses:** `zipdir.py` on the 205 MB ZIP,
`pngpair.py` across the object boundary, and `jstore.py` on two populations.
**The falsification does not fire.**

**And the claim is small and is stated as small.** Three of 227. **What this
session actually learned about P22 is that a list of 227 is not a work plan**;
it is a denominator, and its use is to make *4.6263 % of the box was pointed*
into a sentence with a second number in it. **The prescription that follows is
about the list's shape and not its length.**

**And one confirmation of P22's diagnosis arrived without being looked for.**
`oggcensus.ogg_files` selected by extension, and the check that found it was
written for `audiopair.py` and aimed at an inherited tool. **P22 says the
chapters that find something new find it by pointing an existing reader at a
population nobody had pointed it at; this is the same thing one level down —
pointing an existing *check* at an existing tool.**

---

## P16, which is still not a clause

```
python tools/rule0hook.py --report                        (notes/rule0.txt)
shell calls seen by the hook : 190
  allowed                    : 186
  REFUSED as rule-0          : 4
      heredoc 2     inline program 1     in-place edit script 1
```

**Four refusals: one deliberate probe and three reflexes** — a heredoc reached
for to print one line, a `sed -i` pointed at `/dev/null` while checking whether
an import existed, and a second heredoc. **None reached the shell.** The
denominator is a running count that only grows; the four refusals are complete
and they are the measurement. Reported as a plain fact worth zero points.

---

## The calibration series, extended

```
python _work/calib3.py                             (notes/calibration.txt)
  the inherited series : 37 terms, sum -36.4300, mean -0.9846,
  25 negative, 1 zero, last10 -44.7200 for a mean of -4.4720,
  tail run of consecutive negatives : 6
  the prompt's eight claims about the series : 0 wrong

python _work/calib3.py --append -3.33
with this session's term appended:
  terms    : 38          sum : -39.7600      mean : -1.0463
  negative : 26          positive : 11       zero : 1
  last10   : -45.1300    mean -4.5130
  tail run of consecutive negatives : 7
  the last term -3.33 ranks 24 of 38 by absolute value
```

*The first draft of this block said `−39.2900`, a mean of `−3.9290` and a rank
of 22, and called the last-ten mean an improvement. The command says **−45.1300,
−4.5130 and 24**, and the last-ten mean **worsened**. **A scoring chapter that
gets its own arithmetic wrong on the first pass is the fifth in this collection
to do it, and the second in this repository** ([13](13-corrections.md) C.9 is the
other); it is recorded here rather than quietly corrected, and it is the reason
`calib3.py` exists.*

**The last-ten mean worsens from −4.4720 to −4.5130 and the tail run reaches
seven.** The series has now been negative for seven consecutive objects.

**And the term itself is the second smallest of the last ten**, at −3.33 against
a last-ten mean of −4.5130 — **which is almost entirely one thing.** −2.55 of
last session's −5.16 was P12's five paying in full; **−0.20 of this session's
−3.33 is P12's five paying a twelfth of that**, because all five came back at
exactly half. **The part that measures calibration went the other way: −0.1004
per clause last session and −0.1423 this one.**

**So the headline term shrank and the calibration worsened**, which is the mirror
image of last session, where the headline grew and the calibration improved.
**Two consecutive sessions in which the two numbers move in opposite directions
is the strongest evidence P14 has produced that they are two signals** — and it
arrives in a session where P14's own falsification did not fire and the reason it
did not fire is unrelated to what P14 is about.

**The next document has to decide whether the headline number is worth keeping**,
and this one's answer is that it is not, on its own: **−3.33 is a smaller number
than −5.16 and this was the worse-run session.**

---

## A note on C35, which was scored twice

**C35 is the repository clause and its last third happens after this file is
first written**: the remote is created, the description is read back, the topics
are set, and `pc-gamelist-doc` is pushed.

**It was scored a HALF in the first pass of this table, because a clause cannot
be scored on work not yet done** — and the alternative, writing the verdict
first and the work after, is exactly the failure this whole chapter is about.
When the push happened the verdict was raised to a hit and **this note was left
in rather than deleted**, because a table that quietly gains a point is a table
nobody can check.

**What the hit rests on**: branch `master`; the `git ls-files` filter empty with
a positive control planted, fired and removed; the six excluded paths tested one
at a time; **the description read back out of `gh api repos/… --jq
.description` at 329 characters, which is the remote's copy and not the argument
that set it**; ten topics read back from the same call; and `pc-gamelist-doc`
pushed on `main` with `rowlen.py` reporting 80 rows and 0 over budget against the
79 committed in `notes/rowlen-before.txt`.

**And the totals at the top of this page include the hit.** They were computed
after the push, and the arithmetic that produced them is `predcount.py`'s, not
this session's.

---

## What this document predicts

> **P23 — every instrument P20 asked for was built and the document still came
> last.** The register was a program, the work plan was written first, §C had ten
> entries, and `regcheck.py` refused seven clauses and was right about three.
> **None of that governs when the predictions document is written**, and this
> session wrote it after five pieces of content work because the object handed
> it five interesting questions and nothing said *not yet*. **P20 policed the
> contents of a document and the failure was its position in the session.**
> The next document should make the ordering a program too: **before any tool is
> pointed at the object for a purpose other than populating §C, a check should
> require that `docs/00` exists and that `predcount.py` runs clean on it** —
> which is a `PreToolUse` hook of exactly the shape `rule0hook.py` already is,
> and which P16 has already shown to be the only kind of rule this pipeline
> obeys. **Falsification: if a session with that hook in place still measures
> before it predicts — by writing a stub `docs/00` to satisfy the check and
> filling it in afterwards — then the ordering is not enforceable by a program
> either, and the honest response is to stop scoring open clauses at all.**

> **P24 — P12's five came back at exactly half, five times out of five, and the
> reason is structural rather than about ambition.** Every one of C42, C43, C48,
> C50 and C55 promised **two things** and delivered one: a walk *and* a
> comparison, a count *and* an attribution, a reader pointed *and* its
> discrimination exercised. **A clause that asks for the most the object could
> conceivably support is not the same as a clause that asks for two things**,
> and this session wrote the second while believing it was writing the first.
> The next document should **price P12's five on a single measurement each** —
> the hardest single thing, not the hardest pair — and record how many separate
> measurements each declares, which `predmeasure.py` now makes free.
> **Falsification: if five single-measurement P12 clauses priced below 0.60 come
> back at half again, then halves are what an ambitious clause is worth and the
> band is measuring the object's patience rather than the session's reach.**

> **P23 and P24 together cost nothing to run and one of them is a hook.** The
> third thing this document predicts is not a prescription and is put here
> because there is no seventh object of this family to carry it: **the four
> repairs this session made to inherited tools were all found by pointing them
> at an object they were not written for, and all four had survived every
> selftest in the box.** `coverage.py`'s byte-order mark, `oggcensus.py`'s
> extension filter, `refusals.py`'s stale sentence and its eight-byte read were
> each invisible from inside. **A tool box that is only ever tested against the
> object it was written for is a tool box whose defects are exactly as old as
> its last new object**, and this collection's only defence against that is that
> there is always a next one. **For this family there is not**, and the four
> repairs are the last ones these six objects will produce.
