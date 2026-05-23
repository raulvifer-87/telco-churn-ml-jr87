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

# Error Analysis (modelo balanced)

## Configuración
- Modelo: Logistic Regression + OneHot (class_weight="balanced")
- Threshold operativo: **0.70**
- Motivo: operación conservadora (reduce volumen de contactos) y balancea precisión/recall (~0.60/0.60).
- % marcado como churn (test): ~26.6%

## Falsos Negativos (churners que se escaparon)
Patrones observados:
- Por contrato (proporciones en FN): Month-to-month **70.47%**, One year **23.49%**, Two year **6.04%**.
- Muchos FN tienen probas cercanas al umbral (≈0.67–0.70): casos “borderline” que se pierden por una decisión operativa conservadora.
- Se observan FN con contratos no mensuales (One year/Two year) donde el modelo tiende a subestimar riesgo: posible falta de variables (satisfacción/promos) o necesidad de interacciones (contrato × tenure × cargos).

## Falsos Positivos (contactos innecesarios)
Patrones observados:
- Por contrato (proporciones en FP): Month-to-month **98.67%**, One year **1.33%**.
- Perfil típico de FP: Month-to-month + Fiber optic + MonthlyCharges altos + PaperlessBilling=Yes + PaymentMethod=Electronic check + OnlineSecurity/TechSupport=No.
- Algunas predicciones erróneas tienen probas muy altas (≈0.88–0.92): el modelo está “muy seguro” pero falla → sugiere variables no observadas o falta de interacciones no lineales.

## Acciones recomendadas
- Estrategia 2 etapas: mantener threshold=0.70, pero mandar a revisión manual el “borde” 0.65–0.70 (para reducir FN sin disparar demasiado FP).
- Considerar thresholds por segmento: uno para Month-to-month y otro para contratos anuales.
- Probar un modelo no lineal (GradientBoosting/RandomForest) para capturar interacciones.
