# n8n-workflown asennus

Workflow: [[Flowly - Aamuraportti.json]] (tässä kansiossa). Se tekee joka aamu klo 7:00 (ma–la):
1. lukee kaikki liidikortit GitHub-repostasi kansiosta `09 - Myynti/10 - Liidit`
2. koostaa niistä aamuraportin LLM:llä (OpenRouter, Claude)
3. lähettää raportin Telegramiin JA tallentaa sen vaultiin `00 - Ohjaus` -kansioon

## Ennen asennusta tarvitset (placeholderit JSON:ssa)

| Placeholder | Mikä | Mistä |
|---|---|---|
| `GITHUB_OMISTAJA/GITHUB_REPO` | vault-repon omistaja/nimi | GitHub-repon URL:sta |
| GitHub-token | Fine-grained PAT, vain tähän repoon, Contents: Read & Write | github.com → Settings → Developer settings → Personal access tokens |
| OpenRouter API-avain | LLM-kutsuille | openrouter.ai → Keys |
| Telegram-botti + chat id | raportin vastaanotto | @BotFather → /newbot; chat id: lähetä botille viesti ja avaa api.telegram.org/bot<TOKEN>/getUpdates |

Huom: raportti syntyy GitHubiin → näkyy Obsidianissa vasta kun git pull ajetaan. Laita Obsidian Git -pluginiin auto-pull (esim. 10 min välein), tai luota Telegram-viestiin aamulla.

---

## Kopioi tästä alaspäin kaikki ChatGPT:lle (tai mille tahansa AI-avustajalle):

```
Toimi n8n-asiantuntijana ja asenna kanssani valmis workflow vaihe vaiheelta. Älä hypi vaiheiden yli, varmista jokaisen vaiheen onnistuminen ennen seuraavaa, ja jos jokin epäonnistuu, debuggaa se kanssani ennen jatkamista.

TILANNE:
- Minulla on n8n (kerro minulle ensin miten tarkistan onko se cloud vai self-hosted, ja toimi sen mukaan)
- Minulla on valmis workflow-JSON-tiedosto nimeltä "Flowly - Aamuraportti.json"
- Workflow: Schedule (cron 0 7 * * 1-6) → GitHub API (listaa .md-tiedostot kansiosta "09 - Myynti/10 - Liidit") → Code (suodatus) → HTTP (lataa tiedostot) → Code (kokoaa aineiston ja system promptin) → OpenRouter chat completions (model anthropic/claude-sonnet-4.5) → Code (Telegram-teksti + base64-commit) → Telegram sendMessage JA GitHub PUT (tallentaa raportin polkuun "09 - Myynti/00 - Ohjaus/{pvm} Aamuraportti.md")
- Obsidian-vaulttini on GitHub-repossa
- HTTP-nodet käyttävät authentikointina Header Auth -credentiaaleja (genericCredentialType / httpHeaderAuth)

OHJAA MINUT NÄIDEN VAIHEIDEN LÄPI, YKSI KERRALLAAN:

VAIHE 1 – GitHub-token: Fine-grained personal access token, pääsy VAIN vault-repooni, oikeudet Contents: Read and write. Näytä tarkat klikkaukset.

VAIHE 2 – OpenRouter-avain: openrouter.ai, avaimen luonti ja pienen saldon lataus.

VAIHE 3 – Telegram-botti: @BotFather /newbot, tokenin talteenotto, ja chat id:n selvitys (lähetän botille viestin ja haen id:n getUpdates-osoitteesta). Näytä tarkka URL.

VAIHE 4 – Workflown tuonti: n8n → uusi workflow → Import from file → valitsen JSON-tiedoston.

VAIHE 5 – Credentiaalit n8n:ään, tarkalleen näin:
a) Header Auth -credential nimellä "GitHub Token": Name-kenttä "Authorization", Value "Bearer <github-token>". Valitsen tämän molempiin GitHub-HTTP-nodeihin ("Hae liidikansio (GitHub)" ja "Tallenna raportti vaultiin (GitHub)").
b) Header Auth -credential nimellä "OpenRouter": Name "Authorization", Value "Bearer <openrouter-avain>". Valitsen tämän nodeen "LLM koostaa raportin (OpenRouter)".
c) Telegram-credential bot-tokenilla nodeen "Lähetä Telegramiin".

VAIHE 6 – Placeholderien vaihto:
a) Molemmissa GitHub-nodeissa URL:iin oikea "GITHUB_OMISTAJA/GITHUB_REPO"
b) Telegram-nodeen oikea chatId ("VAIHDA_TELEGRAM_CHAT_ID" tilalle)

VAIHE 7 – Testaus: aja workflow käsin (Execute workflow). Käy kanssani läpi mitä jokaisen noden outputista pitäisi näkyä, ja auta tulkitsemaan virheet. Yleisimmät: 401 (väärä token/Bearer puuttuu), 404 (väärä repo tai kansiopolku – huomaa että polussa on välilyöntejä: "09 - Myynti/10 - Liidit"), Telegram "chat not found" (väärä chat id tai en ole aloittanut keskustelua botin kanssa).

VAIHE 8 – Aktivointi: kytke workflow aktiiviseksi ja varmista että n8n:n aikavyöhyke on Europe/Helsinki (workflown settings + instanssin asetus).

Kysy minulta aina vaiheen lopuksi "toimiiko, mitä näet ruudulla?" ennen kuin jatkat.
```
