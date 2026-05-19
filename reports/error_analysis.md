# Error Analysis (baseline)

## Qué errores importan
En churn, suele importar capturar a los churners (clase 1). Por eso se revisan **falsos negativos** (clientes que sí churn y el modelo predice no).

## Observaciones iniciales
- Recall (churn=1) en baseline: **0.56** → aún se están escapando churners.
- Próximo paso para mejorar: `class_weight="balanced"` y/o bajar el threshold.

## Plan de revisión (pendiente)
- Revisar 10 falsos negativos con mayor probabilidad de churn.
- Revisar 10 falsos positivos con mayor probabilidad de churn.
- Identificar patrones (contrato, tenure, MonthlyCharges, soporte, etc.)
