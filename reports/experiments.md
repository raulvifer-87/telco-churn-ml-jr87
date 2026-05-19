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
