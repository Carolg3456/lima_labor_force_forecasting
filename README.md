<a id="english-version"></a>

# Metropolitan Lima Labor Force Forecasting 📈

[Go to the Spanish version](#version-en-espanol)

## Executive Summary

This project develops a time-series forecasting solution to estimate the Economically Active Population (EAP) of Metropolitan Lima.

Using monthly data from January 2020 to December 2025, eight statistical forecasting alternatives were evaluated under a temporal validation framework. The objective was not simply to fit historical data, but to identify the model with the strongest performance on unseen observations.

The selected **SARIMA(2,1,2)(1,1,0)[12]** model achieved a **1.60% MAPE** during the 2025 test period. After validation, the model was re-estimated with the complete historical series to generate monthly forecasts and confidence intervals for 2026.

The results provide a quantitative baseline for labor-market monitoring, workforce planning and economic analysis.

## Business Problem

Organizations and public institutions need reliable labor-market estimates to support decisions related to employment programs, workforce capacity, economic planning and resource allocation.

However, labor-force data presents several forecasting challenges:

* Long-term growth and changing trends.
* Monthly seasonal patterns.
* Structural disruptions such as the COVID-19 pandemic.
* Increasing uncertainty across longer forecast horizons.

This analysis addresses those challenges through a structured comparison of forecasting models and an explicit measurement of out-of-sample error.

## Business Objective

The objective is to identify the model with the best predictive performance and use it to estimate the monthly evolution of Metropolitan Lima’s labor force during 2026.

The analysis supports the following business questions:

* How has the labor force evolved since the disruption observed in 2020?
* Which temporal patterns are relevant for forecasting?
* Which statistical model performs best on unseen data?
* What trajectory can be expected during 2026?
* How much uncertainty surrounds the monthly forecasts?

## Data

The dataset contains **72 monthly observations** from January 2020 to December 2025.

| Variable  | Description                                                      |
| --------- | ---------------------------------------------------------------- |
| `periodo` | Monthly observation date                                         |
| `PEA`     | Economically Active Population, expressed in thousands of people |

Source: [Central Reserve Bank of Peru statistical database](https://estadisticas.bcrp.gob.pe/estadisticas/series/mensuales/resultados/PN38050GM/html/2020-1/2025-12/).

The dataset is excluded from the repository and managed separately to maintain a clean project structure.

## Analytical Approach

The analysis was organized into five stages:

1. **Data quality assessment:** validation of dates, frequency, duplicates and missing values.
2. **Time-series diagnosis:** evaluation of trend, seasonality, stationarity and autocorrelation.
3. **Model development:** estimation of smoothing, ARIMA and SARIMA alternatives.
4. **Out-of-sample validation:** comparison against the actual observations from 2025.
5. **Final forecasting:** re-estimation of the selected model and projection of the monthly labor force for 2026.

## Models Evaluated

Eight forecasting alternatives were compared:

* Simple Moving Average — 3 months.
* Simple Moving Average — 6 months.
* Weighted Moving Average — 3 months.
* Simple Exponential Smoothing.
* Holt’s linear trend method.
* Additive Holt-Winters.
* ARIMA.
* SARIMA.

ARIMA and SARIMA parameters were selected through an AIC-based search. Final model selection was based on the lowest RMSE over the test period.

## Validation Strategy

The observations were divided chronologically:

| Dataset  | Period                     | Observations |
| -------- | -------------------------- | -----------: |
| Training | January 2020–December 2024 |           60 |
| Test     | January 2025–December 2025 |           12 |

The models were evaluated using:

* **MAE:** average magnitude of prediction errors.
* **MAPE:** average percentage prediction error.
* **RMSE:** error measure that assigns greater weight to larger deviations.

The test period remained outside the model estimation process, providing a more realistic assessment of forecasting performance.

## Model Performance

| Model                              |  Test MAE | Test MAPE |  Test RMSE |
| ---------------------------------- | --------: | --------: | ---------: |
| **SARIMA(2,1,2)(1,1,0)[12]**       | **95.23** | **1.60%** | **106.38** |
| Weighted Moving Average — 3 months |    109.70 |     1.81% |     146.43 |
| Simple Moving Average — 3 months   |    109.57 |     1.81% |     146.93 |
| Simple Exponential Smoothing       |    109.84 |     1.81% |     147.02 |
| ARIMA(3,1,3)                       |    112.75 |     1.86% |     156.42 |
| Simple Moving Average — 6 months   |    109.32 |     1.80% |     157.96 |
| Additive Holt-Winters              |    220.89 |     3.71% |     247.84 |
| Holt                               |    204.56 |     3.37% |     275.04 |

MAE and RMSE are expressed in thousands of people.

## Key Results

The selected model was:

**SARIMA(2,1,2)(1,1,0)[12]**

Its performance during the 2025 test period was:

* **MAE:** 95.23 thousand people.
* **MAPE:** 1.60%.
* **RMSE:** 106.38 thousand people.

The SARIMA model reduced test RMSE by approximately **27%** compared with the second-ranked alternative.

Residual diagnostics did not identify significant remaining autocorrelation at the evaluated lags, indicating that the model captured the main temporal structure present in the historical series.

## 2026 Outlook

After validation, the selected SARIMA structure was re-estimated using all 72 available observations.

The forecast indicates a generally upward trajectory:

| Forecast point |   Estimated labor force |
| -------------- | ----------------------: |
| January 2026   | 6,117.3 thousand people |
| December 2026  | 6,501.6 thousand people |

The model estimates an increase of approximately **384.3 thousand people** between January and December 2026.

Confidence intervals widen across the forecast horizon, reflecting greater uncertainty for more distant months. Therefore, the central forecast should be interpreted together with its upper and lower bounds.

## Business Insights

* The labor force reached its lowest point in June 2020, at approximately **2,625.3 thousand people**, reflecting the exceptional impact of the pandemic.
* A progressive recovery followed the 2020 disruption.
* By December 2025, the labor force reached approximately **6,189.4 thousand people**.
* The 2026 forecast suggests continued expansion, although monthly variations remain present.
* The selected model provides a measurable forecasting baseline that can be updated as new observations become available.
* Forecast intervals should be incorporated into planning decisions instead of relying exclusively on point estimates.

## Potential Business Applications

The analysis can support:

* Labor-market monitoring and reporting.
* Workforce supply planning.
* Design and evaluation of employment programs.
* Economic scenario development.
* Public resource and service-capacity planning.
* Early identification of deviations from the expected labor-market trajectory.

## Limitations

* The analysis is based on 72 monthly observations.
* Predictive performance was evaluated over one twelve-month test period.
* The 2020 pandemic represents an exceptional structural disruption.
* The model is univariate and does not include inflation, economic growth, migration, investment or policy variables.
* The forecasts assume that historical temporal patterns remain sufficiently relevant during 2026.
* The results support forecasting and planning but do not establish causal relationships.

## Technology Stack

* Python
* pandas
* NumPy
* SciPy
* statsmodels
* Plotly
* openpyxl
* Jupyter Notebook

## Repository Structure

```text
lima_labor_force_forecasting/
│
├── pea_lima_time_series_analysis.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

---

<a id="version-en-espanol"></a>

# Pronóstico de la fuerza laboral de Lima Metropolitana 📊

[Ir a la versión en inglés](#english-version)

## Resumen ejecutivo

Este proyecto desarrolla una solución de series temporales para pronosticar la Población Económicamente Activa (PEA) de Lima Metropolitana.

A partir de información mensual comprendida entre enero de 2020 y diciembre de 2025, se evaluaron ocho alternativas estadísticas mediante un esquema de validación temporal. El propósito no fue únicamente ajustar los datos históricos, sino identificar el modelo con mejor desempeño sobre observaciones no utilizadas durante el entrenamiento.

El modelo seleccionado, **SARIMA(2,1,2)(1,1,0)[12]**, alcanzó un **MAPE de 1.60%** durante el periodo de prueba de 2025. Después de su validación, se volvió a estimar con toda la serie disponible para generar pronósticos mensuales e intervalos de confianza para 2026.

Los resultados proporcionan una referencia cuantitativa para el monitoreo del mercado laboral, la planificación de la fuerza de trabajo y el análisis económico.

## Problema de negocio

Las organizaciones e instituciones públicas necesitan estimaciones confiables del mercado laboral para respaldar decisiones relacionadas con programas de empleo, disponibilidad de fuerza de trabajo, planificación económica y asignación de recursos.

Sin embargo, la evolución de la PEA presenta diversos desafíos:

* Tendencias de crecimiento que cambian con el tiempo.
* Patrones estacionales mensuales.
* Disrupciones estructurales como la pandemia de COVID-19.
* Mayor incertidumbre conforme se amplía el horizonte de pronóstico.

Este análisis aborda esos desafíos mediante una comparación estructurada de modelos y una medición explícita del error fuera de muestra.

## Objetivo de negocio

El objetivo es identificar el modelo con mejor capacidad predictiva y utilizarlo para estimar la evolución mensual de la fuerza laboral de Lima Metropolitana durante 2026.

El análisis busca responder las siguientes preguntas:

* ¿Cómo evolucionó la fuerza laboral después de la disrupción observada en 2020?
* ¿Qué patrones temporales son relevantes para su pronóstico?
* ¿Qué modelo estadístico presenta el mejor desempeño sobre datos no observados?
* ¿Qué trayectoria puede esperarse durante 2026?
* ¿Qué nivel de incertidumbre acompaña a las estimaciones mensuales?

## Datos

La base contiene **72 observaciones mensuales** entre enero de 2020 y diciembre de 2025.

| Variable  | Descripción                                                    |
| --------- | -------------------------------------------------------------- |
| `periodo` | Fecha mensual de observación                                   |
| `PEA`     | Población Económicamente Activa expresada en miles de personas |

Fuente: [base de datos estadísticos del Banco Central de Reserva del Perú](https://estadisticas.bcrp.gob.pe/estadisticas/series/mensuales/resultados/PN38050GM/html/2020-1/2025-12/).

El dataset se excluye del repositorio y se administra por separado para mantener una estructura limpia del proyecto.

## Enfoque analítico

El análisis se organizó en cinco etapas:

1. **Evaluación de calidad:** validación de fechas, frecuencia, duplicados y valores ausentes.
2. **Diagnóstico temporal:** análisis de tendencia, estacionalidad, estacionariedad y autocorrelación.
3. **Desarrollo de modelos:** estimación de alternativas de suavización, ARIMA y SARIMA.
4. **Validación fuera de muestra:** comparación con los valores reales observados durante 2025.
5. **Pronóstico final:** reestimación del modelo seleccionado y proyección mensual de la PEA para 2026.

## Modelos evaluados

Se compararon ocho alternativas:

* Promedio móvil simple de 3 meses.
* Promedio móvil simple de 6 meses.
* Promedio móvil ponderado de 3 meses.
* Suavización exponencial simple.
* Método de tendencia lineal de Holt.
* Holt-Winters aditivo.
* ARIMA.
* SARIMA.

Los parámetros de ARIMA y SARIMA fueron seleccionados mediante una búsqueda basada en AIC. La selección final se realizó utilizando el menor RMSE en el periodo de prueba.

## Estrategia de validación

Las observaciones se dividieron cronológicamente:

| Conjunto      | Periodo                         | Observaciones |
| ------------- | ------------------------------- | ------------: |
| Entrenamiento | Enero de 2020–diciembre de 2024 |            60 |
| Prueba        | Enero de 2025–diciembre de 2025 |            12 |

Los modelos fueron evaluados mediante:

* **MAE:** magnitud promedio de los errores.
* **MAPE:** error porcentual promedio.
* **RMSE:** medida que penaliza con mayor intensidad los errores grandes.

El periodo de prueba permaneció fuera de la estimación de los modelos, permitiendo una evaluación más realista de su capacidad predictiva.

## Desempeño de los modelos

| Modelo                             | MAE de prueba | MAPE de prueba | RMSE de prueba |
| ---------------------------------- | ------------: | -------------: | -------------: |
| **SARIMA(2,1,2)(1,1,0)[12]**       |     **95.23** |      **1.60%** |     **106.38** |
| Promedio móvil ponderado — 3 meses |        109.70 |          1.81% |         146.43 |
| Promedio móvil simple — 3 meses    |        109.57 |          1.81% |         146.93 |
| Suavización exponencial simple     |        109.84 |          1.81% |         147.02 |
| ARIMA(3,1,3)                       |        112.75 |          1.86% |         156.42 |
| Promedio móvil simple — 6 meses    |        109.32 |          1.80% |         157.96 |
| Holt-Winters aditivo               |        220.89 |          3.71% |         247.84 |
| Holt                               |        204.56 |          3.37% |         275.04 |

El MAE y el RMSE están expresados en miles de personas.

## Resultados principales

El modelo seleccionado fue:

**SARIMA(2,1,2)(1,1,0)[12]**

Su desempeño durante el periodo de prueba de 2025 fue:

* **MAE:** 95.23 miles de personas.
* **MAPE:** 1.60%.
* **RMSE:** 106.38 miles de personas.

El modelo SARIMA redujo el RMSE de prueba en aproximadamente **27%** frente a la segunda alternativa mejor posicionada.

Los diagnósticos no identificaron autocorrelación residual significativa en los rezagos evaluados, lo que indica que el modelo capturó la principal estructura temporal presente en la serie histórica.

## Perspectiva para 2026

Después de su validación, la estructura SARIMA seleccionada se volvió a estimar utilizando las 72 observaciones disponibles.

El pronóstico muestra una trayectoria generalmente ascendente:

| Punto del pronóstico |              PEA estimada |
| -------------------- | ------------------------: |
| Enero de 2026        | 6,117.3 miles de personas |
| Diciembre de 2026    | 6,501.6 miles de personas |

El modelo estima un incremento aproximado de **384.3 miles de personas** entre enero y diciembre de 2026.

Los intervalos de confianza se amplían conforme avanza el horizonte de pronóstico, reflejando una mayor incertidumbre para los meses más alejados. Por ello, las estimaciones centrales deben analizarse junto con sus límites superiores e inferiores.

## Hallazgos de negocio

* La PEA alcanzó su punto más bajo en junio de 2020, con aproximadamente **2,625.3 miles de personas**, como consecuencia del impacto excepcional de la pandemia.
* Después de la disrupción de 2020, la fuerza laboral mostró una recuperación progresiva.
* En diciembre de 2025, la PEA alcanzó aproximadamente **6,189.4 miles de personas**.
* El pronóstico para 2026 sugiere una expansión sostenida, aunque con variaciones mensuales.
* El modelo seleccionado proporciona una referencia cuantitativa que puede actualizarse a medida que se incorporen nuevas observaciones.
* Los intervalos de pronóstico deben formar parte de las decisiones de planificación, evitando depender únicamente de estimaciones puntuales.

## Aplicaciones de negocio

El análisis puede apoyar:

* Monitoreo y elaboración de reportes del mercado laboral.
* Planificación de la oferta de fuerza de trabajo.
* Diseño y evaluación de programas de empleo.
* Desarrollo de escenarios económicos.
* Planificación de recursos públicos y capacidad de atención.
* Detección temprana de desviaciones frente a la trayectoria laboral esperada.

## Limitaciones

* El análisis utiliza 72 observaciones mensuales.
* El desempeño predictivo se evaluó sobre un único periodo de prueba de doce meses.
* La pandemia de 2020 representa una disrupción estructural excepcional.
* El modelo es univariado y no incorpora inflación, crecimiento económico, migración, inversión ni variables regulatorias.
* Los pronósticos dependen de que los patrones históricos continúen siendo suficientemente relevantes durante 2026.
* Los resultados sirven para pronóstico y planificación, pero no establecen relaciones causales.

## Tecnologías

* Python
* pandas
* NumPy
* SciPy
* statsmodels
* Plotly
* openpyxl
* Jupyter Notebook

## Estructura del repositorio

```text
lima_labor_force_forecasting/
│
├── pea_lima_time_series_analysis.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```
