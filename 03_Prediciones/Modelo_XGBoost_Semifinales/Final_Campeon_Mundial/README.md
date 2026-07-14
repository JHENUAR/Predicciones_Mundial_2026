**Predicción Final y Campeón Mundial**

Este módulo complementa el script principal de predicción de cuartos de final. Una vez que el modelo XGBoost ha clasificado a los cuatro equipos que pasan a semifinales (usando el código base), este script adicional realiza las siguientes funciones:

* Determina los emparejamientos de semifinales según el orden generado.
* Predice el ganador de cada semifinal y el de la final de forma determinista, mostrando marcador, xG y probabilidades.
* Simula 1000 veces toda la fase final (semifinales + final) mediante Monte Carlo para obtener:

  * Probabilidades de resultado de cada partido (local, empate, visitante).
  * Promedio de goles por partido.
  * Probabilidad de cada equipo de llegar a la final y de ganar el Mundial.
* Presenta los resultados en tablas con el mismo formato que las generadas para los cuartos de final, facilitando la comparación.

---

**📌 Requisitos previos**

Antes de ejecutar este código, asegúrate de haber ejecutado el script principal que:

* Carga y limpia los datos (Cruces_cuartos.csv, datos_historicos.csv, etc.).
* Entrena o carga el modelo XGBoost (best_model_xgb.pkl) y el escalador (scaler_xgb.pkl).
* Define las funciones `predict_winner`, `simular_partido`, `build_match_features` y otras auxiliares.
* Genera la lista `clasificados_semifinales` con los 4 equipos ganadores de los cuartos de final (en el orden de los cruces originales).

Este nuevo script reutiliza todas esas funciones y objetos, por lo que no es necesario duplicarlos.

---

**🔗 Conexión con el código base**

El script adicional está diseñado para ejecutarse inmediatamente después del código original, en el mismo entorno (por ejemplo, una celda de Google Colab o un script secuencial). Detecta automáticamente si las variables necesarias (`clasificados_semifinales`, `stats`, `best_model`, `scaler`) existen en la sesión.

En caso contrario (por ejemplo, si se ejecuta en una sesión nueva), intenta cargar el modelo y el scaler desde los archivos guardados en el directorio especificado y reconstruye `stats` a partir de los datos originales.

Esto garantiza que el módulo pueda ejecutarse de forma independiente o como continuación del flujo principal.

---

**⚙️ Flujo de ejecución**

1. **Verificación de variables**
   Si no se encuentran, se cargan desde los archivos `.pkl`.

2. **Definición de emparejamientos**
   Los 4 equipos de `clasificados_semifinales` se organizan en dos semifinales:

   * Semifinal 1: [0] vs [1]
   * Semifinal 2: [2] vs [3]

3. **Predicción determinista**
   Se llama a `predict_winner` para cada semifinal y luego para la final (cuyos participantes son los ganadores de las semifinales). Se almacenan los resultados (marcador, xG, probabilidades).

4. **Simulación Monte Carlo (partidos fijos)**
   Se simulan 1000 veces cada partido (semifinales y final) utilizando `simular_partido` y se calculan:

   * Probabilidad de victoria local, empate y visitante.
   * Goles promedio de cada equipo.

5. **Simulación Monte Carlo (fase completa)**
   Se simulan 1000 veces todas las eliminatorias (semifinales + final) para estimar:

   * Probabilidad de cada equipo de llegar a la final.
   * Probabilidad de cada equipo de ganar el Mundial.

6. **Salida de resultados**
   Se imprimen las tablas y el campeón determinista.

---

**📁 Archivos generados y dependencias**

* **Entrada:**
  Los mismos archivos CSV que el script base (Cruces_cuartos.csv, datos_historicos.csv, etc.) y los modelos guardados (best_model_xgb.pkl, scaler_xgb.pkl).

* **Salida:**
  Imprime en consola las tablas y resúmenes. No guarda archivos adicionales, pero puede adaptarse fácilmente para exportar a CSV o Markdown.

---

**🛠️ Personalización**

Puedes ajustar:

* `N_SIM = 1000`: Número de iteraciones de Monte Carlo (a mayor número, mayor precisión pero más tiempo).
* El orden de los emparejamientos de semifinales si deseas otro criterio (actualmente usa el orden de la lista `clasificados_semifinales`).
* Si prefieres no mostrar las probabilidades de finalistas o campeón, puedes comentar esa sección.

---

**📝 Notas importantes**

* El código asume que el modelo XGBoost ya ha sido entrenado y guardado en el directorio `base_path`. Si ejecutas el script sin haber generado previamente el modelo, se entrenará uno nuevo (si se incluye la lógica de entrenamiento del código base).
* Todas las funciones reutilizadas (`predict_winner`, `simular_partido`, etc.) deben estar definidas en el entorno antes de ejecutar este módulo.
* La simulación de los partidos fijos (tabla Monte Carlo) se realiza con los enfrentamientos deterministas de la final (ganadores de las semifinales), no con los ganadores variables de cada iteración. Esto es coherente con la tabla de cuartos, que también se calcula sobre los cruces fijos.
