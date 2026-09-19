# Datos abiertos de Maps by AFI (Arda)

Archivos de datos que la app **Maps by AFI** descarga sola —una vez al mes, sólo con wifi— para renovar lo que
trae de fábrica. Cada archivo va **firmado** (Ed25519): la app comprueba `<archivo>.sig` con la llave pública
que lleva dentro antes de leer un solo byte, y sólo sustituye lo suyo si es más nuevo y viene de la casa.

| Archivo | Qué es | Fuente |
|---|---|---|
| `zonas-mx.json` | Municipios con alerta de México: el 10 % de municipios de 20 000 habitantes o más con más homicidios dolosos, secuestros, extorsiones y robos con violencia por cada 100 000 habitantes, con sus polígonos | SESNSP (denuncias, ene–dic 2025) · INEGI (población y marco geoestadístico) |
| `zonas-cdmx.json` | Colonias con alerta de la Ciudad de México, mismo criterio a escala de colonia | FGJ CDMX (carpetas de investigación con punto, 2024) · IECM (colonias y población, 2022) |
| `casetas-mx.json` | Las plazas de cobro de México **por sentido de circulación** (1 007 el 2026-09-18) con su punto, el rumbo de la carretera y las tarifas para auto, moto y camión de 2 ejes: el mínimo visto (`costos`) y, en tramos de cuota cerrada, el máximo (`costosHasta`); las que no tienen tarifa confirmada van en `sinTarifa`. Se regenera cada semana | OpenStreetMap (`barrier=toll_booth`, ODbL) · INEGI, Sakbé v3.1 sobre la Red Nacional de Caminos 2025 (tarifas) |
| `*.sig` | La firma Ed25519 de cada archivo, en base64 | — |

Los datos son **derivados de fuentes públicas** y dicen lo que dicen las denuncias: una zona sin alerta no es
una zona segura, y una con alerta no es una condena. La app lo dice así en pantalla.

Cómo se generan y se firman: `scripts/zonas-mx.py`, `scripts/zonas-cdmx.py`, `scripts/casetas-mx.py` y
`scripts/firmar-zonas.py` en el repositorio de la app (el catálogo de casetas, cada lunes por el Action `datos-semanal`). La llave privada que firma no está en ningún repositorio.

## Licencia

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.es). Los datos fuente conservan las licencias de
sus autores (SESNSP, INEGI, FGJ CDMX, IECM: datos abiertos del gobierno de México; las plazas de cobro vienen de
OpenStreetMap, © colaboradores de OpenStreetMap, ODbL).
