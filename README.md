# telco-churn-ml-jr87
Este repo construye un baseline para predecir churn y documenta limpieza, métricas y análisis de errores.
Incluye un notebook inicial y reportes en /reports para seguimiento del proyecto.

## Resultados (baseline)
| Modelo | ROC-AUC | F1 (churn=1) | Precision/Recall (churn=1) |
|---|---:|---:|---:|
| Logistic Regression + OneHot Pipeline | 0.842 | 0.61 | 0.66 / 0.56 |

Notas:
- Se corrigió leakage al excluir columnas derivadas del target (ej. `churn`).
- Próximos pasos: `class_weight="balanced"` y ajuste de threshold para mejorar recall.
