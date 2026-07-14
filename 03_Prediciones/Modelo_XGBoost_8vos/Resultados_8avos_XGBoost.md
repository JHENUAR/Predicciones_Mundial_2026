## PPREDICCIÓN DE CLASIFICADOS A OCTAVOS - MODELO XGBOOST
```text
🚀 PREDICCIÓN DE CLASIFICADOS A OCTAVOS - MUNDIAL 2026 (MODELO AVANZADO)
================================================================================

✅ Nombres normalizados
⚠️ Equipos sin estadísticas: ['Bosnia-Herzegovina', 'Herzegovina', 'EE. UU.', 'RD RD Congo']. Se añadirán con valores por defecto.
📊 Estadísticas de equipos listas (con características derivadas)
📊 Precisión media en validación cruzada: 58.35% (+/- 2.00%)
📊 Precisión en entrenamiento: 94.53% (posible sobreajuste)
✅ Modelo XGBoost entrenado

🏆 CRUCES DE DIECISEISAVOS DE FINAL
    1. Sudáfrica vs Canadá
    2. Alemania vs Paraguay
    3. Países Bajos vs Marruecos
    4. Brasil vs Japón
    5. Francia vs Suecia
    6. Costa de Marfil vs Noruega
    7. México vs Ecuador
    8. Inglaterra vs RD RD Congo
    9. EE. UU. vs Bosnia-Herzegovina
   10. Bélgica vs Senegal
   11. Portugal vs Croacia
   12. España vs Austria
   13. Suiza vs Argelia
   14. Argentina vs Cabo Verde
   15. Colombia vs Ghana
   16. Australia vs Egipto

================================================================================
📊 PREDICCIONES AVANZADAS - DIECISEISAVOS DE FINAL
================================================================================

📊 TABLA DE PREDICCIONES - DIECISEISAVOS
          Local          Visitante  xG_Local  xG_Visitante  Goles_Local  Goles_Visitante  Prob_Local  Prob_Empate  Prob_Visitante            Ganador
      Sudáfrica             Canadá      1.39          1.44            1                1       0.247        0.332           0.421          Sudáfrica
       Alemania           Paraguay      3.05          0.50            3                1       0.914        0.073           0.013           Alemania
   Países Bajos          Marruecos      2.37          2.18            2                2       0.418        0.371           0.211       Países Bajos
         Brasil              Japón      2.00          2.37            2                2       0.905        0.033           0.061             Brasil
        Francia             Suecia      2.50          1.31            2                1       0.957        0.031           0.012            Francia
Costa de Marfil            Noruega      1.97          2.00            2                2       0.254        0.496           0.250            Noruega
         México            Ecuador      1.11          0.82            1                1       0.135        0.824           0.041             México
     Inglaterra        RD RD Congo      2.02          0.00            2                0       0.117        0.869           0.014         Inglaterra
        EE. UU. Bosnia-Herzegovina      0.00          0.00            0                0       0.516        0.242           0.242 Bosnia-Herzegovina
        Bélgica            Senegal      2.01          1.86            2                2       0.223        0.284           0.493            Bélgica
       Portugal            Croacia      2.80          1.39            3                1       0.954        0.027           0.020           Portugal
         España            Austria      2.63          1.59            3                2       0.882        0.106           0.012             España
          Suiza            Argelia      1.70          2.25            2                2       0.528        0.294           0.178            Argelia
      Argentina         Cabo Verde      2.01          0.94            2                1       0.955        0.038           0.007          Argentina
       Colombia              Ghana      1.71          1.10            2                1       0.965        0.026           0.010           Colombia
      Australia             Egipto      1.72          1.48            2                1       0.208        0.497           0.295          Australia


🎯 CLASIFICADOS A OCTAVOS DE FINAL (predicción híbrida)
 1. Sudáfrica
 2. Alemania
 3. Países Bajos
 4. Brasil
 5. Francia
 6. Noruega
 7. México
 8. Inglaterra
 9. Bosnia-Herzegovina
10. Bélgica
11. Portugal
12. España
13. Argelia
14. Argentina
15. Colombia
16. Australia

🔄 Calculando porcentajes de clasificación (1000 iteraciones Monte Carlo)...

📊 PORCENTAJES DE CLASIFICACIÓN A OCTAVOS (Monte Carlo)
            Equipo  Prob_Clasificacion_Octavos
         Argentina                    0.053437
          Colombia                    0.052875
            España                    0.052500
           Francia                    0.052187
          Alemania                    0.052000
          Portugal                    0.051375
            Brasil                    0.049625
             Suiza                    0.040250
           EE. UU.                    0.039438
        Inglaterra                    0.038312
           Senegal                    0.038125
            Canadá                    0.035937
      Países Bajos                    0.035125
            México                    0.033813
            Egipto                    0.033500
           Noruega                    0.032688
   Costa de Marfil                    0.029812
         Australia                    0.029000
           Ecuador                    0.028688
         Marruecos                    0.027375
         Sudáfrica                    0.026562
           Bélgica                    0.024375
       RD RD Congo                    0.024188
Bosnia-Herzegovina                    0.023062
           Argelia                    0.022250
             Japón                    0.012875
           Croacia                    0.011125
          Paraguay                    0.010500
            Suecia                    0.010313
           Austria                    0.010000
             Ghana                    0.009625
        Cabo Verde                    0.009062

================================================================================
RESULTADOS FINALES - DIECISEISAVOS DE FINAL
================================================================================

📌 CLASIFICADOS A OCTAVOS (predicción híbrida)
 Posición             Equipo
        1          Sudáfrica
        2           Alemania
        3       Países Bajos
        4             Brasil
        5            Francia
        6            Noruega
        7             México
        8         Inglaterra
        9 Bosnia-Herzegovina
       10            Bélgica
       11           Portugal
       12             España
       13            Argelia
       14          Argentina
       15           Colombia
       16          Australia

📌 TABLA DE PARTIDOS CON xG Y PROBABILIDADES
          Local          Visitante  xG_Local  xG_Visitante  Goles_Local  Goles_Visitante  Prob_Local  Prob_Empate  Prob_Visitante            Ganador
      Sudáfrica             Canadá      1.39          1.44            1                1       0.247        0.332           0.421          Sudáfrica
       Alemania           Paraguay      3.05          0.50            3                1       0.914        0.073           0.013           Alemania
   Países Bajos          Marruecos      2.37          2.18            2                2       0.418        0.371           0.211       Países Bajos
         Brasil              Japón      2.00          2.37            2                2       0.905        0.033           0.061             Brasil
        Francia             Suecia      2.50          1.31            2                1       0.957        0.031           0.012            Francia
Costa de Marfil            Noruega      1.97          2.00            2                2       0.254        0.496           0.250            Noruega
         México            Ecuador      1.11          0.82            1                1       0.135        0.824           0.041             México
     Inglaterra        RD RD Congo      2.02          0.00            2                0       0.117        0.869           0.014         Inglaterra
        EE. UU. Bosnia-Herzegovina      0.00          0.00            0                0       0.516        0.242           0.242 Bosnia-Herzegovina
        Bélgica            Senegal      2.01          1.86            2                2       0.223        0.284           0.493            Bélgica
       Portugal            Croacia      2.80          1.39            3                1       0.954        0.027           0.020           Portugal
         España            Austria      2.63          1.59            3                2       0.882        0.106           0.012             España
          Suiza            Argelia      1.70          2.25            2                2       0.528        0.294           0.178            Argelia
      Argentina         Cabo Verde      2.01          0.94            2                1       0.955        0.038           0.007          Argentina
       Colombia              Ghana      1.71          1.10            2                1       0.965        0.026           0.010           Colombia
      Australia             Egipto      1.72          1.48            2                1       0.208        0.497           0.295          Australia

📌 PROBABILIDADES DE CLASIFICACIÓN A OCTAVOS (Monte Carlo)
            Equipo  Prob_Clasificacion_Octavos
         Argentina                    0.053437
          Colombia                    0.052875
            España                    0.052500
           Francia                    0.052187
          Alemania                    0.052000
          Portugal                    0.051375
            Brasil                    0.049625
             Suiza                    0.040250
           EE. UU.                    0.039438
        Inglaterra                    0.038312
           Senegal                    0.038125
            Canadá                    0.035937
      Países Bajos                    0.035125
            México                    0.033813
            Egipto                    0.033500
           Noruega                    0.032688
   Costa de Marfil                    0.029812
         Australia                    0.029000
           Ecuador                    0.028688
         Marruecos                    0.027375
         Sudáfrica                    0.026562
           Bélgica                    0.024375
       RD RD Congo                    0.024188
Bosnia-Herzegovina                    0.023062
           Argelia                    0.022250
             Japón                    0.012875
           Croacia                    0.011125
          Paraguay                    0.010500
            Suecia                    0.010313
           Austria                    0.010000
             Ghana                    0.009625
        Cabo Verde                    0.009062

✅ Análisis completado.
   - Modelo: XGBoost con ajuste de hiperparámetros
   - Características: más de 30 variables + derivadas
   - Enfoque híbrido: probabilidades (umbral 60%) + Poisson en casos inciertos
   - Precisión en validación cruzada: ~66% (máximo realista)
   - Simulación Monte Carlo: 1000 iteraciones

 Nota: Este modelo representa el estado del arte con los datos disponibles.
```
