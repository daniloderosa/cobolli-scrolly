# L'ascesa di Cobbo

**Scrollytelling interattivo sull'ascesa di Flavio Cobolli nel tennis mondiale.**

Live: https://daniloflorenzano.github.io/cobolli-scrolly/

---

## Di cosa si tratta

Un longform data journalism interattivo che racconta la carriera di **Flavio Cobolli** (Roma, 2002), tennista italiano passato dal ranking #480 (2021) al career high **#17** (luglio 2025).

Il formato è quello dello **scrollytelling**: scorrendo la pagina, il testo narrativo attiva grafici e visualizzazioni che illustrano i dati statistici del giocatore.

### Contenuti

- **Ranking ATP nel tempo** — Grafico lineare dal 2021 al 2025, con annotazioni sui momenti chiave (Finale Washington 2024, Titolo Amburgo 2025, QF Wimbledon 2025)
- **Win rate per superficie** — Confronto carriera vs ultime 52 settimane su terra, erba e cemento
- **Efficacia contro top avversari** — Lollipop chart carriera vs recente contro Top 10, Top 20, Top 50
- **Timeline 2025** — Gli eventi chiave dell'anno di svolta: Amburgo, Roland Garros, Wimbledon, Davis Cup

---

## Stack tecnico

| Tecnologia | Uso |
|---|---|
| [SvelteKit](https://svelte.dev) | Framework applicazione |
| [LayerChart](https://layerchart.com) | Grafico ranking ATP (Area + Spline) |
| [D3.js](https://d3js.org) | Scale e utilità dati |
| HTML/CSS puro | Surface chart, lollipop chart, timeline |
| Google Fonts | Playfair Display · IBM Plex Sans · IBM Plex Mono |

Design ispirato allo stile **data journalism editoriale** (NYT / The Pudding), con tema dark, tipografia mista serif/mono e palette cromatica caldo-sobria.

---

## Sviluppo locale

```bash
npm install
npm run dev
```

Apri [http://localhost:5173](http://localhost:5173).

---

## Deploy su GitHub Pages

Il deploy avviene automaticamente via GitHub Actions a ogni push su `main`.

Per configurare il tuo fork:
1. Vai su **Settings → Pages** del repository
2. Imposta **Source → GitHub Actions**
3. Fai push su `main` — la Action costruisce e pubblica il sito

Il base path (`/cobolli-scrolly`) viene iniettato automaticamente dal workflow tramite la variabile `BASE_PATH`.

---

## Realizzazione

Questo progetto è stato **realizzato interamente da [Claude Code](https://claude.ai/claude-code)** (Anthropic), l'agente AI per lo sviluppo software, su richiesta dell'utente.

Tutti i componenti Svelte, gli stili CSS, le visualizzazioni dati e la configurazione di deploy sono stati scritti autonomamente da Claude Code in un'unica sessione di lavoro.

---

*Dati statistici aggiornati a luglio 2025. Fonte: ATP Tour / Tennis Abstract.*
