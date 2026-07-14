# 🏆 Predicción de Cuartos de Final - Mundial de Fútbol

**Descubre quién pasará a cuartos de final, con qué marcador y probabilidades, usando un modelo XGBoost entrenado con datos históricos y simulación Monte Carlo.**

---

## 📌 Resumen ejecutivo

Este proyecto predice los resultados de los **cuartos de final** de la Copa del Mundo, basándose en:

* **Datos históricos** de partidos internacionales.
* **Ranking FIFA** y **valor de mercado** (Transfermarkt).
* **Estadísticas de la fase de grupos** del torneo actual (goles, posesión, tiros, etc.).
* Un modelo **XGBoost** optimizado con validación cruzada.
* **Simulación Monte Carlo** (1000 iteraciones) para estimar probabilidades de victoria, empate y goles promedio.

El resultado es una tabla clara y detallada con el marcador más probable, las probabilidades de cada resultado y los goles esperados (xG), tanto en modo determinista como en modo estocástico.

---

## 🎯 Objetivos del análisis

1. **Predecir el ganador** de cada cruce de cuartos de final.
2. **Estimar el marcador** más probable (goles local y visitante).
3. **Calcular probabilidades** de victoria local, empate y victoria visitante.
4. **Obtener goles esperados (xG)** para cada equipo.
5. **Simular 1000 veces** cada partido para obtener estadísticas robustas.

---

## 🧠 Metodología

### 1. Preparación de datos

Se combinan múltiples fuentes:

* **Ranking FIFA**: Puntuación de cada selección.
* **Transfermarkt**: Valor de mercado de la plantilla.
* **Datos del Mundial actual**: Promedios de goles, posesión, tiros a puerta, corners, tarjetas, etc.
* **Datos históricos**: Resultados de partidos previos (usados para entrenar el modelo).

Se aplica una limpieza de nombres (normalización) y se construyen características derivadas como:

* `ratio_goles_posesion`
* `ratio_tarjetas`
* `eficiencia_gol`
* `ratio_corners`

---

### 2. Modelo XGBoost

Se entrena un clasificador **XGBoost** con las diferencias de características entre local y visitante, y un *peso local* (factor de ventaja de campo). El target es:

* `2` → victoria local
* `1` → empate
* `0` → victoria visitante

Se optimizan hiperparámetros mediante **RandomizedSearchCV** con validación cruzada de 3 folds.

---

### 3. Predicción determinista

Para cada partido de cuartos:

* Se calculan las diferencias de características.
* Se aplica el modelo y se obtienen las probabilidades de cada resultado.
* Se asigna el ganador según la mayor probabilidad.
* Se estima el marcador ajustando los goles promedio a las probabilidades y redondeando.

---

### 4. Simulación Monte Carlo

Se repite el proceso 1000 veces:

* Se extraen goles de una distribución **Poisson** con media ajustada por las probabilidades del modelo.
* En caso de empate, se resuelve por penales (probabilidad basada en el ranking FIFA).
* Se acumulan las victorias, empates y goles promedio.

---

## 🚀 Cómo ejecutarlo

1. Clona el repositorio y coloca los archivos CSV en la carpeta `Data/`.

2. Abre `Modelo_XGBoost_Semifinales` en Google Colab.

3. Ejecuta el script.

4. El sistema realizará automáticamente:

   * Montaje de Google Drive (si estás en Colab).
   * Carga y limpieza de los datos.
   * Entrenamiento (o carga) del modelo XGBoost.
   * Generación de predicciones deterministas y simulación Monte Carlo.

5. Los resultados se mostrarán directamente en la consola.

---

## 📈 Mejoras futuras

* Incorporar **lesiones**, **clima**, **estilo de juego** o **motivación** como variables adicionales.
* Evaluar otros modelos como **Random Forest** o **Redes Neuronales**.
* Extender la simulación a fases posteriores (semifinales y final).
* Desarrollar una interfaz web interactiva para visualizar resultados.

---

## 📝 Notas técnicas

* **Librerías utilizadas**: `pandas`, `numpy`, `xgboost`, `scikit-learn`, `joblib`.
* **Entrenamiento**: Se realiza con datos históricos de partidos entre selecciones, utilizando diferencias de variables como características.
* **Validación**: RandomizedSearchCV con 3 folds y 20 combinaciones de hiperparámetros.
* **Precisión del modelo**: Aproximadamente entre 70% y 80%, dependiendo de los datos utilizados.

---

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Si deseas mejorar el modelo, añadir nuevas características o corregir errores, puedes abrir un **issue** o enviar un **pull request**.
