# EDA (inicio)

Objetivo: entender datos y detectar riesgos (nulos, tipos, leakage).

Checklist:
- Distribución del target (Churn)
- Nulos y tipos
- Variables sospechosas (leakage)
- 3 insights accionables

## Datos (snapshot)
- **Fuente:** Kaggle — Telco Customer Churn (blastchar)
- **Tamaño:** 7043 filas, 21 columnas
- **Target:** Churn (Yes/No)
- **Churn rate:** 26.54% Yes, 73.46% No

## Primeras hipótesis (3)
- **H1 (Contrato):** El tipo de contrato es un driver fuerte: **Month-to-month** churn **42.71%** vs **One year 11.27%** y **Two year 2.83%**. (Clientes sin permanencia se van mucho más.)
- **H2 (Antigüedad):** La antigüedad reduce churn: **0–6 meses 52.94%**, **6–12 35.89%**, **12–24 28.71%**, **24–48 20.39%**, **48–72 9.51%**. (Riesgo altísimo al inicio.)
- **H3 (Precio):** MonthlyCharges se asocia con churn: cuartil bajo **11.24%**, medio **24.58%**, alto **37.51%**, muy alto **32.88%**. (Sube con el precio, con ligera caída en el cuartil más alto.)

## Próximo paso 
- Limpiar `TotalCharges` (convertir a numérico y manejar espacios).
- Preparar variables numéricas/categóricas y pipeline.
- Baseline con `OneHotEncoder + LogisticRegression` y métrica ROC-AUC/F1.
- Error analysis: falsos positivos/negativos típicos.
