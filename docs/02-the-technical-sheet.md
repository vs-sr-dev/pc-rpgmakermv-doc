# 02 — the technical sheet: every figure in this repository, with the command that makes it again

*Measure: every row below carries the command that produces it. Nothing on this
page is quoted from the pre-briefing; where a figure here disagrees with the
pre-briefing, the disagreement is in [13](13-corrections.md).*

---

## The tree

| figure | value | command |
|---|---:|---|
| files | **9,641** | `python tools/treecensus.py rpgmakermv-steam` |
| bytes | **2,925,489,709** | as above |
| directories | **406** | as above |
| empty directories | **10** | `python _work/copyverify.py` |
| directories carrying no file | **83** | `python _work/bydir.py` |
| distinct sha1 | **7,417** | `python tools/hashall.py rpgmakermv-steam` |
| extra copies | **2,224** | `python _work/repeats.py` |
| bytes in extra copies | **659,123,163** | as above |
| hashes appearing more than once | **1,351** | as above |
| copies of the commonest hash | **106** | as above (`nwjs-win/locales/*.pak.info`) |
| non-ASCII file names | **5** | `python tools/hashall.py …` under the name guard |

## The shop

| figure | value | command |
|---|---:|---|
| `SizeOnDisk` | **2,925,487,466** | `python tools/steamacf.py --path <manifest> --root rpgmakermv-steam --check` |
| residue against the tree | **−2,243** | as above |
| depot 363891 | **1,466,881,351** | as above |
| depot 363894 | **1,449,233,791** | as above |
| depot 363895 | **9,372,308** | as above |
| depot 363896 | **16** | as above |
| the four depots, summed | **2,925,487,466**, residue **0** | as above |
| depot 363896's files | **8 files of 2 bytes, all named `Locale`, all `65 6e`** | `python tools/depotsplit.py --root rpgmakermv-steam --path 363896=… --rest everything-else --declare 363896=16` |
| build id | **12244690** | `python tools/steamacf.py --path <manifest>` |
| `LastUpdated` | **1695877036** = 2023-09-28 04:57:16 UTC | as above |
| `LastPlayed` | **1775864950** | as above |
| `SharedDepots` | **228985 and 228986, both of app 228980** | as above |
| `BytesToDownload` / `BytesToStage` | **absent** | as above |

## The clocks

| figure | value | command |
|---|---:|---|
| mtime waves | **17** | `python tools/mtimes.py rpgmakermv-steam --waves` |
| waves Steam wrote | **15**, 9,638 files, 2,925,487,253 bytes | `python _work/wavesum.py` |
| waves the owner wrote | **2**, 3 files, 2,456 bytes | as above |
| the seventeen, summed | 9,641 files and 2,925,489,709 bytes, residue **0** | as above |
| wave 1 | 2017-05-07, **6,945 files, 1,598,692,892 bytes** | as above |
| wave 15 | 2023-09-28, **451 files, 452,652,918 bytes** | as above |
| distinct COFF days | **17**, 2013-05-13 to **2047-10-19** | `python tools/pecensus.py rpgmakermv-steam --by-magic` |
| version-1 UUIDs | **731 in 258 files**, **103 distinct node fields** | `python tools/uuidscan.py rpgmakermv-steam` |
| UUIDs with a plausible date | **638 of 731** | as above |
| node fields in more than one file | **56 of 103** | `python _work/addrcount.py` |

## The formats, by magic

| bucket | files | bytes | command |
|---|---:|---:|---|
| specified | **9,384** | **2,786,158,378** | `python tools/coverage.py tree --root rpgmakermv-steam` |
| decoded | **222** | **89,662,863** | as above |
| derived | 0 | 0 | as above |
| opaque | **35** | **49,668,468** | as above |
| — before this session | 7,806 / 2,100,016,569 specified, 1,835 / 825,473,140 opaque | `notes/coverage-tree-before.txt` |

## By extension — 34 rows, summing to 9,641 and 2,925,489,709

| ext | files | bytes | ext | files | bytes |
|---|---:|---:|---|---:|---:|
| `.png` | 5,578 | 733,723,600 | `.ogg` | 1,341 | 684,463,713 |
| `.m4a` | 1,341 | 473,279,531 | `.dll` | 92 | 335,115,552 |
| `.zip` | 1 | 205,182,933 | `.so` | 5 | 147,013,560 |
| `.pak` | 222 | 89,662,863 | `.info` | 159 | 63,826,999 |
| (none) | 73 | 54,206,679 | `.exe` | 9 | 43,651,584 |
| `.dat` | 4 | 40,494,112 | `.js` | 218 | 13,147,515 |
| `.html` | 147 | 7,814,014 | `.ttf` | 5 | 7,708,840 |
| `.nexe` | 2 | 7,211,744 | `.qm` | 24 | 4,873,554 |
| `.bin` | 6 | 4,300,802 | `.json` | 129 | 4,286,178 |
| `.dylib` | 13 | 3,348,192 | `.txt` | 192 | 810,693 |
| `.qmltypes` | 10 | 386,156 | `.qml` | 40 | 356,596 |
| `.node` | 1 | 353,792 | `.rb` | 3 | 155,214 |
| `.jpg` | 1 | 73,307 | `.plist` | 6 | 4,301 |
| `.css` | 6 | 18,332 | `.docx` | 1 | 16,645 |
| `.log` | 2 | 2,405 | `.conf` | 3 | 120 |
| `.desktop` | 1 | 88 | `.vdf` | 1 | 51 |
| `.rpgproject` | 4 | 44 | `.lproj` | 1 | 0 |

`python tools/treecensus.py rpgmakermv-steam`. **No `.chm`, no `.rvdata2`, no
`.rxdata`, no `.lmu`, no `.mid` and no `.wav`.** Exactly one `.jpg` in 9,641
files.

## By top-level subtree

| name | files | bytes | share |
|---|---:|---:|---:|
| `dlc` | 4,612 | 1,458,606,099 | 49.8585 % |
| `NewData` | 1,101 | 403,792,717 | 13.8026 % |
| (root) | 37 | 323,097,210 | 11.0442 % |
| `nwjs-win-test` | 152 | 232,540,106 | 7.9488 % |
| `nwjs-lnx` | 122 | 202,552,945 | 6.9237 % |
| `nwjs-win` | 125 | 159,791,316 | 5.4620 % |
| `Help` | 491 | 47,622,147 | 1.6278 % |
| `tutorial-win` | 40 | 45,369,543 | 1.5508 % |
| `tutorial-osx` | 49 | 22,551,339 | 0.7709 % |
| `qtwebengine_locales` | 53 | 14,282,881 | 0.4882 % |
| `Generator` | 2,738 | 9,283,272 | 0.3173 % |

`python tools/treecensus.py rpgmakermv-steam`; the shares recomputed in exact
decimal by `python _work/bydir.py`.

## Entropy

| family | mean H | family | mean H |
|---|---:|---|---:|
| `.ZIP` | **7.9970** | `.OGG` | 7.9579 |
| `.PNG` | 7.9555 | `.M4A` | 7.9379 |
| `.JPG` | 7.7568 | `.EXE` | 7.1014 |
| `.TTF` | 6.8458 | `.DLL` | 6.7814 |
| `.SO` | 6.3261 | `.DAT` | 6.1735 |
| `.PAK` | 5.6307 | `.QM` | 5.0254 |
| `.HTML` | 5.0083 | `.JS` | 4.9957 |
| `.RB` | 4.7509 | `.QML` | 4.7200 |
| `.JSON` | **3.8035** | | |

`python tools/entropy.py rpgmakermv-steam --tree --by-ext`; **35,810 of 51,926
blocks above 7.5**. `.JSON` is the least compressed family in the tree, against
the previous object's `.RVDATA2` at 2.0714 and the one before's `.RXDATA` at
3.8587 — **both quoted from those repositories' own `docs\`.**

## The pictures, the music and the fonts

| figure | value | command |
|---|---:|---|
| PNG parsed | **5,578 of 5,578**, residue 0 | `python tools/pngcensus.py rpgmakermv-steam --by-dir` |
| PNG chunk CRC-32 | **91,607 of 91,607** | as above |
| IHDR shapes | 5: depth 4 palettised ×4, depth 8 truecolour ×1,102, depth 8 palettised ×561, depth 8 truecolour+alpha ×3,903, **depth 16 truecolour+alpha ×8** | as above |
| interlaced PNG | **0** | as above |
| Ogg parsed | **1,341 of 1,341**, residue 0 | `python tools/oggcensus.py census rpgmakermv-steam` |
| Ogg page CRC | **144,905 of 144,905** | as above |
| Ogg with an EOS flag on the last page | **1,341 of 1,341** | as above |
| Ogg total time | **20,484.642 s** | as above |
| MPEG-4 box trees closing on the last byte | **1,341 of 1,341** | `python tools/mp4box.py census rpgmakermv-steam` |
| MPEG-4 total time, from `stts` | **20,590.761 s** | as above |
| audio stems in both containers | **1,341**, residue 0 both ways | `python tools/audiopair.py rpgmakermv-steam` |
| fonts | **5 sfnt**, 7,708,840 bytes | `python tools/coverage.py tree --root rpgmakermv-steam` |

## The programs

| figure | value | command |
|---|---:|---|
| binaries, all formats | **149**, 590,874,844 bytes | `python _work/native.py` |
| PE / MZ | **102**, 379,120,928 | as above |
| ELF | **20**, 188,948,352 | as above |
| Mach-O | **19**, 22,524,976 | as above |
| Unix `ar` | **8**, 280,588 | as above |
| PE32 / PE32+ | **101 / 1** | `python tools/pecensus.py rpgmakermv-steam --by-magic` |
| Authenticode | **6 of 102** | as above |
| `stampcheck` hits | **8 of 102** — T1 ×2, T2 ×6, T3 ×0 | `python tools/stampcheck.py rpgmakermv-steam` |
| `mzcensus` | **9 of 102** | `python tools/mzcensus.py rpgmakermv-steam` |
| `sigcount --hex 4d5a5000` | **0 beginning, 1 anywhere** — in `dlc/BaseResource/audio/bgm/Dungeon5.ogg` | `python tools/sigcount.py rpgmakermv-steam --hex 4d5a5000` |
| protection markers | **0 of 11**, control firing on **102 of 102** | `python tools/protscan.py rpgmakermv-steam` |
| third-party components listed | **1,674**, 1 carrier | `python tools/vendorhash.py rpgmakermv-steam` |
| companies with no probe | **1 of 6** | `python tools/vendorhash.py rpgmakermv-steam --survey` |

## The database and the text

| figure | value | command |
|---|---:|---|
| JSON documents | **129**, 4,286,178 bytes | `python _work/jsonprobe.py` |
| parsing cleanly | **128 of 129** | as above |
| arrays with `null` at index 0 | **83 of 83** | as above |
| distinct object keys | **153** | as above |
| Fantasy databases, files agreeing on record count | **8 of 9** | `python tools/jsondiff.py …NewData_FantasyEN/data …NewData_FantasyJP/data` |
| `Items.json` records | **35 English, 30 Japanese** | as above |
| e-mail shapes | **561 in 30 blobs** | `python tools/sift.py rpgmakermv-steam --group personal` |
| distinct addresses among them | **92 over 64 domains** | `python _work/addrcount.py` |
| drive-letter build paths | **2,314 in 44 files** | `python tools/sift.py rpgmakermv-steam --group buildpath` |
| Unix build paths | **15,529 in 411 files** | as above |
| `Kadokawa` | **96 in 45 at eight bits, 9 in 3 at sixteen** | `python tools/namescan.py rpgmakermv-steam --name Kadokawa …` |
| `Yoji Ojima` | **95 in 54** | as above |
| `Yukihiro Matsumoto` / `Neil Hodgson` / `Scintilla` | **0 / 0 / 0** | as above |
| `pixi` | **8,625 in 47** | as above |

## Against the collection

| figure | value | command |
|---|---:|---|
| `-doc` directories | **137** | `ls -1d ../*-doc/ \| wc -l` |
| `pc-*-doc` directories | **68** | `ls -1d ../pc-*-doc/ \| wc -l` |
| repositories swept | **107** | `python tools/crossall.py notes/sha1-all.txt --collection .. --skip pc-rpgmakermv-doc` |
| list files swept | **477** | as above |
| hash tokens read | **161,543** | as above |
| crossings | **297 of 7,417** | as above |
| crossings with two partners | **21** | `python _work/crosssplit.py` |
| crossings keeping their base name | **266 of 281** | `python tools/crossnames.py notes/sha1-all.txt ../pc-rpgmakervxace-doc/notes/sha1-all.txt` |

## The box

| figure | value | command |
|---|---:|---|
| tools before this session | **562**, 0 differing from the previous object's | `notes/toolsdiff-before.txt` |
| tools after | **568** | `python tools/toolsdiff.py ../pc-rpgmakervxace-doc/tools` |
| readers pointed by the harness | **91**, 58 refusing | `python tools/refusals.py rpgmakermv-steam` |
| `argparse` refusals | **23**, for the **eighth** time | `python tools/refusalclass.py notes/refusals.txt` |
| tools raising on a directory | **216 of 561** before, unchanged | `notes/dirguard-survey-before.txt` |
| tools dying on a non-Latin-1 name | **7 of the 10 that emit one** | `notes/nameguard-survey-before.txt` |
| P22's list — pointable and not pointed | **227 of 260 pointable, of 568** | `python _work/p22list.py` |
