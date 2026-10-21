# 🌊 Nautilus Dive Datasets

Raccolta di dataset geografici open-data con siti di immersione, relitti storici, barriere coralline, parchi archeologici sommersi e fauna marina per l'app mobile **Nautilus**.

I dataset sono strutturati per **macro-aree geografiche**, consentendo all'utente di scaricare su richiesta solo la regione di interesse (es. vacanza a Creta / Mar Egeo) e visualizzare tutti i siti sulla mappa interattiva senza appesantire il pacchetto iniziale dell'applicazione.

---

## 🗺️ Regioni Disponibili

| ID Regione | Nome | Copertura Geografica | Formati |
|---|---|---|---|
| `aegean-sea` | **Mar Egeo & Creta** | Creta (Chania, Drepano, Plakias, Heraklion, Agia Pelagia, Elounda Olous), Cicladi (Kea Britannic, Mykonos Anna II, Santorini Caldera, Iraklia), Sporadi (Alonissos Museo Sommerso di Peristera), Dodecaneso (Rodi, Leros). | [JSON](./aegean-sea.json) · [GeoJSON](./aegean-sea.geojson) |
| `tyrrhenian-ligurian` | **Mar Tirreno & Mar Ligure** | Parco Archeologico Sommerso di Baia, Superpetroliera MT Haven, Cristo degli Abissi di Portofino, Scoglio del Medico a Ustica, Nasim II a Giannutri, Grotte carsiche di Palinuro. | [JSON](./tyrrhenian-ligurian.json) · [GeoJSON](./tyrrhenian-ligurian.geojson) |
| `ionian-adriatic` | **Mar Ionio & Mar Adriatico** | Città preistorica sommersa di Pavlopetri, Sommergibile HMS Perseus (Cefalonia), Relitto Nicole (Otranto), Piroscafo SS Baron Gautsch (Rovigno/Istria). | [JSON](./ionian-adriatic.json) · [GeoJSON](./ionian-adriatic.geojson) |
| `red-sea-north` | **Mar Rosso Settentrionale** | SS Thistlegorm, Relitto Giannis D (Abu Nuhas), Blue Hole di Dahab, Parco Marino di Ras Mohammed (Shark & Yolanda). | [JSON](./red-sea-north.json) · [GeoJSON](./red-sea-north.geojson) |

---

## 📊 Formati di Distribuzione

Ciascuna area geografica è distribuita in due formati sincronizzati:

1. **`*.json` (Nautilus Native Catalog)**:
   - Compatibile al 100% con il tipo `CatalogSite` di Nautilus (`src/data/sitesCatalog.ts`).
   - Include metadati bilingue (`name.en`, `name.it`), livello (`beginner`, `intermediate`, `advanced`, `technical`), profondità min/max (`depthMinM`, `depthMaxM`), tipologia (`wreck`, `reef`, `cave`, `wall`, `other`), specie marine scientifiche verificate e orientamento di esposizione al moto ondoso (`exposure`).

2. **`*.geojson` (Standard GIS & GitHub Interactive Map)**:
   - Specifiche GeoJSON RFC 7946 (Point FeatureCollection).
   - Consente l'anteprima visuale immediata interattiva direttamente su GitHub (cliccando sul file `.geojson` nel repository si apre la mappa mondiale con tutti i punti cliccabili!).
   - Compatibile con `MapLibre GL`, `Mapbox`, `Leaflet`, `QGIS`.

3. **`index.json` (Catalogo Master)**:
   - Elenco dinamico delle regioni disponibili con bounding box (`bbox`: `[minLon, minLat, maxLon, maxLat]`), conteggio siti e URL diretti per il download over-the-air.

---

## 💨 Integrazione Previsioni Meteo & Sicurezza Immersioni

I dataset includono il campo **`exposure`** (`exposed_north`, `sheltered_north`, `exposed_west`, `exposed_all`, ecc.), progettato specificamente per integrarsi con le previsioni meteo:

- **Esempio Creta & Venti Settentrionali (Meltemi / Tramontana)**:
  - Quando a Creta soffia un forte vento da Nord (Meltemi a 20-30 nodi):
    - I siti della costa nord (`exposed_north`, es. *Elephant Cave* a Drepano o *Messerschmitt Wreck*) presentano mare mosso/agitato e visibilità ridotta, con avviso **"Sconsigliato per mare formato da Nord"**.
    - I siti della costa sud (`sheltered_north`, es. *Shinaria Beach* o *Byron I* a Kaloi Limenes) rimangono a ridosso delle montagne di Creta, con mare calmo e visibilità ottima.
  - L'utente che consulta la mappa di Nautilus riceve un indicatore chiaro (🟢 Condizioni favorevoli / 🟡 Attenzione moto ondoso / 🔴 Sconsigliata immersione) incrociando i dati del vento in tempo reale (OpenWeather / Open-Meteo Marine) con l'orientamento della costa.

---

## 📄 Licenza

I dati storici e geografici sono rilasciati sotto licenza **Creative Commons Attribution 4.0 International (CC BY 4.0)** o pubblico dominio (CC0).
