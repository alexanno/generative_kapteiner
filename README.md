# Generative Kapteiner

Et generativt kunstverk som skriver skipsdagbøker som aldri ble skrevet — forankret i ekte steder, ekte vær og en kapteins stemme fra en annen tid.

## Hvordan det virker

1. Tilfeldig fyr velges fra Kystverkets database
2. Sanntidsvær hentes fra Met.no sitt API for det valgte fyret
3. Historiske skipsdagbøker brukes som stilreferanse
4. En systeminstruks binder alt sammen til ett prompt
5. Gemma 4 31B (via Ollama) genererer én dagbokoppføring
6. Resultatet lagres som Markdown og indekseres i `registry.json`

Kjøres automatisk på ulike dager og tidspunkter via GitHub Actions.

## Kjøre lokalt

```bash
uv run main.py --output markdown
```

Krever [Ollama](https://ollama.ai) kjørende lokalt med `gemma4:31b-cloud` eller tilsvarende modell.

### Flagg

| Flagg | Verdier | Standard |
|---|---|---|
| `--output` | `shell`, `markdown`, `webhook` | `shell` |
| `--model` | Ollama-modellnavn | `gemma4:31b-cloud` |
| `--webhook-url` | URL | — |

## Prosjektstruktur

```
loggbok_robot/
├── main.py                        # Hovedskript
├── fyrlykter_sorlandet.geojson   # Fyrlykt-database (Kystverket)
├── index.html                     # Visning av loggbøkene
├── om.html                        # Om prosjektet
├── logs/                          # Genererte oppføringer (Markdown)
├── registry.json                  # Indeks over alle oppføringer
└── samples and plans/             # Referanseeksempler og notater
```

## Kilder

- [Ships Logs Collection — FromThePage](https://fromthepage.com/nharl/ships-logs-collection/ms220-log4)
- [Najaden — norsk skipsdagbok (UiO-arkiv)](https://web.archive.org/web/20041229065525/http://heim.ifi.uio.no/~oddharry/dsfmc/etext/najaden.html)
- [Navigasjonsinstallasjoner WFS — Geonorge / Kystverket](https://kartkatalog.geonorge.no/metadata/navigasjonsinstallasjoner-wfs/73e46cf4-d9f5-4d75-b148-bb5edf888c4a)
- [Locationforecast 2.0 — Meteorologisk institutt](https://api.met.no/weatherapi/locationforecast/2.0/documentation)
