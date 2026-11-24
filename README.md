# Hidalgo Tours · Performance de creativos por país

Reporte interactivo de la campaña **HC_HT_CONV_LATAM | MAY_2026** (cuenta **HIDALGO TOURS BM**, Meta Ads).
Muestra qué creativo funcionó mejor en cada país, mes a mes. Moneda: bolivianos (BOB).

## Qué incluye

- **Selector de período:** cada mes calendario por separado, o el acumulado desde el inicio de la campaña.
- **Indicadores:** gasto, conversaciones, CPL, alcance, frecuencia e impresiones, con la variación contra el mes anterior.
- **Top 3 creativos por país**, con CPL, conversaciones, gasto, alcance, frecuencia y formato (video, estático o carrusel).
- **Gráfico de CPL por creativo**, resumen por país y una tabla con todos los creativos que se puede ordenar.
- **Filtros** por país y formato, criterio para ordenar el ranking y un gasto mínimo para entrar.

Se puede compartir un mes concreto agregando `#AAAA-MM` al link, por ejemplo `.../#2026-10`.

## Estructura

```
index.html          La página del reporte (sin dependencias externas)
data/meses.js       Índice de períodos: qué meses hay y cuál se abre por defecto
data/AAAA-MM.js     Un archivo por mes calendario (ej. data/2026-11.js)
data/acumulado.js   Total desde el inicio de la campaña
```

## Actualización mensual

Cada mes:

1. Se genera `data/AAAA-MM.js` con los datos del mes desde Meta Ads.
2. Si el mes anterior estaba en curso, se regenera con el mes ya cerrado.
3. Se actualiza `data/acumulado.js`.
4. En `data/meses.js` se agrega el mes nuevo al inicio de `periods` y se cambia `default`.

GitHub Pages publica el cambio solo, en uno o dos minutos. El link no cambia.

### Formato de cada archivo de período

```js
(window.REPORT_PERIODS = window.REPORT_PERIODS || {})["2026-11"] = {
  key, label, period_start, period_end, partial,
  total:     { spend, conversations, impressions, reach, link_clicks },
  countries: [ { code, spend, conversations, impressions, reach, link_clicks } ],
  creatives: [ { country, creative, format, spend, conversations, impressions,
                 reach, link_clicks, ads, active, ad_names } ]
};
```

## Notas de método

- **Conversaciones:** conversaciones de mensajes iniciadas (7 días clic / 1 día vista), que es el resultado que optimiza la campaña.
- **CPL:** gasto ÷ conversaciones.
- **Creativo:** agrupa los anuncios con la misma pieza aunque estén duplicados en varios conjuntos o como "- Copia". Si una pieza existe en dos formatos, se separa por formato.
- **Formato:** *Video* si el anuncio registró reproducciones, *Carrusel* si tiene varias tarjetas, *Estático* si es una imagen única.
- **Alcance:** el alcance por país es el real de Meta, sin duplicar. El alcance por creativo es una suma entre anuncios y puede contar dos veces a la misma persona.
- Los resultados con menos de 20 conversaciones se marcan como "volumen bajo".
- Un mes en curso se marca como tal. Su gasto y sus conversaciones van a subir hasta que el mes cierre.
