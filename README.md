# Crecimiento Económico de Guatemala en Función de los Factores de Producción

Modelo econométrico basado en la función de producción de Cobb-Douglas, que analiza los determinantes del crecimiento económico de Guatemala durante 43 años (1980-2022).

## 🎯 Objetivo

Identificar y cuantificar la contribución de los principales factores productivos —inversión, inversión extranjera directa, importaciones de bienes de capital, tierra agrícola y crecimiento poblacional— al crecimiento del PIB de Guatemala, validando empíricamente la teoría de la función de producción Q = f(T, L, K).

## 📈 Modelo econométrico

Regresión lineal múltiple especificada como:

```
PIBᵢ = β0 + β1·Invᵢ + β2·IEDᵢ + β3·BCᵢ + β4·TAᵢ + β5·Pobᵢ + e
```

**Variables:**
- **PIB**: variación porcentual del PIB (variable dependiente)
- **Inv**: inversión total, % del PIB
- **IED**: inversión extranjera directa, % del PIB
- **BC**: importaciones CIF de bienes de capital, millones USD
- **TA**: tierra agrícola, % del área de tierra
- **Pob**: crecimiento poblacional, % anual

**Periodo:** 1980–2022 (43 observaciones) · **Fuentes:** Banco de Guatemala, Banco Mundial, FMI

## 📊 Resultados principales

| Variable | Coeficiente | t | P>\|t\| |
|---|---|---|---|
| Inversión total | 0.2734 | 2.95 | 0.006 |
| IED | 0.2837 | 2.46 | 0.019 |
| Bienes de capital | 0.0017 | 2.36 | 0.023 |
| Tierra agrícola | 0.1501 | 2.08 | 0.045 |
| Crecimiento poblacional | 4.4779 | 2.07 | 0.046 |
| Constante | -20.6038 | -3.20 | 0.003 |

**R² = 0.5527** · Todos los coeficientes son estadísticamente significativos (p < 0.05) y muestran relación positiva con el crecimiento económico.

### Pruebas de diagnóstico realizadas
- Matriz de correlación y factor de inflación de varianza (VIF) — sin multicolinealidad severa (VIF promedio: 7.28)
- Test de Skewness/Kurtosis y Shapiro-Wilk — normalidad de residuos
- Test de Breusch-Pagan/Cook-Weisberg — homocedasticidad (no se rechaza varianza constante, p = 0.083)
- Test de especificación (Cameron & Trivedi IM-test)

## 📂 Contenido del repositorio

| Archivo | Descripción |
|---|---|
| `Modelo_Econométrico_.pdf` | Informe completo: introducción, metodología, resultados, interpretación económica, conclusiones y anexos (tablas de regresión, estadísticas descriptivas, matriz de correlación, VIF, gráficas de dispersión y densidad kernel) |
| `Modelo.dta` | Base de datos en formato Stata con las series 1980-2022, lista para reproducir el análisis |

## 🛠️ Herramientas utilizadas

**Stata** — estimación de la regresión y pruebas de diagnóstico mediante los comandos: `regress`, `pwcorr`, `vif`, `graph matrix`, `sktest`, `swilk`, `kdensity`, `imtest`, `estat hettest`

## ▶️ Cómo reproducir el análisis

1. Descarga `Modelo.dta`
2. Ábrelo con **Stata** (o alternativamente **RStudio**, importando el `.dta` con el paquete `haven`: `read_dta("Modelo.dta")`)
3. Comandos principales para replicar el modelo:
   ```stata
   regress pib inv ied bc ta pob
   vif
   pwcorr pib inv ied bc ta pob
   predict error, resid
   sktest error
   swilk error
   estat hettest
   ```
4. Consulta `Modelo_Econométrico_.pdf` para la interpretación completa de cada resultado

## ⚠️ Nota

Datos macroeconómicos reales de fuentes oficiales (Banco de Guatemala, Banco Mundial, FMI), actualizados a mayo de 2024. El análisis y las interpretaciones son elaboración propia con fines académicos.

---
*Proyecto desarrollado para el curso de Métodos Econométricos I, Facultad de Ciencias Económicas, UMG.*
