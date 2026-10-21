# Kirtan · Sing Along

A sing-aloud reader for kirtans and pads: the Gujarati in easy Roman letters, large enough to
sing from at arm's length, with a plain-English meaning one tap away.

Three collections so far:
- **Chosath Padi** by Nishkulanand Swami: 64 pads, 264 stanzas.
- **Cheshta**: 23 kirtans, 165 stanzas (Kirtan Muktavali 170–192). It includes Premanand Swami's
  Lila Chintamani and Dhyan Chintamani, plus kirtans by Premanand, Nishkulanand and Muktanand
  Swami.
- **Kirtans**: single kirtans from Kirtan Muktavali, added one at a time. So far: *Aaj maare orde re*
  by Premanand Swami (1-270 to 1-273), *Aaj sakhi aanandni heli* by Jeram Brahmachari
  (1-592 to 1-595), and Gopaldas's nine pads on Shri Hari in Amdavad, starting *Ek same
  Amdavadmaa* (2-248 to 2-256).

- **Roman spelling** is made by a script and then checked by ear. It uses plain letters: *aa* for
  the long a, *chh*, *sh*, and no accents. The silent "a" is dropped the way it's spoken
  (*vaat*, *manbhaai*). Words the script gets wrong are listed in
  `_work/scripts/overrides.json`.
- **Meanings** are our own, one per stanza, with short glosses of key words. Every one is a
  draft until reviewed. Every stanza of both collections has one. Readings we are unsure of are
  flagged "To check".
- **Tek**, the refrain, is highlighted. In Cheshta it is shown only where the source marks one,
  with a "↺ back to the tek" cue after each stanza. In Chosath Padi, stanza 1 is taken as the
  tek. **Chhap** marks the stanza carrying the poet's name. **Also sung** gives a variant
  reading.

## Using it

Tap a stanza to open its Gujarati and meaning; on a computer, hovering shows the Gujarati.
Long lines are split at the comma so each half sings as one phrase. For bigger or smaller
text, use the browser's own zoom.

**☰ Index** lists every pad by its first line, A to Z, like the index at the back of a book, with
a letter bar to jump to. **By book** shows them in order by collection instead. Search doesn't need
exact spelling: *aj mare orde* finds *Aaj maare orde*. A link can name a first line too, such as
`stinct9.github.io/kirtan/#aaj-sakhi`.

In the bottom bar:
- **ગુ** shows the Gujarati above every line;
- **☀︎** keeps the screen on while you sing;
- **‹ ›** go to the previous or next pad in the same collection.

**☆** bookmarks a stanza. The ★ panel holds your bookmarks, notes and recently sung pads,
plus **Back up / Restore**. Bookmarks live in this browser only, so back them up now and then.
For the best chance of keeping them, add the reader to your home screen.

## Source and rights

The poems are public domain. The Gujarati text is taken from anirdesh.com
([Chosath Padi](https://www.anirdesh.com/kavya/chosath-padi/),
[Cheshta](https://www.anirdesh.com/kirtan/cheshta.php), and single kirtans from
[Kirtan Muktavali](https://www.anirdesh.com/kirtan/)), and each pad links back there for
listening. anirdesh's own Roman text, translation and footnotes are their work and are not
copied here. The modern invocation that opens their Chosath Padi is left out, as is the closing doha on the
Cheshta page, which falls outside the Kirtan Muktavali numbering.

## Building

```
python3 -I _work/scripts/fetch.py    # once; caches pages in _work/raw/
python3 -I _work/scripts/parse.py    # -> _work/chosath_padi.json (checks: 64 pads, no empty stanza)
python3 -I _work/scripts/parse_cheshta.py   # -> _work/cheshta.json
python3 -I _work/scripts/parse_km.py        # _work/raw/km/km<part>-<no>.html -> _work/kirtans.json
python3 _work/scripts/roman.py       # transliteration self-check
python3 _work/scripts/build.py       # + _work/meanings/*.json -> Reader/data.js
```

Stanza ids never change: `cp-<pad>.<stanza>`, `ch-<Kirtan Muktavali no>.<stanza>` and
`km-<part>-<no>.<stanza>`, with the tek as `.0`. The build refuses to drop one, so bookmarks and
links stay valid. A new collection gets its own id prefix and its own meanings file.
