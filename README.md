# Meelium Gene Pro

**mp3 sisse → Suno-valmis pakett välja.** Brauseripõhine loo-analüsaator ja
prompti-koostaja Suno AI jaoks. Üks HTML-fail, null sõltuvust — ava
topeltklõpsuga ja kõik töötab. Ühtegi faili ei laadita kuhugi üles;
analüüs jookseb täielikult sinu brauseris.

*A browser-based track analyzer and Suno AI prompt packager. One HTML file,
zero dependencies, fully client-side — your audio never leaves your machine.
UI available in Estonian and English (toggle top-right).*

## Mida ta teeb

- **Analüüs:** tempo (BPM), taktimõõt, helistik, akordijärgnevus + levinuim
  progressioon (Rooma numbritega), sektsioonistruktuur rollidega
  (intro/salm/refrään/…), energia- ja valjuskõver, dünaamika (crest, DR),
  spektraalbalanss, stereopilt, meloodiakontuur, modulatsioonid.
- **Kuulamine ja toimetamine:** sisseehitatud pleier, sektsioonide
  esitamine ja loop, piiride lohistamine, poolitamine ja liitmine.
- **Võrdlus:** A/B kahe loo mõõdikute kõrvutus, albumirežiim mitme failiga,
  voogedastuse valjussihid (Spotify −14 / Apple −16).
- **Suno pakett:** täisprompt style-väljale, struktuur täissiltidega
  (akordid + emotsioonid) lüürikaväljale, laulusõnade prompti generaator,
  promptide raamatukogu, MIDI- ja raportieksport.

## Kasutamine

1. Ava `index.html` brauseris (Chrome/Edge/Firefox).
2. Lohista sisse mp3/wav/m4a — või mitu korraga albumirežiimi jaoks.
3. Käi sakid läbi, kohenda sektsioone kõrva järgi, kopeeri pakett Sunosse.

## Arendus

Projekti kontekst ja reeglid Claude Code'i jaoks on failis
[CLAUDE.md](CLAUDE.md). Lühidalt: vanilla JS, neli script-plokki,
kõik UI-stringid läbi I18N sõnastiku, versiooninumber kuues kohas.

## Litsents

MIT — vt [LICENSE](LICENSE).

---
*Osa Meeliumi Machina-seeria tööriistadest · [suno.ee](https://suno.ee)*
