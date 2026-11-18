# brightbean-build

Bouwt het Docker-image van [BrightBean Studio](https://github.com/brightbeanxyz/brightbean-studio)
op GitHub Actions en zet het op `ghcr.io/ruben-wadup/brightbean-studio`. De broncode wordt
niet aangepast (AGPL-3.0, zie de upstream-repo). Zo hoeft de Coolify-server niet zelf te bouwen.

Bijwerken: zet een nieuwe commit-SHA van upstream in `BRIGHTBEAN_REF` en push. De workflow bouwt
dan `:<korte-sha>` en `:latest`. Daarna in Coolify de tag in de service aanpassen en opnieuw deployen.
