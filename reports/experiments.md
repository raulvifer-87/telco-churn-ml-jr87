# Experiments log

## Baseline v0.1 — Logistic Regression + OneHot Pipeline
- **Modelo:** LogisticRegression (baseline) con Pipeline (imputer + OneHotEncoder)
- **Validación:** train/test split 80/20 (stratify)
- **Métricas (test):**
  - ROC-AUC: **0.842**
  - F1 (churn=1, threshold=0.5): **0.61**
  - Precision/Recall (churn=1): **0.66 / 0.56**
- **Notas:**
  - Se detectó un resultado “perfecto” inicialmente (1.0/1.0) por **leakage** al incluir una columna derivada (`churn`) en features. Se corrigió eliminando columnas prohibidas (`Churn`, `churn`, bins derivados).
  - Apareció `ConvergenceWarning` (no bloquea resultados). Posible mejora: StandardScaler en numéricas y/o aumentar `max_iter`, y evaluar `class_weight="balanced"`.

## Próximo experimento sugerido
- LogisticRegression con `class_weight="balanced"` para subir recall de churn.
- Ajuste de threshold (0.4, 0.35) para priorizar recall vs precisión.
- 
## Baseline v0.2 — Logistic Regression (class_weight="balanced")
- **Modelo:** LogisticRegression + Pipeline (imputer + OneHotEncoder)
- **Validación:** train/test split 80/20 (stratify)
- **Métricas (test):**
  - ROC-AUC: **0.842** (≈ 0.8416)
  - F1 (churn=1, threshold=0.5): **0.616**
  - Precision/Recall (churn=1): **0.51 / 0.79**
- **Interpretación de negocio:**
  - Se prioriza **recall** (capturar churners) a costa de menor precisión → más falsos positivos, pero menos churners “se escapan”.

### Threshold seleccionado (operación)
- **Threshold:** 0.70  
- **Volumen estimado:** ~26.6% de clientes marcados como churn (predicted_churn_rate=0.266)  
- **Motivo:** operación conservadora para reducir volumen de contacto; balancea precisión/recall (~0.60/0.60).

- ### Threshold alternativo (equilibrio)
- **Threshold:** 0.55  
- **Volumen estimado:** ~38.0% de clientes marcados como churn (predicted_churn_rate=0.380)  
- **Motivo:** maximiza F1 (0.618) con recall alto (0.751) para retención más agresiva.

