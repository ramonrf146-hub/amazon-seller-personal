# Estado actual — Amazon Seller / FBA personal (retail arbitrage)

> Este archivo se actualiza en cada checkpoint importante. No es un log línea por línea.

## Pendiente
- **Decisión de compra final**: quedó en revisión la rentabilidad de 4 productos candidatos (Vitamin C Serum, Eye Cream, Hydra Serum Blueberry, Face Serum Oil/Dermasil Marula) a $1.34/unidad de costo. Falta que el usuario confirme cantidades finales a comprar de cada uno.
- **Cambio de nombre en Seller Central**: pendiente desde hace tiempo — nunca se ejecutó porque el usuario no dio el nombre nuevo deseado. No retomar salvo que lo pida.

## Contexto y decisiones importantes
- Bundles planeados: 60 unidades de Fresh Aloe (bundles de 20) y 60 de Enzema (bundles de 30). Cada **bundle** (no cada unidad individual dentro del bundle) necesita su propia etiqueta FNSKU de Amazon.
- Análisis de rentabilidad hecho con la Revenue Calculator real de Seller Central (operada directamente en el Chrome del usuario, no estimada).
- **Corrección importante ya comunicada al usuario**: "Dermasil Face Serum Oil Marula" parecía el mejor candidato por margen/ROI ($2.99, 223%), pero al revisar el BSR resultó #280.147 (muy malo, ~1-3 unidades/mes) y 0 reviews — se bajó de prioridad al último lugar. Margen alto en el papel no sirve si el producto no vende.
- Regla de oro para evaluar candidatos: nunca confiar en los números de "Tu gestión logística" (FBM) de la calculadora — subestiman el costo de envío real (queda en $0 si no se completa a mano). Siempre comparar con la columna "Logística de Amazon" (FBA).

## Herramienta nueva: `evaluar-fba` (Trazado Engine, Paso 4)
Desde 2026-09-11 existe `node src/cli.mjs evaluar-fba --asin <ASIN> --costo <n>` en `C:\Projects\Trazado_Engine` — consulta Keepa (precio actual, BSR, ventas mensuales estimadas) y estima ganancia/margen/ROI, sin necesitar la sesión de Chrome en vivo. Es una **estimación** (Keepa es un tercero, no Amazon) — para una decisión de compra real, seguir confirmando en la Revenue Calculator de Seller Central antes de comprar. Requiere `KEEPA_API_KEY` en `Trazado_Engine/.env.local` (ya configurada). Ver `Trazado_Engine/ESTADO_ACTUAL.md` para el detalle completo, incluido un bug de conversión de porcentaje ya encontrado y arreglado.

## Convenciones a respetar
- Nunca ejecutar compras, ventas o transferencias — solo análisis y recomendaciones. Las decisiones de compra las toma el usuario.
- Al calcular rentabilidad en Seller Central: el campo "Coste de los productos vendidos" usa coma decimal (`1,34`), no punto — si se escribe con punto, el sitio lo trunca mal.
- El scanning de clearance de Walmart/Target sigue siendo manual (sin API oficial confiable, se descartó hacer scraping) — el usuario manda lo que encuentra y se analiza en el momento, con `evaluar-fba` si hay ASIN o a mano si no.
