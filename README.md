# brightbean-build

Bouwt het Docker-image van [BrightBean Studio](https://github.com/brightbeanxyz/brightbean-studio)
op GitHub Actions en zet het op `ghcr.io/ruben-wadup/brightbean-studio`. Zo hoeft de Coolify-server
niet zelf te bouwen.

## Eigen aanpassingen (AGPL-3.0)

BrightBean Studio valt onder de AGPL-3.0. Onze aanpassingen staan als patch in [`patches/`](patches/)
en worden bij elke build op de upstream-code toegepast. Hiermee is de broncode van de versie die wij
draaien openbaar: upstream op de commit uit `BRIGHTBEAN_REF`, plus deze patches.

| Patch | Wat het doet |
|---|---|
| `0001-instagram-story.patch` | Keuze "Publish as: Feed post / Reel / Story" bij Instagram in de composer; geen caption en geen eerste reactie bij een story. |

Een image met patches krijgt de tag `<korte-sha>-wadup.<hash>`; de hash volgt de inhoud van de patches.
Zonder patches is de tag `<korte-sha>`.

## Bijwerken

Zet een nieuwe commit-SHA van upstream in `BRIGHTBEAN_REF` en push. De workflow bouwt dan de nieuwe
tag en `:latest`. Faalt het toepassen van een patch, dan moet die patch eerst op de nieuwe versie
worden bijgewerkt. Daarna in Coolify de tag in de service aanpassen en opnieuw deployen.
