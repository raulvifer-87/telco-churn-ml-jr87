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

## Resultados (baseline)
| Modelo | ROC-AUC | F1 (churn=1) | Precision/Recall (churn=1) |
|---|---:|---:|---:|
| Logistic Regression + OneHot (baseline) | 0.842 | 0.606 | 0.66 / 0.56 |
| Logistic Regression + OneHot (balanced) | 0.842 | 0.616 | 0.51 / 0.79 |

Nota: el modelo balanced prioriza capturar churners (recall alto) con más falsos positivos.
