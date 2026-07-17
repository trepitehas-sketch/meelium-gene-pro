# Meelium Gene Pro — projekti kontekst

Suhtle kasutajaga eesti keeles.

## Mis see on

Brauseripõhine mp3-analüsaator + Suno AI prompti-paketikoostaja. Üks fail
(`index.html`), null sõltuvust, null build-sammu — kogu analüüs (FFT, BPM,
helistik, akordid, struktuur, valjus, spekter, stereo, meloodiakontuur)
jookseb kasutaja brauseris Web Audio API-ga; midagi ei laadita serverisse.

Autor: Meelium (digiloome-muusika artist). Tööriist on osa Machina-seeriast
(Opus Machina, Velvet Machina jt) ja mõeldud jagamiseks Suno Klubi
kogukonnas (suno.ee).

## Faili ehitus (index.html, ~1480 rida)

Neli eraldi `<script>` plokki, igaüks `"use strict"` all — funktsioonid on
globaalsed ja plokid sõltuvad eelnevatest:

1. **Analüüsimootor** — `fft()`, `analyzeBuffer()`, Krumhansl-helistik,
   akorditemplaadid, sektsioonituvastus (novelty-kõver), konstandid
   (sr=22050, N=1024, HOP=512, MIN_SEG=7s, akordilävi 0.55).
2. **Sõnastikud ja loogika** — `VOCAB` (10 žanri sildikaardistust),
   `PRESETS` (rippmenüüde valikud), `I18N` (ET/EN, ~80 võtit), `App` olek,
   pleier (`playFrom`/`pausePlay`/`tick`), `recomputeSegs()`, Suno tekstide
   koostajad (`fullPromptText`, `structureText`, `lyricsPromptText`,
   `mergeLyrics`).
3. **Renderdus** — SVG graafikud (`svgEnergy`, `svgChords`, `svgLoud`,
   `svgBands`, `svgMelody`), `renderAll()`, album/võrdlustabelid,
   MIDI-eksport (`exportMidi`), raamatukogu (localStorage võti
   `formaMachinaLibrary` — ÄRA muuda, vanad salvestused lähevad kaotsi),
   raportid (`exportJson`, `exportTxt`).
4. **Sündmused ja init** — failide laadimine/dekodeerimine, piiride
   lohistamine (pointer-sündmused), delegeeritud klõpsu/muutuse kuularid,
   `applyLang()`, `initManualGrid()`.

## Reeglid muudatuste tegemisel

- Jää vanilla JS-i juurde: ei mingeid teeke, raamistikke ega build-tööriistu.
  Kogu väärtus on selles, et fail avaneb topeltklõpsuga.
- Iga kasutajale nähtav string käib läbi `I18N` sõnastiku (`t("võti")`) —
  lisa alati nii `et` kui `en` tõlge. Staatilised HTML-elemendid uuendatakse
  `applyLang()`-is id-de kaudu (prefiks `i-`).
- Versiooninumber elab KUUES kohas — muuda kõiki korraga:
  `<title>`, päise seeriarida, jalus, `reportObj()` tool-väli,
  `exportTxt()` päis, ja commit'i sõnum. Versioneerimine: v2.1, v2.2 …
- Uued sektsioonirollid: lisa `ROLES`, `ROLE_COLORS`, `ROLE_LBL` (et+en)
  JA igasse `VOCAB` žanrikaardistusse.
- Segmentide muutmise järel (piirid, poolitamine, rollivahetus) kutsu alati
  `recomputeSegs(T)` ja siis `renderAll()`.
- Pleieri playhead-jooned on `id="ph1"`/`id="ph2"` — SVG uuesti renderdamisel
  peavad need alles jääma.

## Testimine

Automaatteste pole. Käsitsi kontroll:
1. `node --check` igale script-plokile (ekstrakti nt
   `python3 -c "..."` abil või ava fail brauseris ja vaata konsooli).
2. Ava `index.html` brauseris, lohista sisse mõni mp3, käi läbi kõik 6 sakki.
3. Kontrolli mõlemat keelt (EN/ET nupp paremal üleval).
4. Kui muutsid analüüsimootorit: võrdle BPM/helistik tulemust mõne teadaoleva
   looga (nt 128 BPM house-lugu peab andma 128±2).

## Teadaolevad piirangud (ära "paranda" ilma küsimata)

- Akordituvastus taandab kõik maj/min kolmkõladeks — teadlik lihtsustus.
- Helistik on chroma-korrelatsioon, mitte absoluutne tõde; Suno ise
  transponeerib lugusid vabalt.
- localStorage raamatukogu on brauseri+domeeni põhine — failiversioonilt
  veebiversioonile kolides see kaasa ei tule.
