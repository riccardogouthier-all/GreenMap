# GreenMap

**GreenMap** è un servizio online che mostra su una mappa interattiva la posizione dei **coffee shop**, cioè i negozi in cui viene venduta la cannabis.

> ⚠️ **Nota terminologica.** In GreenMap "coffee shop" indica **esclusivamente** i punti vendita di cannabis (secondo l'uso diffuso nei Paesi Bassi e in altri Paesi). **Non** si tratta di caffetterie, bar, tavole calde o ristoranti, che non fanno parte del servizio e non vengono mostrati sulla mappa.

---

## Cos'è

GreenMap permette a chiunque di trovare rapidamente i coffee shop nella zona che gli interessa: si apre la mappa, si cerca una città o ci si geolocalizza, e si vedono i punti vendita con le informazioni essenziali (indirizzo, orari, contatti).

GreenMap è una **directory informativa**: non vende prodotti, non gestisce ordini e non intermedia transazioni.

## Funzionalità

- 🗺️ **Mappa interattiva** con marker per ogni coffee shop
- 📍 **Geolocalizzazione** dell'utente e ricerca "vicino a me"
- 🔎 **Ricerca** per città, indirizzo o nome del locale
- 🧭 **Filtri** (es. aperto ora, valutazione, servizi disponibili)
- 📄 **Scheda dettaglio** per ogni locale: nome, indirizzo, orari di apertura, sito web/telefono, foto
- 🚗 **Indicazioni stradali** tramite link a app di navigazione esterne
- ⭐ **Recensioni e valutazioni** degli utenti (moderate)
- 🔖 **Preferiti** per salvare i locali di interesse
- 🧾 **Segnalazione** di dati errati, locali chiusi o nuovi locali da aggiungere
- 🌍 **Multilingua** (italiano, inglese, olandese, ...)
- 📱 **Design responsive**, utilizzabile da smartphone, tablet e desktop

## Accesso e uso responsabile

- Il servizio è destinato esclusivamente a **maggiorenni**. Al primo accesso viene richiesta la conferma dell'età (*age gate*).
- La legalità della vendita e del consumo di cannabis **varia da Paese a Paese** (e talvolta da città a città). GreenMap riporta le informazioni sui locali ma **non** costituisce consulenza legale: ogni utente è responsabile del rispetto delle leggi locali.
- Sono vietate nel servizio promozioni rivolte a minori e qualsiasi incitamento a un uso irresponsabile.

## Dati di ogni locale

| Campo | Descrizione |
|---|---|
| `id` | Identificativo univoco |
| `name` | Nome del coffee shop |
| `address` | Indirizzo completo |
| `city`, `country` | Località e Paese |
| `lat`, `lng` | Coordinate geografiche |
| `opening_hours` | Orari di apertura |
| `phone`, `website` | Contatti |
| `photos` | Immagini del locale |
| `rating` | Valutazione media |
| `status` | `attivo`, `chiuso`, `in verifica` |
| `updated_at` | Data ultimo aggiornamento |

## Architettura (panoramica)

```
Client (web app)  ──►  API REST  ──►  Database geospaziale
       │                                   │
       └── Libreria mappe (tile + marker)  └── Indici su coordinate
```

- **Frontend:** web app responsive con libreria di mappe (es. Leaflet / Mapbox GL / Google Maps)
- **Backend:** API REST per ricerca, filtri, schede e recensioni
- **Database:** archivio con supporto a query geografiche (es. PostgreSQL + PostGIS)
- **Servizi esterni:** geocoding per la ricerca di indirizzi e città

## API (esempio)

| Metodo | Endpoint | Descrizione |
|---|---|---|
| `GET` | `/api/shops?lat=&lng=&radius=` | Locali entro un raggio dalla posizione |
| `GET` | `/api/shops?city=` | Locali di una città |
| `GET` | `/api/shops/:id` | Dettaglio di un locale |
| `POST` | `/api/shops/:id/reviews` | Aggiunge una recensione |
| `POST` | `/api/reports` | Segnala un errore o un nuovo locale |

## Installazione e avvio in locale

```bash
# clona il repository
git clone <url-del-repository>
cd greenmap

# installa le dipendenze
npm install

# configura le variabili d'ambiente
cp .env.example .env

# avvia in sviluppo
npm run dev
```

### Variabili d'ambiente

| Variabile | Descrizione |
|---|---|
| `DATABASE_URL` | Stringa di connessione al database |
| `MAPS_API_KEY` | Chiave del provider di mappe/geocoding |
| `APP_URL` | URL pubblico dell'applicazione |

## Roadmap

- [ ] Mappa con marker e scheda dettaglio
- [ ] Ricerca e filtri
- [ ] Geolocalizzazione
- [ ] Recensioni e moderazione
- [ ] Account utente e preferiti
- [ ] Multilingua
- [ ] Pannello di gestione per i proprietari dei locali

## Contribuire

Segnalazioni di errori, nuovi locali e miglioramenti sono benvenuti. Apri una *issue* o una *pull request* descrivendo chiaramente la modifica proposta.

## Licenza

Da definire.

---

*GreenMap — trova il coffee shop giusto, ovunque ti trovi.*