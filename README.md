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
| `0001-instagram-story.patch` | Keuze "Publish as: Feed post / Reel / Story" bij Instagram in de composer; geen caption en geen eerste reactie bij een story. Aangeboden aan upstream als [PR #243](https://github.com/brightbeanxyz/brightbean-studio/pull/243). |

Een image met patches krijgt de tag `<korte-sha>-wadup.<hash>`; de hash volgt de inhoud van de patches.
Zonder patches is de tag `<korte-sha>`.

## Upstream-check (elke maandag)

De workflow `upstream-check.yml` zet de patches elke maandag op de nieuwste `main` van upstream en
draait daar de volledige testsuite op. Hij bouwt en deployt niets. Faalt hij, dan mailt GitHub:

- **Patch past niet meer:** upstream heeft dezelfde bestanden veranderd. Werk de patch bij op de
  nieuwe versie vóór je `BRIGHTBEAN_REF` verhoogt.
- **Patch zit al in upstream:** bijvoorbeeld omdat onze PR is gemerged. Haal de patch uit `patches/`
  en verhoog `BRIGHTBEAN_REF`.
- **Tests falen:** de patch past wel, maar werkt niet meer goed samen met de nieuwe code.

In de samenvatting van een run zie je ook hoeveel commits upstream verder is dan wat wij draaien.
GitHub zet geplande workflows uit na 60 dagen zonder commits in deze repo; je krijgt daar vooraf een
mail over en kunt hem onder Actions weer aanzetten.

## Bijwerken

Zet een nieuwe commit-SHA van upstream in `BRIGHTBEAN_REF` en push. De workflow bouwt dan de nieuwe
tag en `:latest`. Faalt het toepassen van een patch, dan moet die patch eerst op de nieuwe versie
worden bijgewerkt. Daarna in Coolify de tag in de service aanpassen en opnieuw deployen.
