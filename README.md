# Hidalgo Tours · Creativos por país (Conversiones LATAM)

Reporte interactivo que muestra qué creativo funcionó mejor en cada país en la campaña
**HC_HT_CONV_LATAM | MAY_2026** de la cuenta **HIDALGO TOURS BM** (Meta Ads).

Período: 5 de mayo al 24 de noviembre de 2026. Moneda: bolivianos (BOB).

## Qué incluye

- KPIs de la campaña: gasto, conversaciones, CPL, alcance, frecuencia e impresiones.
- **Top 3 creativos por país** con CPL, conversaciones, gasto, alcance, frecuencia y formato.
- Gráfico de CPL por creativo, coloreado por formato (video, estático o carrusel).
- Resumen por país y una tabla con el detalle de todos los creativos, que se puede ordenar.
- Filtros por país y formato, criterio para ordenar el ranking (CPL, conversaciones o alcance)
  y gasto mínimo para entrar al ranking.

## Archivos

| Archivo | Qué es |
|---|---|
| `index.html` | La página del reporte (HTML, CSS y JS en un solo archivo, sin dependencias externas). |
| `data.js` | Los datos que usa el reporte (`window.REPORT_DATA`). |

## Publicarlo con GitHub Pages

1. Sube `index.html`, `data.js` y este `README.md` a la raíz del repositorio (o a una carpeta `docs/`).
2. En GitHub, ve a **Settings → Pages**.
3. En **Source** elige la rama (por ejemplo `main`) y la carpeta (`/root` o `/docs`). Guarda.
4. En uno o dos minutos el reporte queda en `https://<usuario>.github.io/<repositorio>/`.

También se puede abrir directamente con doble clic en `index.html`; funciona sin servidor.

## Actualizar los datos

Solo hay que reemplazar `data.js`. Su estructura es:

```js
window.REPORT_DATA = {
  meta: { campaign, campaign_id, account, account_id, currency,
          period_start, period_end, generated, result_type,
          total: { spend, conversations, impressions, reach, link_clicks } },
  countries: [ { code, spend, conversations, impressions, reach, link_clicks } ],
  creatives: [ { country, creative, format, spend, conversations, impressions,
                 reach, link_clicks, ads, active, ad_names } ]
};
```

- `countries` usa el alcance real por país (sin duplicar), sacado de la campaña con desglose por país.
- `creatives` tiene una fila por país + creativo + formato. Los anuncios duplicados de la misma pieza
  (en varios conjuntos o como "- Copia") se suman en una sola fila.
- `format` puede ser `Video`, `Estático` o `Carrusel`.

## Notas de método

- **Conversaciones** = conversaciones de mensajes iniciadas (7 días clic / 1 día vista).
- **CPL** = gasto ÷ conversaciones.
- **Alcance y frecuencia por creativo** se suman entre los anuncios de la misma pieza, así que
  pueden contar dos veces a una persona que vio dos copias. Sirven para comparar creativos;
  el alcance exacto está a nivel país.
- Los resultados con menos de 20 conversaciones se marcan como "volumen bajo".
