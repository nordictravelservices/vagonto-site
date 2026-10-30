# vagonto-site

Kildekoden til **vagonto.com** – forside og landingssider for Vagonto Travel AS.

Booking skjer ikke her. Alle salgsknapper lenker videre til bookingmotoren
(Travel Compositor) på **booking.vagonto.com** (live med SSL fra 30. okt 2026,
satt som standarddomene på Airticket Collective-micrositen).

## Struktur

| Fil | Innhold |
|---|---|
| `index.html` | Forsiden («Din reise, satt sammen av deg») |
| `montenegro.html` | Destinasjonsside Montenegro |
| `arsenal.html` | Landingsside Arsenal hjemmekamper (demo – kun Everton-pakken er live) |
| `site.css` | Felles stilark (farger, typografi, header, kort, footer) |
| `img/` | Bilder. `vagonto-logo.png` er logoen |

Rene statiske filer – ingen byggesteg, ingen rammeverk. Hver side er én
HTML-fil som lenker `site.css`; sidespesifikk CSS ligger i en `<style>`-blokk
i den aktuelle siden.

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
