# 🌍 Nautilus Global Dive Datasets

Raccolta di dataset geografici open-data con i siti di immersione più celebri al mondo: relitti storici, barriere coralline incontaminate, parchi archeologici sommersi, grotte, cenotes e grandi pelagici per l'applicazione mobile **Nautilus**.

I dataset sono strutturati sia come **catalogo globale unificato** (`global-sites.json`), sia suddivisi in **9 macro-aree geografiche** scaricabili su richiesta direttamente dall'app (es. vacanza a Creta / Mar Egeo, crociera in Mar Rosso, o viaggio alle Galápagos).

---

## 🗺️ Regioni e Copertura Globale

| ID Regione | Nome Area | Copertura Geografica | Siti Chiave | Formati |
|---|---|---|---|---|
| `global` | **Catalogo Globale** | Tutto il mondo | Tutti i 59 siti leggendari mondiali | [JSON](./global-sites.json) · [GeoJSON](./global-sites.geojson) |
| `aegean-sea` | **Mar Egeo & Creta** | Grecia, Creta, Cicladi, Sporadi, Dodecaneso | *Elephant Cave, Shinaria, Messerschmitt Wreck, Olous sommersa, HMHS Britannic, Alonissos Museo Sommerso di Peristera* | [JSON](./aegean-sea.json) · [GeoJSON](./aegean-sea.geojson) |
| `mediterranean` | **Mar Mediterraneo** | Italia, Malta & Gozo, Spagna, Croazia | *Parco Sommerso di Baia, Superpetroliera MT Haven, Cristo degli Abissi, Scoglio del Medico (Ustica), Blue Hole Gozo, Um El Faroud, Isole Medes* | [JSON](./mediterranean.json) · [GeoJSON](./mediterranean.geojson) |
| `red-sea` | **Mar Rosso** | Egitto (Sinai, Hurghada, Marsa Alam) e Sudan | *SS Thistlegorm, Giannis D, Carnatic, Dahab Blue Hole & Canyon, Shark & Yolanda Reef, Elphinstone, Piroscafo Umbria* | [JSON](./red-sea.json) · [GeoJSON](./red-sea.geojson) |
| `caribbean` | **Caraibi & Messico** | Belize, Messico (Yucatán & Cozumel), Cayman, Bahamas, Bonaire | *Great Blue Hole (Belize), Cenote Dos Ojos, Barriera di Palancar, USS Kittiwake, Tiger Beach, Salt Pier* | [JSON](./caribbean.json) · [GeoJSON](./caribbean.geojson) |
| `coral-triangle` | **Triangolo dei Coralli** | Indonesia (Raja Ampat, Komodo, Bali), Filippine, Malesia, Thailandia | *Cape Kri (record biodiversità), Batu Bolong, USAT Liberty a Tulamben, Tubbataha Reefs, Sipadan Barracuda Point, Richelieu Rock* | [JSON](./coral-triangle.json) · [GeoJSON](./coral-triangle.geojson) |
| `pacific-oceania` | **Pacifico & Oceania** | Australia (Great Barrier Reef), Palau, Micronesia (Chuuk Lagoon), Hawaii | *SS Yongala, Cod Hole, Blue Corner (Palau), Flotta WWII Fujikawa Maru (Truk), Mante notturne di Kona* | [JSON](./pacific-oceania.json) · [GeoJSON](./pacific-oceania.geojson) |
| `indian-ocean` | **Oceano Indiano** | Maldive, Sudafrica (Sardine Run & Aliwal Shoal) | *Maaya Thila, Hanifaru Bay (cicloni di mante), Aliwal Shoal (squali toro e tigre)* | [JSON](./indian-ocean.json) · [GeoJSON](./indian-ocean.geojson) |
| `pelagic-eastern-pacific` | **Pacifico Orientale Pelagico** | Galápagos (Ecuador), Isola del Cocco (Costa Rica), Socorro (Messico) | *Darwin's Pillars (squali balena da 14m), Bajo Alcyone (muri di squali martello), The Boiler (mante giganti e delfini)* | [JSON](./pelagic-eastern-pacific.json) · [GeoJSON](./pelagic-eastern-pacific.geojson) |
| `north-atlantic` | **Atlantico Settentrionale** | Islanda (Thingvellir), Scozia (Scapa Flow) | *Faglia di Silfra (tra placche tettoniche con 100m di visibilità), Corazzata SMS Kronprinz Wilhelm* | [JSON](./north-atlantic.json) · [GeoJSON](./north-atlantic.geojson) |

---

## 📊 Standard Dati & Mappe Interattive

Ciascun file è distribuito in due formati sincronizzati:

1. **`*.json` (Nautilus Native Schema)**:
   - Perfettamente compatibile con l'interfaccia TypeScript `CatalogSite` di Nautilus (`src/data/sitesCatalog.ts`).
   - Include coordinate verificate, profondità indicative min/max, livello di brevetto richiesto, elenco specie marine scientifiche, highlights e orientamento della costa (**`exposure`**).

2. **`*.geojson` (GeoJSON RFC 7946 per Mappe GIS)**:
   - Visualizzabile nativamente come mappa interattiva sul repository GitHub.
   - Compatibile con `MapLibre GL`, `Leaflet`, `Mapbox`, `QGIS`.

3. **`index.json` (Catalogo Master Dinamico)**:
   - Fornisce all'app Nautilus l'elenco delle regioni disponibili, bounding box per il posizionamento della mappa, conteggio siti e URL diretti di download.

---

## 🌦️ Sicurezza Meteo-Marina (Vento, Onde & Esposizione)

Ogni sito include il metadato **`exposure`**:
- `exposed_north` / `exposed_south` / `exposed_west` / `exposed_east`
- `sheltered_north` / `sheltered_south` / `sheltered_all`
- `exposed_all`

L'app incrocia questo parametro in tempo reale con i bollettini meteo di **Open-Meteo Marine / OpenWeather**:
- In caso di vento forte (es. **Maestrale o Meltemi da Nord** a 20-30 nodi):
  - I siti esposti a Nord (es. *Elephant Cave* a Creta o *Messerschmitt Wreck*) vengono contrassegnati con un badge di avviso **🔴 Sconsigliata immersione** (forte moto ondoso e risacca).
  - L'app propone i siti ridossati a Sud (es. *Shinaria Beach* o *Byron I* a Kaloi Limenes), dove il mare resta calmo e l'acqua limpida.
