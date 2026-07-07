# Miten ohjelmoin Hermeksen myyntiassistentiksi – konkreettiset askeleet

Hermes pyörii Hostingerissa, Slack + WhatsApp yhdistetty, Obsidian-vault GitHubissa. Ohjelmointi tapahtuu KOLMESSA kerroksessa – tee järjestyksessä:

## Kerros 1: System prompt (5 min) — TEE HETI

Avaa Hermeksen agenttiasetukset (Hostingerissa se paikka, jossa system prompt / ohjeteksti määritellään; jos käytät omaa koodia, se on system-viestin sisältö). LISÄÄ loppuun tämä lohko (älä poista mitään olemassa olevaa):

```
MYYNTIMODUULI:
Kun käyttäjän pyyntö koskee myyntiä, liidejä, puheluita, tarjouksia tai asiakkaita:
1. Lue ensin vaultista tiedosto "01 - Agentin muisti/Hermes myyntiohjeet.md" ja noudata sitä tarkasti.
2. Myynnin työtila on kansio "09 - Myynti". Älä koske muihin kansioihin myyntitehtävissä.
3. Tunnista nämä komennot ja suorita ne myyntiohjeiden mukaan:
   "aamuraportti", "analysoi puhelu", "viikkoraportti", "sparraa [vastaväite]",
   "pisteytä [yritys]", "scriptianalyysi".
4. Et koskaan poista tiedostoja, et muokkaa käyttäjän omia puhelumuistiinpanoja,
   et lähetä mitään asiakkaille. Viestiluonnokset aina käyttäjän hyväksyttäväksi.
5. Vastaa suoralla suomella, ei hypeä. Priorisoi aina: mikä tuo rahaa nopeimmin.
```

Miksi näin: komennot ja säännöt elävät vaultissa ([[Hermes myyntiohjeet]]), joten voit parantaa niitä muokkaamalla md-tiedostoa – system promptiin koskematta.

## Kerros 2: Testaa komennot (10 min)

Lähetä Hermekselle WhatsApp/Slack-viestinä järjestyksessä ja tarkista tulos:

1. `pisteytä Esimerkki Katto Oy, Seinäjoki, 6 hlö, mainostaa Googlessa, tj Pekka 040-123` → pitää palauttaa pisteet perusteluineen ja kirjata liidikorttiin
2. `sparraa liian kallis` → pitää alkaa roolipeli
3. `aamuraportti` → pitää syntyä tiedosto `09 - Myynti/00 - Ohjaus/` -kansioon (alussa laiha, koska dataa ei ole – se on ok, EI saa keksiä dataa)
4. `analysoi puhelu` (kun ensimmäinen oikea puhelumuistiinpano on olemassa)

Jos jokin ei toimi: ongelma on lähes aina siinä, ettei Hermes löydä/lue vault-tiedostoa → varmista että Personal Obsidian Brain -skill lukee myös `09 - Myynti`- ja `01 - Agentin muisti` -kansiot, ja että git-synkka (pull) ajetaan ennen lukua.

## Kerros 3: Ajastus n8n:llä (30–60 min)

Aamuraportin EI pidä odottaa että pyydät sitä. `Flowly - Aamuraportti.json` (tässä kansiossa) hoitaa: joka aamu 7:00 → lukee liidikortit GitHubista → LLM koostaa raportin → Telegram + tallennus vaultiin. Asennus: [[n8n asennus - ChatGPT-prompt]].

## Työnjako (tärkeä ymmärtää)

- **n8n** = ajastukset ja putket (aamuraportti, follow-up-pingit, liidihaku)
- **Hermes** = keskustelu, analyysi, sparraus, kirjoittaminen vaultiin pyynnöstä
- **Sinä** = puhelut, hinnat, lupaukset, päätökset

Älä rakenna samaa asiaa molempiin. Jos jokin toimii Hermes-komennolla, ajasta se n8n:llä vasta kun käytät sitä oikeasti päivittäin.
