# Myyntijärjestelmä – lue ensin

Tämä kansio on Flowlyn myyntikone. Se on erillinen muusta vaultista – mitään vanhaa ei ole siirretty tai poistettu.

## Kansiot

- **00 - Ohjaus** — Hermeksen aamuraportit ja viikkoraportit tulevat tänne
- **10 - Liidit** — yksi tiedosto per yritys (liidi JA asiakas = sama kortti, status vaihtuu)
- **20 - Puhelut** — yksi tiedosto per puhelu, sisältää myös analyysin
- **30 - Tarjoukset** — yksi tiedosto per tarjous
- **40 - Scriptit** — cold call -scriptit, vastaväitepankki, viestipohjat, A/B-testit
- **50 - Analyysit** — voitot, häviöt, caset
- **60 - Tieto** — palvelupaketit, toimialatieto
- **90 - Templatet** — valmiit pohjat (aseta Obsidianin Templates-pluginin kansioksi tai kopioi käsin)
- **95 - n8n** — valmis workflow-JSON + asennusohjeet

## Tagit (vain nämä)

`#status/uusi` `#status/soitettu` `#status/kiinnostunut` `#status/tarjous` `#status/asiakas` `#status/hävitty` `#status/myöhemmin` + `#toimiala/katto` (tms.) + `#kuuma` (pisteet 70+)

## Päivittäinen kierto

1. **Aamu:** n8n tuottaa aamuraportin → 00 - Ohjaus + Telegram
2. **Ennen soittoja:** 10 min harjoitus Hermeksen kanssa (ks. [[Harjoitusohjelma]])
3. **Jokaisen puhelun jälkeen:** täytä [[Puhelu ja analyysi]] -template 20 - Puhelut-kansioon (2 min) → pyydä Hermekseltä "analysoi puhelu"
4. **Ilta:** täytä päivän rivi + huomisen 3 tärkeintä
5. **Sunnuntai:** "viikkoraportti" Hermekseltä

## Hermeksen oikeudet tässä kansiossa

- SAA muokata: 00 - Ohjaus, liidikorttien Pisteet- ja Hermes-osiot, 50 - Analyysit, scriptien EHDOTUS-osiot
- EI SAA muokata: puhelumuistiinpanojen omat havainnot, tarjousten hinnat/lupaukset, scriptien AKTIIVINEN-osiot, ei poistaa mitään

Koko strategia: [[Myyntikone-suunnitelma]]
Hermeksen ohjelmointi: [[Hermes myyntiohjeet]] (01 - Agentin muisti)
