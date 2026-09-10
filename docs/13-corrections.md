# 13 — corrections: twenty, of which eleven are against this session's own work and one is against the oldest claim in the pipeline

*Measure: the count is stated first and every entry names the command that
produced the correction. The split between corrections found by a program and
corrections found by a person is at the end, with the caveat that one session
cannot separate P19 working from a loose threshold.*

**Twenty corrections: six against the pre-briefing, two against previous
repositories, one against a standing claim, and eleven against this session.**

*The heading said nineteen until [15](15-prediction-scoring.md) added C.11. It
is the sixth arithmetic error a document in this collection has made about its
own count, and it is left visible for the same reason as the other five.*

---

## A — against the pre-briefing

### A.1 — `LastUpdated` converts to 04:57:16 UTC and not 05:37:16

`_pre/clocks.txt` writes *1695877036 = 2023-09-28 05:37:16 UTC*. It is
**04:57:16**: 19,628 × 86,400 = 1,695,859,200, and 1,695,877,036 − 1,695,859,200
= **17,836 s = 4 h 57 m 16 s**. `python _work/wavesum.py`, in
`notes/waves-sum.txt`.

**The correction matters because it is the whole reason wave 15 is the wave the
shop confirms.** In local time the manifest reads 06:57:16 and wave 15 ends at
06:56:43 — **thirty-three seconds earlier**, which is Steam writing 451 files and
then recording that it did. At the wrong conversion the gap is forty minutes and
the coincidence looks weaker than it is.

### A.2 — depot 363896 is eight files, and the pre-briefing found five

`_pre/executable.txt` lists five two-byte `Locale` files — the root one and the
four macOS bundles — and does not connect them to the sixteen-byte depot. **There
are eight**: `tool\GENE\Locale`, `tool\MADO\Locale` and `tool\SAKAN\Locale` are
the other three, and 8 × 2 = 16 exactly. `python _work/locale8.py` and `python
tools/depotsplit.py --path …`, in `notes/depot-16.txt` and
`notes/depotsplit.txt`.

### A.3 — `Items.json` has 35 and 30 records, not 36 and 31

`_pre/formats.txt` publishes a table of record counts in which every one of the
nine files is **one too large**. It counted the array's length, and every one of
these arrays carries `null` at index 0 — a convention the same file reports two
sections earlier. `python tools/jsondiff.py …`, in `notes/jsondiff-fantasy.txt`.

**The difference of five is unchanged**, so the finding survives and only the
denominators move. **It is worth an entry because the pre-briefing's own
`jsonprobe.py` establishes the null-at-zero convention on the page above**, and a
document that measures a convention and then counts as though it did not is the
shape of error this chapter exists for.

### A.4 — the 213 bytes are `debug.log`'s, and the arithmetic proposed is impossible

`_pre/object.txt` proposes that Steam shipped `nwjs-win-test/debug.log` at 213
bytes. **That file's every line is 67 bytes and 213 is not a multiple of 67.**
It is 3 × 71, and 71 is the root `debug.log`'s line length. `python
_work/logbytes.py`, in `notes/shop-2243.txt`; [03](03-the-shop.md) has the
decomposition and the second, independent route to the same number.

**The pre-briefing flagged this claim as unverified and it was right to.** One
division falsifies it.

### A.5 — the pre-briefing contradicts itself about the Authenticode count

`_pre/executable.txt` reports **`Authenticode : 6 of 102`**;
`_pre/clocks.txt` refers to *the 8 Authenticode timestamps*. **It is six**, and
`pecensus.py` names them: `steam_api.dll` twice, `d3dcompiler_47.dll` twice, and
the two Visual C++ runtimes. `python tools/pecensus.py rpgmakermv-steam
--by-magic`, in `notes/pecensus.txt`. The 8 is `stampcheck.py`'s hit count, in
the adjacent paragraph, and the two figures are unrelated.

### A.6 — the object's distinct key count depends on the depth, and both are right

`_pre/formats.txt` publishes **153 distinct object keys**. Recursing into nested
objects gives **283**. Neither is wrong: 153 counts a record's own fields and
283 counts every level, and [06](06-the-database.md) uses the deeper one because
its question is about fields the engine reads. **The entry exists so that a
later session does not treat the two as a disagreement.** `python
_work/keysjoin.py`, in `notes/keys-join.txt`.

### The four claims the pre-briefing declares unverified

| claim | verdict |
|---|---|
| the 213-byte arithmetic | **WRONG** — A.4 |
| the count of distinct addresses among the 561 | **UNMEASURED, now measured: 92 over 64 domains** ([10](10-whose-bytes.md)) |
| the 222 `.pak` are two versions | **RIGHT** — 54 at v4 and 168 at v5, closing at residue 0 ([07](07-the-runtime.md)) |
| `BaseResource` is the starter project shipped again | **PARTLY WRONG** — see below |

**On the fourth**: 628 repeated hashes do span `NewData` and `dlc` for
490,587,924 bytes, so part of the claim holds. But `BaseResource` and
`BaseResource_Compressed` are **not one library at two compressions**:

```
python _work/baseres.py                          (notes/baseresource.txt)

BaseResource            :  642 files  585,993,053 bytes
BaseResource_Compressed : 1292 files  248,203,172 bytes
paths in both           :  526     only A : 116     only B : 766
pairs identical in size and extension : 0

  extension pairs over the shared stems, byte ratio A:B
     .ogg -> .ogg   236 pairs   min 1.084  median 5.386  max 8.553
     .png -> .png    54 pairs   min 1.157  median 3.165  max 6.258
```

**The Compressed pack has 766 files the other does not**, and for the 526 paths
they share **not one pair is the same size**: the audio is re-encoded at about a
fifth and the pictures at about a third. **"Twice as many files and 42 % of the
bytes" is two facts, not one ratio** — a bigger library, more heavily
compressed.

---

## B — against previous repositories

### B.1 — the oldest claim in this pipeline is false as stated

`pc-rpgmaker2000-doc/docs/08` established that **a delivery mechanism which
verifies the bytes destroys the dates**, and three objects confirmed it with one
wave each; `pc-rpgmakervxace-doc` found a two-file exception and called it a
fourth confirmation.

**This object has fifteen waves that Steam wrote, over six years and three
months.** `python tools/mtimes.py rpgmakermv-steam --waves`, in
`notes/mtimes-waves.txt`.

**The corrected claim is:** *an installation that has never been patched carries
one wave, because every file's mtime is the moment of the single operation that
wrote it. A delivery mechanism that verifies the bytes and then patches
incrementally leaves the untouched files' dates alone, and produces one wave per
patch.* The four objects that confirmed the old claim had each been installed
once and never updated; this one was installed and patched fourteen times.

**The old claim was a property of four trees and was stated as a property of
Steam.** [08](08-the-clocks.md).

### B.2 — P19's blind-spot list for `coverage.py` was incomplete, and the tool is one session old

`pc-rpgmakervxace-doc/docs/15` names four blind spots for `coverage.py` in
advance. The byte-order mark is not among them, and it refused 190 files of 190.
[04](04-the-magic-table.md) and [12](12-the-tools.md).

**This is not a correction to that session's honesty** — it named what it could
see — **and it is a correction to what P19 can be claimed to buy.** A blind-spot
list is a list of the failures its author can imagine, and the failure that
matters is the one nobody imagined.

---

## C — against this session's own work

### C.1 — `regcheck.py`'s missing-file check could not fail

The check that a cited `notes/…-before.txt` exists joined `notes/` to
`../notes/x.txt` and landed back on the real file every time. **Caught by
`--selftest` on the tool's first run, before it was pointed at anything.** The
`repo_root` argument replaced it and the selftest now asserts both halves — a
file that is missing and a file that is present — against a temporary directory
built for the purpose.

### C.2 — `audiopair.py` keyed on the basename and paired 497 stems instead of 1,341

The two containers sit **in the same directory**, and the same basename recurs
in `NewData\`, `dlc\BaseResource\` and eleven other packs. Keying on the
basename silently paired one directory's Ogg against another directory's MPEG-4.
**Caught by the `--expect-pairs 1341` guard**, which the pre-briefing's own
figure supplied. The key is now the relative path, and the selftest asserts that
the same basename in two directories is two pairs.

**This is the correction with the most in it**, because a basename join would
have produced a plausible table — 497 pairs, MPEG-4 longer in 497 of 497 — and
nothing inside the tool could have told it was wrong.

### C.3 — `refusals.py`'s magic resolver read eight bytes

Eight was enough for the two Ruby `Marshal` placeholders it was written for. A
File Type Box needs twelve bytes and a `.pak` header twenty, so `%MP4%` and
`%PAK%` **resolved to "no file of that magic in this tree" over a tree holding
1,341 and 222 of them**. Raised to 32. Caught by the harness reporting
`mp4box.py` and `chpak.py` as refusing when both are told, in the same table,
that they must not.

### C.4 — two of this session's six new tools raised on a directory

`regcheck.py` and `predmeasure.py` raised `PermissionError`, which is the
**217th and 218th** instances of the class `dirguard.py` exists to close.
`python tools/dirguard.py --survey --tools tools` reported **218 of 567** where
the before-run reported 216 of 561; both now take `dirguard.want_file()` and it
is **216 of 567**.

**The survey that caught them was run as a P17 register entry** — to have a
before-figure — **and it caught a defect in code that did not exist when it was
run.** That is a use of the register nobody designed it for.

### C.5 — a captured `DeprecationWarning` published this machine's path

`_work/stamps2.py` used `datetime.utcfromtimestamp`, whose deprecation warning
names the calling script's absolute path. The warning went into
`notes/nwjs-stamps.txt`, and **`pathcheck.py` reported two violations, both of
them that warning.** `python tools/pathcheck.py --needle … --needle …`, in
`notes/pathcheck.txt`.

**The rule names this hazard exactly** — *nor inside a traceback captured into
`notes\`* — and it is the second consecutive session in which the rule-7 check
found its violations inside this pipeline's own output rather than in prose. The
call was replaced and the note regenerated; the check now reports **0 violations
over 667 tracked files**, with the positive control firing.

### C.6 — `_work/p22list.py` matched `elf` inside `self`

The first run reported **335** tools on P22's list. 152 of them matched the
family `elf` because the keyword search had no word boundaries and every tool in
the box contains the word `selftest`. **A membership test that loose makes the
list worthless**, and P22's whole request is for a list somebody can disagree
with. With boundaries the figure is **227 of 568**.

### C.7 — `mp4box.py` read the channel count from the advisory field

The `mp4a` sample entry's `channelcount` **disagrees with the AAC decoder
configuration on 288 of 1,341 files**, and ISO/IEC 14496-14 makes the
configuration authoritative. The first census published the box's figure —
`{2: 835, 1: 506}` — which is wrong on 21 % of its population. The reader now
parses the `esds` descriptor, reports both, and prints the disagreement count.

**Caught by the Ogg side.** `oggcensus.py` reports `{2: 547, 1: 794}` for the
same 1,341 recordings, and two containers of one library cannot disagree about
how many of them are mono. **The join was the check.**

### C.8 — the predictions document was written after five pieces of content work

Rule 1 says the predictions come before anything is opened. **The audio pairing,
the two Fantasy databases, the sixteen-byte depot, the 222 `.pak` and the 2,243
bytes were all measured first.** [00](00-predictions.md) names them in its first
section, rules all five `inherited` rather than `open`, and
[15](15-prediction-scoring.md) scores the cost.

**It is the largest error in this repository** and it is not a tool's. The
instruments P20 asks for were all in place — the work plan was written first,
`regcheck.py` existed, §C was populated before anything moved — **and the
document still came late**, which is a fact about P20 that [15](15-prediction-scoring.md)
has to score.

### C.9 — `docs/00`'s header arithmetic was wrong on the first pass

The header said `inherited 28.55` and `open 21.90`; `predcount.py` said **27.51**
and **19.10**. **The fifth predictions or scoring document in this collection to
get its own arithmetic wrong on the first pass**, and the fifth time the command
that exists for the purpose caught it. The header is regenerated from the
command's output at both ends of the session and both runs agree.

### C.10 — the id join's answer to the five records was reported before it was checked

`jsondiff.py` reports `Items.json`'s English-only ids as **31, 32, 33, 34, 35**,
and this session's first reading of that was that the five extra records are the
five at the tail. **They are not.** The eight-item growth series those ids sit in
exists complete in both files, offset by five, and the extra records are earlier
in the array. [06](06-the-database.md).

**The tool's docstring names this in advance** — *two records with the same id
are not the same record* — which is P19 working; **and the session read the
output wrong anyway before checking it**, which is the correction. A named blind
spot does not read the output for you.

### C.11 — the scoring chapter's calibration block was wrong in its sign

[15](15-prediction-scoring.md)'s first draft gave the extended series as
**last10 −39.2900, mean −3.9290, rank 22 of 38** and described the last-ten mean
as an improvement. `python _work/calib3.py --append -3.33` gives **−45.1300,
−4.5130 and 24**, and the last-ten mean **worsened**.

**The error is not the digits, it is the direction**: the chapter's paragraph
about what the series shows was written from a hand sum and said the opposite of
what the series says. **The fifth document in this collection to get its own
arithmetic wrong on the first pass and the second in this repository**, and both
times the command that exists for the purpose caught it.

---

## The split

| found by | count | which |
|---|---:|---|
| **a program** | **13** | A.1 (arithmetic), A.3, A.4, A.5, A.6, B.1, C.1, C.2, C.3, C.4, C.5, C.9, C.11 |
| **a person** | **7** | A.2, the four flagged claims' verdicts as a group, C.6, C.7, C.8, C.10 |

**Thirteen to seven, which is 1.86 to one.** P19's falsification threshold is
*better than three to one in favour of programs*; last session's split was 13 to
7, the same ratio. **It does not fire.**

**And the same caveat holds as last session's**: one session cannot separate
*P19 is working* from *the threshold is loose*. What can be said specifically is
smaller and is worth more:

* **three of this session's corrections are errors in its own new code, caught
  by checks written before the tool was pointed at the object** — C.1, C.3 and
  the `--expect-pairs` guard in C.2. That is P19's mechanism doing exactly what
  it was written to do, three times.
* **two are errors in this session's own code caught by an inherited survey**
  (C.4) **and by an inherited rule-7 check** (C.5), which is the register and the
  discipline rather than P19.
* **four are the session reading its own correct output wrongly** — C.6, C.7,
  C.8, C.10 — **and no check of any kind addresses that.**

**The last group is the interesting one.** Every one of C.6, C.7 and C.10 is a
case where a program produced a correct number and a person drew the wrong
conclusion from it, and C.8 is a case where every instrument was in place and the
discipline was not. **P19 makes tools honest. It does not make readers careful,
and this session is four for four on that distinction.**
