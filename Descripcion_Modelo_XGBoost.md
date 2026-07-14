# 📘 Modelo XGBoost para Predicción de Partidos de Fútbol

Este documento describe el modelo de **XGBoost (Extreme Gradient Boosting)** utilizado para predecir los resultados de los partidos de la Copa del Mundo (cuartos de final, semifinales y final). Se explican los fundamentos matemáticos, la ingeniería de características, el proceso de entrenamiento y la justificación de su elección.

---

## 🧠 1. ¿Qué es XGBoost?

XGBoost es una implementación optimizada y escalable del algoritmo **Gradient Boosting** (GBM). Pertenece a la familia de métodos de **ensemble learning** que combinan múltiples árboles de decisión débiles para formar un modelo predictivo potente.

### 1.1. Gradient Boosting en pocas palabras

El boosting secuencial construye árboles de forma iterativa, donde cada nuevo árbol corrige los errores (residuos) del conjunto anterior. La predicción final es la suma ponderada de las predicciones de todos los árboles:

$$
\hat{y}_i = \sum_{k=1}^{K} f_k(x_i), \quad f_k \in \mathcal{F}
$$

donde:
- $x_i$ son las características del partido $i$,
- $f_k$ es un árbol de decisión,
- $\mathcal{F}$ es el espacio de funciones (árboles),
- $K$ es el número total de árboles.

### 1.2. Función objetivo de XGBoost

XGBoost minimiza una función objetivo regularizada que combina una **pérdida por error** y un **término de penalización** por complejidad:

$$
\mathcal{L}(\theta) = \sum_{i=1}^{n} \ell(y_i, \hat{y}_i) + \sum_{k=1}^{K} \Omega(f_k)
$$

donde:
- $\ell$ es la función de pérdida (en nuestro caso, **log-loss** para clasificación multiclase),
- $\Omega(f) = \gamma T + \frac{1}{2}\lambda \|\mathbf{w}\|^2$ es la regularización, con $T$ el número de hojas del árbol, $\mathbf{w}$ los pesos de las hojas, $\gamma$ y $\lambda$ hiperparámetros de penalización.

Esta regularización evita el sobreajuste y mejora la generalización.

---

## 📐 2. Matemáticas del entrenamiento de XGBoost

En cada iteración $t$, se añade un nuevo árbol $f_t$ que minimiza una **aproximación de segundo orden** de la pérdida:

$$
\mathcal{L}^{(t)} \simeq \sum_{i=1}^{n} \left[ \ell(y_i, \hat{y}_i^{(t-1)}) + g_i f_t(x_i) + \frac{1}{2} h_i f_t^2(x_i) \right] + \Omega(f_t)
$$

donde:
- $g_i = \partial_{\hat{y}^{(t-1)}} \ell(y_i, \hat{y}^{(t-1)})$ es el gradiente (primera derivada),
- $h_i = \partial^2_{\hat{y}^{(t-1)}} \ell(y_i, \hat{y}^{(t-1)})$ es la hessiana (segunda derivada).

Al expandir y reordenar, la ganancia al dividir un nodo en una hoja se calcula como:

$$
\text{Ganancia} = \frac{1}{2} \left[ \frac{(\sum_{i \in I_L} g_i)^2}{\sum_{i \in I_L} h_i + \lambda} + \frac{(\sum_{i \in I_R} g_i)^2}{\sum_{i \in I_R} h_i + \lambda} - \frac{(\sum_{i \in I} g_i)^2}{\sum_{i \in I} h_i + \lambda} \right] - \gamma
$$

donde $I_L$ e $I_R$ son los conjuntos de muestras en las hojas izquierda y derecha, e $I = I_L \cup I_R$. Solo se realiza la partición si la ganancia supera a $\gamma$.

Este enfoque permite una poda eficiente y controla la complejidad del árbol.

---

## ⚽ 3. Aplicación a la predicción de fútbol

### 3.1. Problema de clasificación

El objetivo es predecir el resultado de un partido entre dos equipos (local y visitante). Se trata de un problema de **clasificación multiclase** con tres clases:

- **Victoria local** (codificada como `2`),
- **Empate** (codificado como `1`),
- **Victoria visitante** (codificada como `0`).

La función de pérdida utilizada es **log-loss** (entropía cruzada) para clasificación multiclase:

$$
\ell(y, \hat{y}) = -\sum_{c=1}^{3} y_c \log(\hat{y}_c)
$$

donde $y_c$ es 1 si la clase real es $c$, y 0 en caso contrario; $\hat{y}_c$ es la probabilidad predicha por el modelo para esa clase.

### 3.2. Ingeniería de características (Feature Engineering)

A partir de las estadísticas de los equipos (provenientes de datos históricos del mundial, ranking FIFA, valor de mercado, etc.), se construyen características que reflejan la **diferencia** entre ambos equipos y algunas relaciones adicionales.

#### Características base (diferencias)

Para cada atributo numérico $A$ (por ejemplo, `avg_Goles_total`, `avg_Posesión_total`, `Puntuación` del ranking FIFA, `Valor_mercado`), se calcula:

$$
\Delta A = A_{\text{local}} - A_{\text{visitante}}
$$

Esto captura la ventaja relativa del local sobre el visitante.

#### Características derivadas (ratios)

Se generan ratios que miden la eficiencia ofensiva, defensiva y de control del juego:

- **Ratio de goles por posesión**:
$$
\text{ratio\_goles\_posesion} = \frac{\text{avg\_Goles\_total}}{\text{avg\_Posesión\_total} + 0.01}
$$
- **Ratio de tarjetas por faltas** (indica disciplina):
$$
\text{ratio\_tarjetas} = \frac{\text{avg\_Tarjetas\_amarillas\_total}}{\text{avg\_Faltas\_total} + 0.01}
$$
- **Eficiencia de gol** (goles por remate a puerta):
$$
\text{eficiencia\_gol} = \frac{\text{avg\_Goles\_total}}{\text{avg\_Remates\_a\_puerta\_total} + 0.01}
$$
- **Ratio de corners por posesión**:
$$
\text{ratio\_corners} = \frac{\text{avg\_Córneres\_total}}{\text{avg\_Posesión\_total} + 0.01}
$$

Luego, también se calcula la diferencia de cada ratio entre local y visitante.

#### Característica adicional: `peso_local`

Se incorpora un factor de ventaja de localía fijo (`0.55`), que refleja la ligera ventaja histórica de jugar en casa (aunque en mundiales en sede neutral, este factor se reduce).

### 3.3. Escalado de características

Las características se **estandarizan** (media 0, desviación estándar 1) usando `StandardScaler` para que todas las variables contribuyan por igual y para acelerar la convergencia del gradiente.

---

## 🔧 4. Entrenamiento y optimización de hiperparámetros

### 4.1. Datos de entrenamiento

Se utilizan **partidos históricos** (de mundiales anteriores) con resultados reales. Para cada partido se construyen las características diferenciales y se asigna la clase target (local gana, empate, visitante gana).

### 4.2. Búsqueda de hiperparámetros con RandomizedSearchCV

Se realiza una búsqueda aleatoria sobre el espacio de hiperparámetros más relevantes para XGBoost:

| Hiperparámetro | Rango / Valores | Descripción |
|----------------|-----------------|-------------|
| `n_estimators` | 200, 300 | Número de árboles (iteraciones de boosting) |
| `max_depth` | 6, 8, 10 | Profundidad máxima de cada árbol |
| `learning_rate` | 0.03, 0.05, 0.07 | Tasa de aprendizaje (contrae la contribución de cada árbol) |
| `subsample` | 0.7, 0.8, 0.9 | Fracción de muestras usadas para entrenar cada árbol |
| `colsample_bytree` | 0.7, 0.8, 0.9 | Fracción de características usadas en cada árbol |

La búsqueda utiliza validación cruzada de 3 folds y optimiza la **accuracy** (precisión global).

### 4.3. Regularización y early stopping

Además de los hiperparámetros de búsqueda, se configuran:

- **`early_stopping_rounds = 10`**: detiene el entrenamiento si la métrica de validación no mejora en 10 rondas.
- **`validation_split = 0.1`**: reserva el 10% de los datos de entrenamiento como conjunto de validación para el early stopping.
- **Regularización implícita**: los parámetros `gamma`, `lambda` y `alpha` se dejan por defecto, pero la penalización por complejidad ya está activa.

---

## 📊 5. Evaluación del modelo

### 5.1. Métrica principal: Accuracy

La precisión global (porcentaje de aciertos) es la métrica principal. En el entrenamiento se obtiene una precisión en validación cruzada de aproximadamente **56-60%** (que es alta para predicción de fútbol, donde el azar es ~33%).

### 5.2. Matriz de confusión

Se puede analizar la matriz de confusión para ver si el modelo tiene sesgos (por ejemplo, subestimar empates). XGBoost maneja bien el desbalanceo de clases (históricamente menos empates) gracias a la función de pérdida log-loss.

### 5.3. Importancia de características

XGBoost proporciona automáticamente la **importancia de cada característica** (basada en la ganancia o en la frecuencia de uso). Esto permite interpretar qué variables influyen más en la predicción (por ejemplo, la diferencia de ranking FIFA o la eficiencia ofensiva).

---

## 🏆 6. ¿Por qué XGBoost para este problema?

1. **Rendimiento**: XGBoost suele ganar competiciones de machine learning por su alta precisión y velocidad.
2. **Manejo de datos tabulares**: Las características son numéricas y el número de muestras no es enorme; XGBoost es ideal para este tipo de datos.
3. **Interpretabilidad**: Aunque es un modelo de caja negra, la importancia de características y los árboles individuales permiten cierta interpretación.
4. **Regularización integrada**: Ayuda a evitar overfitting, crucial cuando el conjunto de datos históricos es limitado (solo partidos de mundiales).
5. **Escalabilidad**: Puede manejar características con diferentes escalas sin necesidad de normalización (aunque nosotros la aplicamos por buenas prácticas).
6. **Manejo de clases desbalanceadas**: La función log-loss no penaliza excesivamente las clases minoritarias (empates) y el modelo puede aprender patrones sutiles.

---

## 📈 7. Ajustes específicos para el fútbol

- **Selección de características**: Solo se incluyen estadísticas agregadas de los equipos (promedios), no datos de partido individuales, para generalizar mejor.
- **Ventaja de localía**: Se introduce como un factor fijo (`peso_local = 0.55`) porque en mundiales hay sedes neutrales, pero el público y el terreno pueden dar ligera ventaja.
- **Simulación Monte Carlo**: Una vez obtenidas las probabilidades de cada resultado con XGBoost, se utilizan para generar distribuciones de goles (Poisson) y simular múltiples escenarios, lo que enriquece el análisis con incertidumbre.

---

## 🔍 8. Limitaciones y posibles mejoras

- **Datos limitados**: Solo se dispone de partidos de Copas del Mundo pasadas; se podrían añadir partidos de eliminatorias o amistosos para aumentar la muestra.
- **Variables contextuales**: No se incluyen lesiones, estado de forma reciente, clima, etc.
- **Modelo alternativo**: Se podría probar con redes neuronales o Random Forest, aunque XGBoost suele ser superior en tabulares.
- **Calibración de probabilidades**: Las probabilidades devueltas por XGBoost pueden no estar perfectamente calibradas; se podría aplicar Platt Scaling o isotonic regression.

---

## 📚 9. Referencias

- Chen, T., & Guestrin, C. (2016). *XGBoost: A Scalable Tree Boosting System*. KDD.
- Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The Elements of Statistical Learning*. Springer.
- Documentación oficial de XGBoost: [https://xgboost.readthedocs.io/](https://xgboost.readthedocs.io/)

---

## 🧪 10. Conclusión

El modelo XGBoost ha demostrado ser una herramienta robusta y precisa para predecir resultados de partidos de fútbol en este contexto. Su capacidad para modelar interacciones complejas entre características, junto con la regularización y la optimización de hiperparámetros, permite obtener predicciones fiables. La combinación con simulaciones Monte Carlo añade un componente probabilístico que refleja la incertidumbre inherente al deporte.

---

