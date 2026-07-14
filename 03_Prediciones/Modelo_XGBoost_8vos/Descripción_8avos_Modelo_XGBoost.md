# 🚀 Predicción de Clasificados a Octavos de Final – Mundial 2026

## 📌 Descripción del proyecto

Este proyecto aplica técnicas de **Machine Learning** para predecir los ganadores de los dieciseisavos de final del Mundial de Fútbol 2026, determinando así los 16 equipos que avanzarán a octavos de final.

El modelo utiliza un enfoque híbrido que combina:

* Un clasificador **XGBoost** entrenado con más de 2.000 partidos internacionales históricos, que proporciona probabilidades de:

  * Victoria local
  * Empate
  * Victoria visitante

* Un mecanismo de desempate basado en la **distribución de Poisson** para simular casos donde las probabilidades no son concluyentes (umbral del 60 %).

* Una **simulación Monte Carlo (1000 iteraciones)** para calcular porcentajes de clasificación, proporcionando robustez y confianza.

Este proyecto está diseñado como un trabajo universitario que demuestra la integración de técnicas avanzadas de aprendizaje automático, análisis de datos y simulación estocástica en el dominio deportivo.

---

## 🎯 Objetivos

### 🥇 Primario

Determinar qué equipos superan la ronda de dieciseisavos y se clasifican a octavos de final.

### 📌 Secundarios

* Estimar los goles esperados (**xG**) para cada enfrentamiento
* Cuantificar la incertidumbre mediante simulación Monte Carlo
* Generar un flujo de trabajo reproducible y documentado

---

## 📊 Datos utilizados

### 📁 Archivos necesarios

| Archivo                | Descripción                                    | Procedencia    |
| ---------------------- | ---------------------------------------------- | -------------- |
| `cruces_16avos.csv`    | Emparejamientos de dieciseisavos (16 partidos) | FIFA           |
| `datos_historicos.csv` | Historial de partidos internacionales (2000+)  | Bases públicas |
| `datos_mundial.csv`    | Estadísticas de fase de grupos                 | FIFA           |
| `ranking_fifa.csv`     | Ranking ELO FIFA                               | FIFA           |
| `transfermarkt.csv`    | Valor de mercado de plantillas                 | Transfermarkt  |

📌 Todos los archivos deben estar en la misma carpeta o en la ruta:

```python
base_path = '/content/drive/MyDrive/Simulaciones_Mundial/Data'
```

---

## 🧹 Preprocesamiento

Se realizó limpieza y normalización de nombres de equipos:

| Nombre original                 | Nombre normalizado |
| ------------------------------- | ------------------ |
| Estados Unidos                  | EE. UU.            |
| Bosnia y Herzegovina            | Bosnia-Herzegovina |
| República Democrática del Congo | RD Congo           |
| Côte d'Ivoire                   | Costa de Marfil    |

### 📈 Features derivadas

* `ratio_goles_posesion`
* `ratio_tarjetas`

---

## 🧠 Modelo XGBoost y enfoque híbrido

### ⚙️ XGBoost

Algoritmo de **Gradient Boosting** que construye árboles secuenciales corrigiendo errores previos.

### 🎯 Clasificación

* `1` → Victoria local
* `0` → Empate
* `-1` → Victoria visitante

---

### 📥 Features de entrada

Se utilizan diferencias entre equipos:

* Ranking FIFA
* Valor de mercado
* Goles promedio
* Posesión
* Tiros a puerta
* Córners
* Tarjetas
* Faltas
* Pases completados
* (+30 variables)

---

### 🔧 Hiperparámetros

```python
n_estimators = 300
max_depth = 8
learning_rate = 0.05
subsample = 0.8
colsample_bytree = 0.8
random_state = 42
eval_metric = 'mlogloss'
```

---

### 🔁 Validación cruzada

* Método: **Stratified K-Fold (5 folds)**
* Precisión promedio: **~66 %**

---

## ⚖️ Enfoque híbrido: XGBoost + Poisson

### 📌 Regla de decisión

* Si probabilidad > 60 % → ganador directo
* Si no → simulación con Poisson

### 🧮 Fórmulas

```python
λ_home = max(0.1, avg_goals_home * (0.8 + 0.4 * p_home))
λ_away = max(0.1, avg_goals_away * (0.8 + 0.4 * p_away))
```

Se simulan **1000 partidos** y el equipo con más victorias es el ganador.

---

## 🎲 Simulación Monte Carlo

* 1000 simulaciones del torneo
* Calcula probabilidades de clasificación
* Mide estabilidad del modelo

---

## 🔧 Instalación de dependencias

```bash
pip install pandas numpy scikit-learn xgboost
```

📌 En Google Colab:

```bash
!pip install xgboost
```

---

## 🚀 Ejecución del modelo

### ☁️ Opción 1: Google Colab

```python
from google.colab import drive
drive.mount('/content/drive')
```

```python
base_path = '/content/drive/MyDrive/Simulaciones_Mundial/Data'
```

Ejecutar todas las celdas.

---

### 💻 Opción 2: Local

```bash
python prediccion_octavos_avanzada.py
```

---

## 📈 Resultados esperados

### 📊 Tabla de predicciones

Incluye:

* Equipos
* xG
* Marcador
* Probabilidades
* Ganador

### 🏆 Clasificados

Lista de los 16 equipos

### 📊 Monte Carlo

Porcentaje de clasificación

---

### 🧾 Ejemplo

```
📊 TABLA DE PREDICCIONES
Sudáfrica vs Canadá → Ganador: Sudáfrica  
Alemania vs Paraguay → Ganador: Alemania  
```

---

## 🔬 Interpretación

* **>60 %** → alta confianza
* **40–60 %** → partido incierto
* **Monte Carlo alto** → predicción estable

---

## ⚠️ Limitaciones

* Precisión máxima ~66 %
* No incluye lesiones ni clima
* Posible sobreajuste (~78 % entrenamiento)

---

## 🚀 Mejoras futuras

* Datos más recientes
* Variables adicionales
* Modelos alternativos (LightGBM, NN)
* Ensemble
* Optimización del umbral

---

## 🔗 Enlaces de interés

* FIFA World Cup
* Transfermarkt
* XGBoost Docs
* Scikit-learn

---

## 👨‍💻 Autor

Proyecto desarrollado como trabajo académico en **Machine Learning aplicado al deporte**, integrando modelos predictivos, estadística avanzada y simulación.

