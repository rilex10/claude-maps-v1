# Mapas CDN — recursos para videos de mapas animados

Repositorio público pensado para servirse por **jsDelivr**:
`https://cdn.jsdelivr.net/gh/rilex10/claude-maps-v1@main/<ruta>`

Claude (o cualquier página) solo necesita leer `catalogo_recursos.json` (~12 KB) y luego carga cada archivo por URL desde el navegador (CORS abierto).

## Estructura
| Carpeta | Contenido |
|---|---|
| `paises/{ISO3}.geojson` | Un país por archivo, Natural Earth 1:50m (ej. `MEX`, `ESP`, `ARG`) |
| `paises_hd/{ISO3}.geojson` | Igual, desde 1:10m simplificado (más detalle de costa) |
| `provincias/{ISO3}.geojson` | Estados/provincias (admin-1) de cada país |
| `mundo/paises_50m.geojson` | Todos los países en un archivo (~1.9 MB) |
| `historicos/` | Polígonos aproximados de episodios (Capitanía de Guatemala, La Mesilla, litoral boliviano, cráter Chicxulub…) |
| `estilos/{estilo}.style.json` + `estilos/raster/{estilo}/{z}/{x}/{y}.jpg` | Mapas base raster 512 px, zoom 0–4: natural, satelite, antiguo, antiguo_relieve, relieve, noche, oscuro, plano, tiempo_profundo |
| `estilos/ejemplos/` | Vistas previas JPG de cada estilo |
| `estilos/config_motor_v4/` | Configuraciones de estilo del motor v4 (Mapas 2) |
| `sprites/emoji/` | Iconos Twemoji (svg/png) por código Unicode |
| `sprites/banderas/{iso2}.png` | Banderas |
| `sfx/`, `musica/` | Efectos de dominio público/CC0 y música CC BY 3.0 |

## Antes de publicar
1. Crea el repo público en GitHub y sube esto.
2. Reemplaza `rilex10`/`claude-maps-v1` en `estilos/*.style.json` (o hazlo en el código al cargar: `fetch(url).then(r=>r.text()).then(t=>JSON.parse(t.replaceAll('rilex10',u).replaceAll('claude-maps-v1',r)))`).
3. Sube `catalogo_recursos.json` al Project Knowledge de Claude.
4. Para caché estable, publica un tag (`v1.0`) y usa `@v1.0` en lugar de `@main`. jsDelivr limita a 20 MB por archivo; aquí todos son menores.

## Uso rápido
```js
const BASE='https://cdn.jsdelivr.net/gh/USUARIO/REPO@main/';
const mx = await fetch(BASE+'paises/MEX.geojson').then(r=>r.json());
```
Ver más ejemplos (MapLibre, D3, Leaflet, Canvas) en `catalogo_recursos.json` → `uso`.

## Licencias
Ver `LICENCIAS.md`. Créditos requeridos: Twemoji (CC BY 4.0), Kevin MacLeod (CC BY 3.0).
