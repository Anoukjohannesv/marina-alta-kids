# Marina Alta Kids — Projectlog

> Overzicht van beslissingen, status en gedane werk. Zo hoef je niet steeds terug te zoeken.

## Wat is dit?
Interactieve kaart met kinderactiviteiten aan de **Costa Blanca & Valencia** (Benidorm → Valencia).
Eén bestand: `index.html`. Drietalig (EN/NL/DE), Leaflet-kaart + OpenStreetMap, routeplanner die
naar Google Maps linkt.

## Doel
**Onderdeel van een betaald product** (gids/cursus/reispakket). Focus dus op: toegang afschermen,
premium-gevoel en betrouwbare data.

## Belangrijke beslissingen
- **Hosting:** blijft op **Netlify**. Niet naar GoHighLevel verplaatsen — wél in GHL tonen via
  een iframe naar de Netlify-URL (dan kun je er e-mail-capture/CTA omheen bouwen).
  - Let op: knop "Gebruik mijn locatie" werkt in een iframe alleen met `allow="geolocation"` + HTTPS.
- **Afschermen betaald product:** een los HTML-bestand is niet écht te beveiligen (view-source).
  Aanpak: kaart achter GHL-membership/login zetten, Netlify-URL onvoorspelbaar maken + `noindex`.
  De waarde zit in de curatie, niet in de code.
- **Geen extra afhankelijkheden.** Bewuste keuze: de kaart moet zelfstandig werken.
  - Visuele kaart = OpenStreetMap (gratis, geen Google API-key/creditcard nodig).
  - Navigeren = overgedragen aan de échte Google Maps via links (turn-by-turn in de app).
  - Marker-clustering-plugin bewust **niet** toegevoegd. Pins overlappen alleen uitgezoomd;
    inzoomen lost het op, en via lijst/zoekbalk is alles altijd te kiezen.
- **Werkvolgorde:** eerst layout + functionaliteit goed, dán pas alle activiteiten toevoegen.

## Gedaan (sessie 2026-07-08)
- 🔴 **Bug gefixt:** je kon maar 1 route-stop toevoegen; vanaf stop 2 crashte de planner
  (`#rp-empty` was uit de DOM verwijderd). Multi-stop route werkt nu (getest met 3 stops,
  correcte Google Maps-link met origin + bestemming + waypoints).
- 📱 **Mobiel scrollen gefixt:** `overflow:hidden` losgelaten op mobiel; kaart bovenaan met
  vaste hoogte, rest scrollt eronder.
- 🔍 **Zoekfunctie toegevoegd:** zoekt op naam + plaats, in alle 3 talen, met wisknop en
  "geen resultaten"-melding.
- ✅ Google Maps-routing bevestigd werkend.

## Nog te doen
- [ ] **Bedrijfsnaam** kiezen (staat nu generiek bovenaan) → daarna logo + favicon zetten
- [ ] **Data verifiëren:** coördinaten, openingstijden, werkende links per activiteit
- [ ] **Premium content:** per plek beste bezoektijd, parkeren, persoonlijke tip, prijs
- [ ] **Social-share preview** (OG-tags + deelplaatje) — heeft naam/logo nodig
- [ ] **GHL-toegang inrichten** (membership + iframe embed + noindex)
- [ ] Evt. analytics (bijv. Plausible)

## Technische notities
- Alles zit in `index.html` (HTML + CSS + JS + data).
- Activiteiten staan in de `locations`-array; vertalingen in het `t`-object (en/nl/de).
- Taalkeuze wordt onthouden in localStorage (`mak-lang`), standaardtaal = EN.
- Testen kan met Playwright (zie eerdere sessie) of gewoon `index.html` openen in de browser.
