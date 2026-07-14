Mounted at /content/drive
🏆 PREDICCIÓN DE CLASIFICADOS A SEMIFINALES (CUARTOS DE FINAL)
================================================================================

✅ Archivos cargados correctamente.
✅ Nombres normalizados.
📊 Estadísticas de equipos listas.
🔄 Cargando modelo y scaler guardados...
✅ Modelo y scaler cargados correctamente.
✅ Modelo XGBoost listo.

================================================================================
📊 PREDICCIONES DETERMINISTAS - CUARTOS DE FINAL
================================================================================

📋 TABLA DE PREDICCIONES DETERMINISTAS - CUARTOS
    Local  Visitante  Prob_Local  Prob_Empate  Prob_Visitante  xG_Local  xG_Visitante  Goles_Local  Goles_Visitante    Ganador
  Francia  Marruecos       0.819        0.064           0.117      2.38          2.08            3                2    Francia
   España    Bélgica       0.906        0.070           0.024      2.65          1.83            3                2     España
  Noruega Inglaterra       0.204        0.339           0.457      1.96          2.34            2                3 Inglaterra
Argentina      Suiza       0.652        0.257           0.091      1.80          1.41            2                1  Argentina


🎯 CLASIFICADOS A SEMIFINALES (según el modelo determinista)
 1. Francia
 2. España
 3. Inglaterra
 4. Argentina

🔄 Ejecutando Monte Carlo (1000 iteraciones) para obtener SCORE por partido...

📊 SCORE POR PARTIDO (Monte Carlo) - Promedio de 1000 simulaciones
    Local  Visitante  Prob_Local  Prob_Empate  Prob_Visitante  Goles_Local_Prom  Goles_Visitante_Prom  Partidos_Simulados
Argentina      Suiza       0.679          0.0           0.321              2.73                  1.80                1000
   España    Bélgica       0.736          0.0           0.264              3.62                  2.28                1000
  Francia  Marruecos       0.619          0.0           0.381              3.39                  2.62                1000
  Noruega Inglaterra       0.380          0.0           0.620              2.60                  3.19                1000

📊 PROBABILIDAD DE CLASIFICACIÓN A SEMIFINALES (basada en Monte Carlo)
    Equipo  Prob_Clasificacion
    España               0.736
 Argentina               0.679
Inglaterra               0.620
   Francia               0.619
 Marruecos               0.381
   Noruega               0.380
     Suiza               0.321
   Bélgica               0.264

================================================================================
RESULTADOS FINALES
================================================================================

📌 CLASIFICADOS A SEMIFINALES (según modelo determinista)
 Posición     Equipo
        1    Francia
        2     España
        3 Inglaterra
        4  Argentina

📌 TABLA DE PREDICCIONES DETERMINISTAS
    Local  Visitante  Prob_Local  Prob_Empate  Prob_Visitante  xG_Local  xG_Visitante  Goles_Local  Goles_Visitante    Ganador
  Francia  Marruecos       0.819        0.064           0.117      2.38          2.08            3                2    Francia
   España    Bélgica       0.906        0.070           0.024      2.65          1.83            3                2     España
  Noruega Inglaterra       0.204        0.339           0.457      1.96          2.34            2                3 Inglaterra
Argentina      Suiza       0.652        0.257           0.091      1.80          1.41            2                1  Argentina

📌 SCORE POR PARTIDO (Monte Carlo)
    Local  Visitante  Prob_Local  Prob_Empate  Prob_Visitante  Goles_Local_Prom  Goles_Visitante_Prom  Partidos_Simulados
Argentina      Suiza       0.679          0.0           0.321              2.73                  1.80                1000
   España    Bélgica       0.736          0.0           0.264              3.62                  2.28                1000
  Francia  Marruecos       0.619          0.0           0.381              3.39                  2.62                1000
  Noruega Inglaterra       0.380          0.0           0.620              2.60                  3.19                1000

📌 PROBABILIDAD DE CLASIFICACIÓN A SEMIFINALES (Monte Carlo)
    Equipo  Prob_Clasificacion
    España               0.736
 Argentina               0.679
Inglaterra               0.620
   Francia               0.619
 Marruecos               0.381
   Noruega               0.380
     Suiza               0.321
   Bélgica               0.264

✅ Análisis completado.
   - Modelo: XGBoost con ajuste de hiperparámetros
   - Predicciones deterministas con goles enteros
   - Score Monte Carlo por partido: promedios de probabilidades y goles
   - Simulación: 1000 iteraciones
   - Modelo guardado para reutilización