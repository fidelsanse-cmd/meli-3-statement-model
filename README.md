# Modelo Financiero de 3 Estados — MercadoLibre (MELI)

Modelo de tres estados contables integrados (Estado de Resultados, Balance y Flujo de Caja) 
construido enteramente en VBA, con proyección a 5 años (FY2026E–FY2030E).

## Qué tiene de particular

**Sin fórmulas de Excel vinculadas.** El motor de proyección es código VBA que lee los supuestos 
y escribe los resultados calculados directamente en cada hoja. Más cerca de cómo funcionaría un 
modelo de producción que de una plantilla estática.

**Datos históricos reales.** Las cifras FY2024–FY2025 provienen de los filings de MELI ante la SEC 
(8-K del 24/02/2026).

**La caja como variable de cierre.** El modelo nunca calcula la caja directamente: proyecta capital 
de trabajo, PP&E, deuda y ganancias retenidas, construye el flujo de caja a partir de esas 
variaciones, y recién ahí despeja el saldo final de caja. Si Activo = Pasivo + Patrimonio sin 
ajustes manuales, la lógica está bien armada. El check cierra en cero en los 5 años proyectados.

## Simplificación deliberada

El balance de MELI incluye una cartera de crédito al consumidor completa — fondos a pagar a 
clientes, créditos de tarjeta, cartera de préstamos — que representa buena parte del activo total. 
Modelar eso correctamente requiere supuestos de originación, mora y fondeo que exceden el alcance 
de este ejercicio.

Por eso esas partidas están neteadas en una sola línea ("posición fintech") que crece a la par de 
los ingresos. El modelo se enfoca en la mecánica central de los tres estados, no en modelar un 
negocio crediticio. Es una simplificación consciente, no una omisión.

## Cómo usarlo

1. Descargá el `.xlsm` y abrilo en Microsoft Excel (requiere macros habilitadas).
2. Si Windows bloquea las macros: clic derecho sobre el archivo → Propiedades → tildar "Desbloquear".
3. Andá a la hoja **Supuestos** y modificá cualquier driver de la sección de proyección: 
   crecimiento de ingresos, margen bruto, gastos como % de ingresos, tasa impositiva, capex, 
   días de capital de trabajo (DSO/DIO/DPO), apalancamiento.
4. Ejecutá la macro `EjecutarModelo` (botón en el Dashboard, o `Alt+F8`).
5. La proyección completa se reconstruye. Verificá la fila **Check** en la hoja Balance: 
   debe dar cero en todos los años.

## Estructura

| Hoja | Contenido |
|---|---|
| `Supuestos` | Históricos FY2024–FY2025 y drivers de proyección (celdas editables en ámbar) |
| `Resultados` | Estado de resultados histórico y proyectado, con márgenes |
| `Balance` | Balance completo, con la fila de validación Activo = Pasivo + Patrimonio |
| `FlujoCaja` | Flujo de caja por método indirecto |
| `Dashboard` | KPIs, gráficos de evolución y botón de ejecución |

## Nota sobre circularidad

Los intereses (activos y pasivos) se calculan sobre los saldos de caja, inversiones y deuda del 
**período anterior**, no del período proyectado. Esto evita la referencia circular clásica 
—para saber la caja necesito el interés, para saber el interés necesito la caja— sin recurrir 
al cálculo iterativo de Excel. Es la convención estándar en modelos de este tipo.

## Fuente de datos

MercadoLibre Inc. — Reporte de resultados FY2025 (SEC Form 8-K, 24 de febrero de 2026).  
Cifras en millones de dólares estadounidenses.

---

Construido como proyecto de portfolio. Comentarios y correcciones son bienvenidos.
