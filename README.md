# Confiabilidad – Equipos Envase

Tablero web para analizar la confiabilidad de los equipos de envase con el indicador **52-12-4**
(meta < 0,5 %) a partir de los archivos Excel *MED* de cada línea: **L5, L7, LE7, L8 y L9**.

## Qué hace

- Lee solo las hojas **BD PARADAS** y **BD TIEMPOS** de cada archivo.
- Calcula el 52-12-4 de cada equipo: horas de falla (causas internas) del equipo ÷ (EPT + horas de causas internas de la línea) en 52, 12 y 4 semanas.
  El resultado coincide con la hoja "52-12-4" del Excel.
- Vistas:
  - **Resumen**: indicadores clave, hallazgos automáticos, equipos con más tiempo perdido y mapa de confiabilidad 52W contra 12W.
  - **Equipos 52-12-4**: tabla ordenable con estado ATO (Cumple, Mejorando, Alerta, Crítico), tendencia y semana estimada de retorno a la meta. Se puede exportar a CSV.
  - **Detalle de equipo**: tendencia móvil, horas por semana, proyección de "¿en qué semana vuelve a 12W ≤ 0,5 %?", subconjuntos, causas raíz, microparadas y bitácora de fallas.
  - **Tiempos de línea**: LEF, OEE, GLY y OAE semanales, distribución de las 168 h, producción en hL, LEF por turno y cambios de formato.
  - **Paradas**: tipos de parada, causas raíz, mapa de calor equipo × semana, hora y día de las fallas, y microparadas.
  - **Comparar líneas**: comparativo de las líneas cargadas.

## Privacidad

Los archivos se procesan **dentro del navegador**. No se envían a ningún servidor.
Los datos quedan guardados en ese navegador (IndexedDB) hasta que uses "Borrar datos guardados".
Este repositorio solo contiene la página, no los datos.

## Cómo usarlo cada semana

1. Abre el link del tablero.
2. Ve a **Cargar archivos** y arrastra los Excel (por ejemplo `18.10_L7_MED_1.xlsx`). La línea se detecta por el nombre del archivo; también puedes usar el botón de cada línea.
3. Para actualizar, vuelve a subir el archivo de la línea: reemplaza al anterior.

## Publicar gratis

### GitHub Pages
1. En el repositorio: **Settings → Pages**.
2. En *Build and deployment*: Source **Deploy from a branch**, Branch **main**, carpeta **/ (root)** → **Save**.
3. En 1 o 2 minutos queda en `https://carlosriost.github.io/confiabilidad-equipos-envase/`.

### Cloudflare Pages (alternativa)
1. dash.cloudflare.com → **Workers & Pages → Create → Pages → Connect to Git**.
2. Elige este repositorio. *Framework preset*: None. *Build command*: vacío. *Output directory*: `/`.
3. Guarda y despliega. Te da un link `*.pages.dev`.

## Ajustes

Al inicio del script en `index.html`:

```js
const LINEAS = ['L5','L7','LE7','L8','L9']; // líneas disponibles
const META = 0.005;                          // meta 52-12-4 (0,5 %)
```

La librería de gráficos (ECharts 5.5.1, licencia Apache 2.0) va incluida en `vendor/`, así que el tablero no depende de CDNs externos. Publica siempre la carpeta `vendor` junto a `index.html`.

Requiere un navegador actualizado (Chrome, Edge, Firefox o Safari recientes).
