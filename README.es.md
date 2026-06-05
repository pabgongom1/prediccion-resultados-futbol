# Métodos estadísticos para la predicción de resultados en el fútbol

[English version](README.md)

Trabajo de Fin de Grado — Doble Grado en Matemáticas y Estadística, Universidad de Sevilla (2024–2025).

Este proyecto explora distintas técnicas estadísticas y de machine learning para predecir resultados de partidos de la Primera División española (LaLiga), y evalúa las predicciones mediante una estrategia de apuestas que se utiliza como medida real de si los modelos capturan valor predictivo genuino.

## Resumen

Se abordan dos objetivos de predicción:

* **Número de goles** por equipo, usado para apostar en el mercado Over/Under 2.5 goles.
* **Resultado del partido (1X2)** — victoria local, empate o victoria visitante — usado para apostar directamente al desenlace.

Los modelos se entrenan con las temporadas 2018/19–2022/23 de LaLiga y se evalúan sobre la temporada 2023/24. Las predicciones se comparan con las cuotas de Bet365, y el rendimiento se mide principalmente mediante el **retorno de la inversión (ROI)**, que refleja si los modelos habrían sido rentables y no solo acertados.

## Modelos

|#|Modelo|Tipo|Objetivo|
|-|-|-|-|
|1|Poisson con independencia|Clásico|Goles|
|2|Poisson con independencia + ponderación temporal|Clásico|Goles|
|3|Poisson bivariado + ponderación temporal|Clásico|Goles|
|4|Random Forest (regresión)|Machine learning|Goles|
|5|Random Forest (clasificación)|Machine learning|Resultado (1X2)|
|6|XGBoost (clasificación)|Machine learning|Resultado (1X2)|

Los modelos de goles (1–4) parten de los marcos clásicos de Maher (1982) y Dixon–Coles (1997), incluyendo una extensión bivariada que captura la correlación entre los goles de ambos equipos. Los modelos de resultado (5–6) usan covariables de los equipos (clasificación de la temporada anterior, valor de mercado de la plantilla, edad media, gasto en fichajes de verano y puntuaciones ELO dinámicas).

## Resultados principales

**Modelos de goles — mercado Over/Under 2.5:**

|Modelo|Apuestas|ROI|
|-|-|-|
|Poisson independencia|37|10,4%|
|Poisson + ponderación temporal|71|19,1%|
|**Poisson bivariado**|38|**23,6%**|
|Random Forest|19|11,3%|

**Modelos de resultado — mercado 1X2 (ROI medio sobre 100 modelos entrenados):**

|Modelo|Precisión global|ROI|
|-|-|-|
|Random Forest|48,6%|5,3%|
|**XGBoost**|**51,5%**|**9,1%**|

Destacan dos hallazgos. Entre los modelos de goles, el **Poisson bivariado con ponderación temporal obtuvo el mejor retorno (23,6% de ROI)**, lo que muestra que modelar la dependencia entre los goles de los equipos y dar más peso a los partidos recientes aporta valor real. Entre los modelos de resultado, **XGBoost superó a Random Forest** tanto en precisión como en ROI, y fue notablemente mejor prediciendo victorias visitantes — la clase más difícil de acertar y la asociada a cuotas más altas. Todos los modelos de regresión generaron un retorno neto positivo a lo largo de la temporada.

## Estructura del repositorio

```
.
├── README.md          # Versión en inglés
├── README.es.md       # Este archivo (español)
├── src/               # Archivos R Markdown (modelos y análisis)
├── data/              # Resultados de partidos y datos de equipos (CSV)
└── docs/              # Memoria completa (PDF) y presentación de la defensa
```

## Tecnologías

R, con `caret`, `randomForest`, `xgboost`, `dplyr`, `ggplot2`, `readr`, `readxl` y `kableExtra`.

## Fuentes de datos

* [Football-Data.co.uk](https://www.football-data.co.uk/spainm.php) — resultados históricos y cuotas de Bet365.
* [Transfermarkt](https://www.transfermarkt.es) — valor de mercado de las plantillas, edad media y gasto en fichajes.
* [ClubElo](http://clubelo.com/) a través del repositorio [xgabora/Club-Football-Match-Data-2000-2025](https://github.com/xgabora/Club-Football-Match-Data-2000-2025) — puntuaciones ELO.

## Limitaciones y líneas futuras

La estrategia de apuestas de clasificación no incorpora las probabilidades implícitas de la casa de apuestas (a diferencia de la de goles), lo que limita la detección de apuestas con valor esperado positivo. Solo se usaron cuotas de Bet365; incorporar más casas ayudaría a identificar mejores oportunidades de valor. Un paso natural sería aplicar los modelos a temporadas posteriores para comprobar si su rendimiento se mantiene en el tiempo.

## Autor

Pablo González Gómez — [LinkedIn](https://www.linkedin.com/in/pablo-gonzalez-gomez)


