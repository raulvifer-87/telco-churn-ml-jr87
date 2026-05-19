# EDA (avance)

## Objetivo
Entender los datos y detectar riesgos (nulos, tipos, leakage) para construir un baseline de churn.

## Datos (snapshot)
- **Fuente:** Kaggle — Telco Customer Churn (blastchar)
- **Tamaño:** 7043 filas, 21 columnas
- **Target:** `Churn` (Yes/No)
- **Churn rate:** 26.54% Yes, 73.46% No

## Calidad de datos (notas)
- Se limpió `TotalCharges` para convertirlo a numérico (había espacios/strings).
- Se evitó **leakage**: no usar columnas derivadas del target (ej. `churn`) dentro de features.

## Primeras hipótesis (3)
- **H1 (Contrato):** `Month-to-month` churn **42.71%** vs `One year` **11.27%** y `Two year` **2.83%**.
- **H2 (Antigüedad):** 0–6 meses **52.94%**, 6–12 **35.89%**, 12–24 **28.71%**, 24–48 **20.39%**, 48–72 **9.51%**.
- **H3 (Precio):** cuartil bajo **11.24%**, medio **24.58%**, alto **37.51%**, muy alto **32.88%**.

## Siguiente paso
Ver resultados del modelo en `reports/experiments.md` y análisis de errores en `reports/error_analysis.md`.
