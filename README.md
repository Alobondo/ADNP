# Sitio Autóctonos de Ninguna Parte

Blog en [Quarto](https://quarto.org) + R que reproduce, sección por sección,
el *Book de Prensa 2026* de Autóctonos de Ninguna Parte. Cada sección del
book (Banda, Biografía, Discografía, Videos, Prensa, Eventos, Contacto) es
un post en `posts/`, generado con código R (tablas `knitr::kable`, tarjetas
armadas dinámicamente y gráficos `ggplot2`).

## Estructura

```
sitio-web/
├── _quarto.yml        # configuración del sitio (navbar, footer, tema)
├── _variables.yml      # datos de contacto y enlaces reutilizados con {{< var >}}
├── styles.scss         # paleta de colores y tipografías del sitio
├── index.qmd            # portada con listado de secciones
├── images/               # logos y fotos usadas en el sitio
└── posts/
    ├── 01-biografia/
    ├── 02-banda/
    ├── 03-discografia/
    ├── 04-videos/
    ├── 05-prensa/
    ├── 06-eventos/
    └── 07-contacto/
```

## Paleta y tipografías

Definidas en `styles.scss`:

| Color | Uso |
|---|---|
| `#726EFF` | color primario (enlaces, hero, títulos H2) |
| `#21272A` | fondo oscuro (navbar, footer, tarjetas, texto) |
| `#CDFE03` | acento lima (etiquetas, subrayados, hitos) |
| `#FFFFFF` | fondo claro |

Tipografías (Google Fonts): **Permanent Marker** para titulares (estilo
marcador, igual al lettering del book de prensa) y **Space Grotesk** para el
cuerpo de texto.

## Antes de publicar

1. Edita `_variables.yml` y reemplaza los valores marcados con `TODO`:
   - IDs de YouTube de cada video (`posts/04-videos`).
   - URLs reales de Spotify y YouTube (`posts/07-contacto`).
2. Edita `_quarto.yml` y reemplaza `site-url` y `repo-url` por la URL real
   del sitio publicado y del repositorio.
3. Revisa las notas de prensa en `posts/05-prensa/index.qmd`: agrega la URL
   de cada nota cuando la tengas para convertir los titulares en enlaces.

## Requisitos

- [R](https://www.r-project.org/) (≥ 4.3)
- [Quarto CLI](https://quarto.org/docs/get-started/)
- Paquetes de R: `knitr`, `rmarkdown`, `ggplot2`, `dplyr`, `tibble`, `glue`,
  `yaml`

```r
install.packages(c("knitr", "rmarkdown", "ggplot2", "dplyr", "tibble", "glue", "yaml"))
```

## Renderizar y previsualizar en local

Desde la carpeta `sitio-web/`:

```bash
quarto preview
```

Esto levanta un servidor local con recarga automática. Para generar el sitio
estático final (carpeta `_site/`):

```bash
quarto render
```

## Publicar en Git / GitHub Pages

1. Inicializa el repositorio dentro de `sitio-web/` (esta carpeta debe ser
   la raíz del repositorio):

   ```bash
   git init
   git add .
   git commit -m "Sitio inicial Autóctonos de Ninguna Parte"
   git branch -M main
   git remote add origin <URL-de-tu-repositorio>
   git push -u origin main
   ```

2. **Publicación automática (recomendada):** el workflow
   `.github/workflows/publish.yml` ya incluido renderiza el sitio con R +
   Quarto y lo publica en la rama `gh-pages` cada vez que se hace push a
   `main`. Solo debes habilitar GitHub Pages en el repositorio (Settings →
   Pages → Source: rama `gh-pages`).

3. **Publicación manual alternativa** (sin GitHub Actions), usando la CLI de
   Quarto:

   ```bash
   quarto publish gh-pages
   ```

## Notas

- El proyecto usa `freeze: auto` (`_quarto.yml`), por lo que los resultados
  de los chunks de R se cachean entre renders; borra la carpeta `_freeze/`
  si necesitas forzar una recomputación completa.
- Las imágenes en `images/` fueron tomadas del book de prensa original
  (`Dossier/Book de Prensa ADNP 2026.pdf`) y de las carpetas `Fotos/`,
  `Logos/` y `Portada/` del proyecto.
