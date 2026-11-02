# vagonto-site

Kildekoden til **vagonto.com** – forside og landingssider for Vagonto AS.

Booking skjer ikke her. Alle salgsknapper lenker videre til bookingmotoren
(Travel Compositor) på **booking.vagonto.com** (live med SSL fra 30. okt 2026,
satt som standarddomene på Airticket Collective-micrositen).

## Struktur

| Fil | Innhold |
|---|---|
| `index.html` | Forsiden («Din reise, satt sammen av deg») – v5 2. nov: Byer du ikke har vært i, Sommer i vinter, Populære nå |
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
| `img/bildebank/` | Egne bilder vi har lov til å bruke (fotograf og bruk står i `img/bildebank/README.md`) |

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

Egen server (GoDaddy VPS «tripilio», cPanel, IP `92.205.161.222`).
Hver push til `main` laster filene opp over SFTP til cPanel-kontoen
`vagonto` (`/home/vagonto/public_html`) via `.github/workflows/deploy.yml`.
Hemmeligheter i repoet: `FTP_SERVER`, `FTP_USERNAME`, `FTP_PASSWORD`.
Ingen byggesteg. SSL kommer fra cPanel AutoSSL (Let's Encrypt).

DNS i Domeneshop: `@` og `www` → A `92.205.161.222`,
`booking` → A `137.116.211.8` (Travel Compositor).
E-post: `info@vagonto.com` er Domeneshop-videresending til Nordic Travel Services.

Flyttet fra Netlify 2. nov 2026 (prosjektet der er slettet).

### Ny nettside på samme server (10 minutter)

1. GoDaddy → serveren → Accounts → **Create**: domene, brukernavn, passord,
   e-post, pakke `default`.
2. GitHub-repo med samme `deploy.yml`; legg inn de tre hemmelighetene
   (server-IP, brukernavnet, passordet) og bytt `remote_path` til
   `/home/<brukernavn>/public_html`.
3. Domeneshop: `@` og `www` → A `92.205.161.222`.
4. Push. AutoSSL henter sertifikat innen en time (eller WHM → Manage AutoSSL
   → Manage Users → «Check» på brukeren).
