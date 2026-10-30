# vagonto-site

Kildekoden til **vagonto.com** – forside og landingssider for Vagonto AS.

Booking skjer ikke her. Alle salgsknapper lenker videre til bookingmotoren
(Travel Compositor) på **booking.vagonto.com** (live med SSL fra 30. okt 2026,
satt som standarddomene på Airticket Collective-micrositen).

## Struktur

| Fil | Innhold |
|---|---|
| `index.html` | Forsiden fra oktober («Din reise, satt sammen av deg») |
| `reiseforslag.html` | Første forside fra september (reiseskapere og reisekort) |
| `akkurat-na.html` | «Akkurat nå» – samleside i menyen for sesongens steder og kampanjer |
| `smabyer.html` | Småbyer (under Akkurat nå, ikke i menyen) |
| `montenegro.html` | Montenegro (kampanjeside under Akkurat nå, ikke i menyen) |
| `pakk-reisen-selv.html` | Slik pakker du reisen selv |
| `bli-reiseskaper.html` | Rekruttering av reiseskapere |
| `maria-solheim.html` | Eksempel på profilside for en reiseskaper |
| `om-oss.html` | Om Vagonto, navnet, trygghet, kontakt |
| `reisehjelp.html` | KI-chat (virker ikke uten KI-tjeneste bak) – ikke i menyen |
| `arsenal.html` | Arsenal hjemmekamper (demo) – ikke i menyen |
| `sider.html` | Arbeidsoversikt over alle sidene – ikke i menyen |
| `site.css` | Stilark for forside og Montenegro |
| `chrome.css` | Felles meny og bunnlinje for alle sider (klasser med `vg-`) |
| `favicon.svg`, `favicon-32.png`, `apple-touch-icon.png` | Rutemerket, samme som på booking.vagonto.com |
| `img/` | Bilder. `vagonto-logo.png` er logoen |

Rene statiske filer – ingen byggesteg, ingen rammeverk. De eldre sidene har
sin egen CSS inline; den gamle toppen og bunnen deres er skjult (beholdt
fordi sidenes skript bruker elementene) og erstattet med felles meny og
bunnlinje fra `chrome.css`.

## Lenker til bookingmotoren

Dette fungerer i dag som direkte lenker fra landingssidene:

- Søkemotor forvalgt: `/no/?tripType=ONLY_HOTEL` (også `ONLY_FLIGHT`,
  `FLIGHT_HOTEL`, `ONLY_TICKET`, `ONLY_TRANSFER`), `/no/tripplanner`,
  `/no/transport-accommodation`
- Destinasjonsside: `/no/destination/<KODE>?tripType=FLIGHT_HOTEL`
  (koder i prosjektdokumentet `vagonto-tc-destinasjonskoder.md`)
- Reiseforslag: `/no/idea/<id>/<slug>`
- Egne landingssider i TC: `/no/landing/<id>/<slug>`

Forhåndsutfylte søk (destinasjon + datoer + antall i URL) er ikke mulig ennå –
avklares med TC-support.

## Deploy

Netlify, koblet direkte til dette repoet. Hver push til `main` publiseres
automatisk. Ingen server, ingen byggesteg (publish directory = repo-roten).
DNS ligger i Domeneshop: `@` → A `75.2.60.5`, `www` → CNAME til
Netlify-sitens `*.netlify.app`-adresse. SSL lages automatisk av Netlify.
