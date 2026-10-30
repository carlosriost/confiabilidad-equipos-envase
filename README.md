# Confiabilidad – Equipos Envase

Tablero web para analizar la confiabilidad de los equipos de envase con el indicador **52-12-4**
(meta < 0,5 %) a partir del **reporte BD** que se descarga con todas las líneas juntas
(por ejemplo `Reporte_BD_2026-10-27_11.20.44.xlsx`).

## Qué lee

- Solo las hojas **BD PARADAS** y **BD TIEMPOS** del reporte. BD PRODUCCION y BD CONSOLIDADO se ignoran.
- Separa las líneas por la columna **LÍNEA**: `TREN-5` → L5, `TREN-7` → L7, `TREN-8` → L8, `TREN-9` → L9.
  Las líneas no están fijas: aparecen solas según lo que traiga el reporte.
- Se pueden subir varios reportes. Se acumulan, y si dos reportes cubren las mismas fechas de una línea,
  se usan los datos del más reciente. Así, subiendo el reporte cada semana, se va completando la historia de 52 y 12 semanas.

## Indicador 52-12-4

52-12-4 de un equipo = horas de falla (causas internas) del equipo ÷ (EPT + horas de causas internas de su línea),
en las últimas 52, 12 y 4 semanas hasta la semana de corte. Es el mismo cálculo de la hoja "52-12-4" del Excel anterior.

## Vistas

- **Resumen**: indicadores clave, hallazgos automáticos, ranking de equipos y mapa 52W contra 12W.
- **Preguntar**: asistente propio para hacer preguntas en español (ver abajo).
- **Equipos de la línea**: todas las máquinas de cada línea agrupadas por tipo, con código SAP, fallas, 52-12-4, estado y última falla. El reporte solo nombra un equipo cuando falla; los que nunca han fallado se agregan a mano o pegando una lista desde Excel/SAP (se guardan en el navegador) y cuentan con 0 %.
- **Equipos 52-12-4**: tabla con estado ATO (Cumple, Mejorando, Alerta, Crítico), tendencia y semana de retorno a la meta. Exporta CSV.
- **Detalle de equipo**: tendencia, horas por semana, proyección de retorno a la meta, subconjuntos, causas raíz, microparadas y bitácora.
- **Tiempos de línea**: LEF, OEE, GLY, OAE, distribución de las 168 h, producción, LEF por turno y cambios de formato.
- **Paradas**: tipos de parada, causas raíz, mapa de calor equipo × semana, hora y día de las fallas, microparadas.
- **Comparar líneas** y **Cargar reportes**.

## Asistente "Preguntar"

Funciona 100 % dentro de la página: no usa internet, ni APIs, ni servicios de pago.
Interpreta la pregunta (líneas, equipos aunque se escriban incompletos, fechas, turnos, tipo de parada,
agrupación y medida), calcula sobre los datos cargados y responde con texto, tabla y gráfico.
Siempre muestra cómo entendió la pregunta (línea, periodo, filtros), para que se pueda verificar.

Ejemplos:

- ¿Cómo va la L5?
- ¿Qué equipo de la L8 tuvo más horas de falla la semana pasada?
- 52-12-4 de la lavadora de botellas de la L8
- ¿Por qué falla la etiquetadora de la L9? · y por subconjunto?
- ¿Cuándo vuelve a la meta la estiradora si pierde 15 min por semana?
- Compara el LEF de todas las líneas por semana
- Últimas fallas de más de 10 min en la L9 · ¿Qué pasó ayer en la L8?
- Equipos con más de 2 horas de falla en la L9 · causas raíz sin la L9
- ¿A qué hora fallan más los equipos de la L5? · ¿Qué turno tiene peor LEF?
- MTBF y MTTR de los equipos de la L8 · ¿Cuánto tiempo se perdió por limpieza en la L5?

Escribe **ayuda** dentro del asistente para ver más ejemplos.

## Privacidad

Los archivos se procesan **dentro del navegador**. No se envían a ningún servidor.
Los datos quedan guardados en ese navegador (IndexedDB) hasta que uses "Borrar datos guardados".
Este repositorio solo contiene la página, no los datos.

## Publicar

### GitHub Pages
**Settings → Pages** → Source **Deploy from a branch** → Branch **main** / **(root)** → **Save**.
Queda en `https://carlosriost.github.io/confiabilidad-equipos-envase/`.

### Cloudflare
Si el proyecto de Cloudflare está conectado a este repositorio, se publica solo con cada cambio.
Publica siempre la carpeta `vendor/` junto a `index.html`.

La librería de gráficos (ECharts 5.5.1, licencia Apache 2.0) va incluida en `vendor/`, así que el tablero
no depende de CDNs externos. Requiere un navegador actualizado (Chrome, Edge, Firefox o Safari recientes).
