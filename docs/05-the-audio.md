# 05 — the audio: one thousand three hundred and forty-one pairs, an overshoot that is two thousand one hundred and twelve samples, and three files made by a different program

*Measure: `python tools/mp4box.py census rpgmakermv-steam`, in
`notes/mp4box-census.txt`; `python tools/oggcensus.py census rpgmakermv-steam`,
in `notes/oggcensus.txt`; `python tools/audiopair.py rpgmakermv-steam
--expect-pairs 1341`, in `notes/audiopair.txt`; `python _work/delayfit.py`, in
`notes/audio-delay.txt`; `python _work/three.py`, in `notes/audio-three.txt`.
The three selftests are `notes/selftest-mp4box.txt` (31 checks),
`notes/selftest-audiopair.txt` (15) and `notes/selftest-oggcensus.txt` (15),
all run with `PYTHONIOENCODING` unset, 0 failures.*

---

## The question, and why it needed a reader

**Every one of this object's 1,341 audio recordings is shipped twice**, once as
Ogg Vorbis and once as MPEG-4 AAC. 684,463,713 + 473,279,531 = **1,157,743,244
bytes, 39.6 % of the object**, and the pre-briefing established that the two
sets of stems join at residue 0 in both directions.

It also established the two aggregate durations — **20,484.642 s** for the Ogg
and **20,590.750 s** for the MPEG-4 — and that nobody had paired them.
**An aggregate cannot tell 1,341 small overshoots from 1,300 identical files and
41 different recordings**, and this box had no MPEG-4 reader: `mp3frames.py`,
written last session, reads MPEG-1 Layer III frames and will not touch a box
tree.

`pc-rpgmakervxace-doc/docs/02` had answered the same question for 23 `.ogg` /
`.mp3` pairs and found the frame-based format longer in **23 of 23** by 2.03 to
2.97 frame-times, with the explanation that a frame-based format can only
overshoot. **This is the same question at fifty-eight times the population.**

---

## The reader, and what it refuses

`tools/mp4box.py` walks the ISO/IEC 14496-12 box tree. There is no index and no
directory: a file is a sequence of `u32 size | u32 type | payload`, and the tree
is walked by addition. **A walk that lands exactly on the last byte is evidence;
a walk that lands anywhere else is a refusal**, and the selftest asserts four
kinds of refusal — a truncated tree, a box shorter than its own header, a file
with no File Type Box, and a directory handed to a file reader.

```
python tools/mp4box.py census rpgmakermv-steam     (notes/mp4box-census.txt)

files whose first box is `ftyp`  : 1341
box trees that close at residue 0: 1341 of 1341
bytes over the parsed files      : 473279531

  major brands       : {'M4A ': 1338, 'mp42': 3}
  top-level boxes    : {'ftyp': 1341, 'moov': 1341, 'mdat': 1341, 'free': 826}
  sample rates       : {44100: 895, 22050: 444, 32000: 2}
  channel counts     : {2: 835, 1: 506}
  audioObjectType    : {2: 1341}     (2 is AAC Low Complexity)
  frame length, units: {1024: 1341}
  files with an edit list : 0 of 1341
  total duration, mvhd : 20590.750 s
  total duration, stts : 20590.761 s
  the two agree per file on : 1338 of 1341
```

**The duration is declared three times and this reader prints all three.** The
movie header's claim, the media header's, and what the sample table actually
sums to. On 1,338 files they agree; on three they do not, and
`mp4box.py`'s selftest asserts in advance that the tool must report both rather
than reconcile them — because a reader that quietly prefers one number has
thrown away the only evidence that something is wrong.

### The advisory field that lies on 288 files of 1,341

The `mp4a` sample entry carries a `channelcount` and a 16.16 `samplerate`.
**For AAC both are advisory: ISO/IEC 14496-14 makes the decoder configuration
authoritative**, and the configuration lives in an `esds` descriptor whose
length is a base-128 varint — the one part of MPEG-4 that is not a plain
length-prefixed box.

```
THE ADVISORY FIELDS, AND HOW OFTEN THEY LIE:
  the mp4a box's channelcount disagrees with the decoder
  configuration on 288 of 1341
  the mp4a box's samplerate   disagrees with it on 0 of 1341
```

**A tool reading only the box would have published a channel census wrong on
21 % of its population and closed at residue 0 while doing it.** The first draft
of this reader did exactly that; the disagreement is what caught it, and the
census now prints the authoritative row and the disagreement count beside it.

---

## The join, and the key is not the basename

```
python tools/audiopair.py rpgmakermv-steam --expect-pairs 1341
                                                    (notes/audiopair.txt)

Ogg stems      : 1341   over 1341 files
MPEG-4 stems   : 1341   over 1341 files
in both        : 1341     only Ogg : 0     only MPEG-4 : 0     residue 0

total Ogg    :    20484.642 s over 1341 pairs
total MPEG-4 :    20590.761 s
difference   :      106.119 s   (MPEG-4 minus Ogg)
per pair     :     0.079134 s

MPEG-4 LONGER  : 1341 of 1341
exactly equal  : 0
MPEG-4 SHORTER : 0   <- padding cannot produce this
  1341 + 0 + 0 = 1341, residue 0
```

**The previous object's finding reproduced at fifty-eight times the population,
in 1,341 of 1,341, at residue 0 in both directions.**

**And the first run of this tool was wrong, in a way worth recording.** Keyed on
the file's basename, it paired 497 stems and not 1,341 — because the two
containers sit **side by side in the same directory** (`audio/bgm/Town1.ogg`
next to `audio/bgm/Town1.m4a`) and the same basename recurs in `NewData\`, in
`dlc\BaseResource\` and in eleven other packs. **A basename join silently paired
one directory's Ogg against another directory's MPEG-4.** The key is the path
relative to the root; the denominator caught it; the selftest now asserts that
the same basename in two directories is two pairs and that pairing happens
within a directory and not across one. That is [13](13-corrections.md) C.2.

---

## The overshoot is 2,112 samples, and 2,112 is a number with a name

```
the delta in the MPEG-4 file's OWN frame-times:
  min 0.795898   max 3.061523   mean 2.556483
  by tenth of a frame : {0.7:1, 0.8:1, 0.9:3, 1.1:1, 2.0:62, 2.1:121,
                         2.2:124, 2.3:131, 2.4:145, 2.5:123, 2.6:159,
                         2.7:149, 2.8:103, 2.9:122, 3.0:96}
```

**1,336 of 1,341 exceed one frame-time**, which simple last-frame padding cannot
produce: padding is at most one frame. The band is **[2, 3] frames**, and in
samples it is exact.

```
python _work/delayfit.py                            (notes/audio-delay.txt)

exact fit  m4a_samples == ceil((ogg_samples + D)/1024)*1024,
           same-rate pairs only:
   D = 2112            1069
   D = no exact fit     269      (266 of them resampled)
   D = 0                  2
   D = 1024               1

all pairs     n=1341  min  815.00  max 3135.00  inside [2112, 3136) : 1335
same rate     n=1075  min  815.00  max 3135.00  inside [2112, 3136) : 1069
resampled     n= 266  min 2112.00  max 3122.00  inside [2112, 3136) :  266
```

**The model closes.** An AAC encoder prepends D priming samples and then emits
whole 1,024-sample frames, so the coded length is `ceil((N + D)/1024) × 1024`
and the overshoot lies in `[D, D + 1024)`. **D = 2,112 is Apple's AAC encoder
delay** — not 2,048, which is what two frames would be — and the predicted band
is therefore `[2112, 3136)`.

**The measured extremes are 2,112 and 3,135.** The band's floor is attained and
its ceiling is attained minus one, over 1,341 files.

**1,069 of the 1,075 pairs whose two sides share a sample rate fit the equation
exactly**, with no tolerance. The 266 resampled pairs cannot be tested for exact
equality — the Ogg clock and the MPEG-4 clock do not tick at the same speed, so
converting one sample count into the other introduces a rounding this reader
does not pretend to undo — but **all 266 fall inside the band**.

**So the previous object's explanation is confirmed and sharpened.** It said *a
frame-based format can only overshoot*; the sharper statement is *a frame-based
format overshoots by its encoder's priming delay plus whatever the last frame
had to be padded with, and both terms are constants of the encoder*. That the
same session measured MP3 at 2.03–2.97 frame-times and this one measures AAC at
2.06–3.06 is not a coincidence: **both encoders prime by about two frames**, and
the two measurements are of the same mechanism in two formats.

---

## The two containers are not the same encode

```
pairs agreeing on sample rate    : 1075 of 1341
  (Ogg rate, MPEG-4 rate) : {(44100,44100): 629, (22050,22050): 444,
                             (22050,44100): 264, (32000,32000): 2,
                             (32000,44100): 2}
pairs agreeing on channel count  : 1341 of 1341
MPEG-4 files carrying an edit list : 0 of 1341
```

**266 of 1,341 pairs disagree about the sample rate, and the MPEG-4 side is the
higher one every single time.** 264 pairs are 22,050 Hz Ogg against 44,100 Hz
AAC and two are 32,000 against 44,100; not one pair has the Ogg above the AAC.
**The MPEG-4 set was resampled up**, which costs bytes and adds nothing, and is
what an encoder run with one output setting over a mixed-rate library does.

**The channel counts agree on 1,341 of 1,341** — once they are read from the
place ISO/IEC 14496-14 says to read them. Read from the `mp4a` box they would
have disagreed on 288.

**And no file carries an edit list.** The conventional way to declare that the
priming samples are not part of the recording is an `elst`, and **0 of 1,341
have one** — so a player that honours edit lists gets no correction here, and
the 2,112 samples are at the front of every one of these files.

### What this does NOT establish

**Two files of equal duration are not the same recording.** This chapter
compares clocks. A stem re-recorded at the same length would pair perfectly and
be a different performance, and `audiopair.py`'s selftest asserts that false
positive rather than describing it. **The strongest thing the measurement
supports is that the durations, rates and channel counts are consistent with one
source encoded twice**, and no audio was decoded to check it.

---

## Three files of 1,341, and four measurements pick out the same three

```
python _work/three.py                              (notes/audio-three.txt)

major brand not 'M4A '               : 3
mvhd disagrees with stts             : 3
stts carries a delta other than 1024 : 3
mvhd timescale != mdhd timescale     : 3

mp42 == disagree      : True
mp42 == short frame   : True
mp42 == timescale 90k : True
```

The three are `NewData/audio/me/Gameover2.m4a`, `Mystery.m4a` and `Organ.m4a`,
and every one of the four measurements is independent of the others:

| | the 1,338 | the three |
|---|---|---|
| `ftyp` major brand | `M4A ` | **`mp42`** |
| `mvhd` timescale | the audio's sample rate | **90,000** |
| final `stts` delta | 1,024, like every other frame | **838, 139 and 209** |
| `mvhd` against `stts` | agree | **differ** |

**90,000 is the MPEG-2 systems clock**, and a final frame declared at 139 units
instead of 1,024 is a muxer saying *the recording ends here* rather than *the
last frame is full*. **These three files were written by a different program
from the other 1,338**, and they are the only three in the object whose
containers say so.

**They are also three of the six pairs whose overshoot is under two frames** —
1,024 samples exactly, for all three — because a muxer that trims the last frame
does not have to pad it. `pc-rpgmakervxace-doc` found one flagless Ogg stream in
363 and `pc-rpgmakerxp-doc` found one battler at seven sizes; **three of 1,341
is this object's version of that**, and it took a reader that printed two clocks
instead of one to see it.
