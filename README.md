# 🏆 Sistema de Predicción del Mundial de Fútbol con Machine Learning

## 📌 Descripción general

El presente proyecto desarrolla un sistema integral de predicción y simulación de partidos de fútbol orientado a torneos de gran escala, como la Copa del Mundo. El objetivo principal es determinar, de manera probabilística y basada en datos, qué equipos avanzarán en cada fase del torneo:

- Octavos de final  
- Cuartos de final  
- Semifinales  
- Final  
- Campeón del mundo  

Para ello, se emplean técnicas avanzadas de **aprendizaje automático (Machine Learning)** junto con métodos de **simulación estocástica**, permitiendo no solo predecir resultados puntuales, sino también modelar escenarios completos del torneo.

---

## 🎯 Objetivos

### Objetivo general
Desarrollar un modelo predictivo capaz de simular el desarrollo completo de un torneo mundial de fútbol, estimando probabilidades de clasificación y resultados en cada fase eliminatoria.

### Objetivos específicos

- Predecir el resultado de partidos utilizando modelos de clasificación.
- Estimar probabilidades de victoria, empate y derrota.
- Calcular goles esperados (xG) por equipo.
- Simular múltiples escenarios del torneo mediante Monte Carlo.
- Identificar el equipo con mayor probabilidad de ganar el campeonato.

---

## 🧠 Metodología

### 1. Enfoque de aprendizaje supervisado

Se utiliza el algoritmo **XGBoost (eXtreme Gradient Boosting)** como modelo principal de clasificación multiclase. Este modelo permite predecir el resultado de un partido según tres categorías:

- `2` → Victoria del equipo local  
- `1` → Empate  
- `0` → Victoria del equipo visitante  

El modelo se entrena con datos históricos de partidos internacionales, considerando diferencias entre características de los equipos.

---

### 2. Ingeniería de características (Feature Engineering)

A partir de los datos recopilados, se construyen variables relevantes como:

- Ratio de goles por posesión  
- Eficiencia de gol  
- Ratio de tarjetas  
- Ratio de corners  

Estas variables permiten capturar el rendimiento real de cada equipo más allá de estadísticas básicas.

---

### 3. Simulación Monte Carlo

Para robustecer las predicciones, se implementa una simulación Monte Carlo con múltiples iteraciones (por defecto 1000), donde:

- Los goles se generan mediante una distribución de Poisson.
- Se simulan resultados de partidos repetidamente.
- Se estiman probabilidades de clasificación en cada fase.

Este enfoque permite modelar la incertidumbre inherente al deporte.

---

## 📊 Fuentes de datos

El modelo se alimenta de múltiples fuentes:

- **Ranking FIFA** → Nivel competitivo de cada selección  
- **Transfermarkt** → Valor de mercado de los jugadores  
- **Datos del Mundial actual**:
  - Goles
  - Posesión
  - Tiros a puerta
  - Corners
  - Tarjetas  
- **Datos históricos (2021–2026)**:
  - Resultados de partidos internacionales  
  - Rendimiento previo  

---

## 📁 Estructura del proyecto

```
📦 Proyecto_Mundial
│
├── 📁 01_Scraping
│ └── Scripts para recolección de datos
│
├── 📁 02_Limpieza_Datos
│ └── Procesamiento y transformación de datos
│
├── 📁 03_Predicciones
│ └── Modelos XGBoost y simulaciones Monte Carlo
│
├── 📁 04_Web
│ └── Visualización (opcional)
│
├── 📁 Data
│ └── Archivos CSV (datos del modelo)
│
└── 📄 Observaciones_Modelo_XGBoost
└── Evaluación y métricas del modelo
```

---

## 🚀 Ejecución del proyecto en Google Colab

El proyecto está diseñado para ejecutarse en **Google Colab**, utilizando **Google Drive** como almacenamiento de datos.

### 🔹 Paso 1: Subir datos a Google Drive

1. Crear una carpeta en Google Drive (por ejemplo: `Proyecto_Mundial`)
2. Dentro de ella, crear una subcarpeta llamada `Data`
3. Subir todos los archivos CSV necesarios a esa carpeta

---

### 🔹 Paso 2: Abrir el proyecto en Google Colab

1. Ir a: https://colab.research.google.com  
2. Subir o abrir el notebook del proyecto  

---

### 🔹 Paso 3: Conectar Google Drive

Ejecutar el siguiente código en una celda:

```python
from google.colab import drive
drive.mount('/content/drive')
```

Esto permitirá acceder a los archivos almacenados en Drive.

🔹 Paso 4: Definir la ruta de los datos

Una vez montado Drive, se define la ruta:

```python
base_path = "/content/drive/MyDrive/Proyecto_Mundial"
data_path = f"{base_path}/Data"
```

🔹 Paso 5: Cargar los datos

Ejemplo de carga de archivos:

```python
import pandas as pd

df_historico = pd.read_csv(f"{data_path}/datos_historicos.csv")
df_ranking = pd.read_csv(f"{data_path}/ranking_fifa.csv")
df_mundial = pd.read_csv(f"{data_path}/datos_mundial.csv")
```

🔹 Paso 6: Ejecutar el pipeline

Ejecutar los módulos en orden:

Limpieza de datos
Feature engineering
Entrenamiento del modelo
Predicción de partidos
Simulación Monte Carlo

📈 Resultados del sistema

El sistema genera:

Predicción del ganador de cada partido
Probabilidades de cada resultado
Goles esperados (xG)
Probabilidad de avanzar de fase
Probabilidad de ser campeón

🛠️ Tecnologías utilizadas

Python
pandas
numpy
xgboost
scikit-learn
joblib

🔮 Mejoras futuras

Incorporar variables adicionales (lesiones, clima, táctica)
Implementar modelos más avanzados
Aumentar número de simulaciones
Desarrollar interfaz web interactiva

📝 Conclusión

Este proyecto demuestra cómo la integración de Machine Learning y simulación probabilística permite analizar y predecir el comportamiento de un torneo de fútbol de manera estructurada y basada en datos. Si bien el modelo no garantiza resultados exactos, proporciona una aproximación robusta y útil para la toma de decisiones y análisis deportivo.
