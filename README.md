# Laboratorio 4

**Curso:** CC2017 - Modelación y Simulación

**Integrantes:**
- Dulce Ambrosio - 231143
- Javier Linares - 231135
- Nadissa Vela - 23764

## Descripción general
Este laboratorio se centra en la construcción de un modelo de simulación basado en agentes (ABM) en Mesa para evaluar si una política de bicicletas compartidas reduce la congestión vehicular en una cuadrícula urbana. El trabajo cubre la inicialización de agentes heterogéneos con una distribución normal multivariada, el diseño del scheduler y la comunicación por entorno.

## Archivos del proyecto
- `Lab4.ipynb` — notebook principal con la implementación del modelo ABM, las pruebas de verificación, el análisis estadístico de la política de bicicletas.

## Contenido desarrollado en Lab4.ipynb

1. Infraestructura del modelo ABM:
   - Definición de dos tipos de agentes: `CommutterAgent` (persona que se desplaza) y `VehicleAgent` (vehículo asociado).
   - Cuadrícula `MultiGrid` de 20×20 celdas que permite la coexistencia de una persona y su vehículo.
   - Scheduler `RandomActivation` (asíncrono aleatorio), justificado por la naturaleza descentralizada de la movilidad urbana.

2. Inicialización de agentes heterogéneos (Task 1.1):
   - Generación de $N=150$ agentes con ingreso y distancia correlacionados mediante una distribución normal multivariada.
   - Descomposición de Cholesky de la matriz de covarianza $\Sigma$ para muestrear atributos correlacionados.
   - Regla determinista de elección de modo de transporte (bicicleta vs. automóvil) según distancia y política activa.

3. Movilidad, comunicación y eliminación (Task 1.2):
   - Movimiento por el camino Manhattan más corto, con espera si la celda objetivo está ocupada.
   - Variable de entorno `congestion_map` que actúa como comunicación por entorno entre agentes.
   - Eliminación del agente y su vehículo al llegar al destino.

4. Pruebas de verificación (Task 1.3):
   - Prueba de scheduler: orden de activación y cobertura completa de agentes por paso.
   - Prueba de inicialización: consistencia de medias y desviaciones con los parámetros teóricos.
   - Prueba de conservación: decrecimiento monótono de agentes activos conforme llegan a destino.

5. Análisis estadístico de la política (Task 2):
   - Función `run_simulation(policy_active, seed)` para correr el modelo de forma reproducible.
   - 100 corridas por escenario (con y sin política), con semillas emparejadas.
   - Cálculo de media, desviación estándar, coeficiente de variación y número mínimo de corridas $M^*$.
   - Estimación bootstrap ($B=2000$) de la media, su error estándar y el intervalo de confianza del 95%.
   - Curva de convergencia del error estándar bootstrap en función del número de corridas.
   - Estimación de la diferencia $\Delta Y$ entre escenarios y su intervalo de confianza.



## Cómo ejecutar Lab4.ipynb
1. Abrir el archivo `Lab4.ipynb` en Jupyter Notebook o VS Code con soporte para notebooks.
2. Asegurarse de tener instalado Python y las librerías necesarias, especialmente `mesa==2.4.0`, `numpy` y `matplotlib`.
3. Ejecutar las celdas en orden desde la primera hasta la última.
4. Se imprimirán los resultados de las pruebas de verificación, el análisis estadístico y se mostrarán las gráficas correspondientes.



## Requisitos
- Python 3.x
- Jupyter Notebook o VS Code con soporte de notebooks
- Librerías `mesa==2.4.0`, `numpy` y `matplotlib` para ejecutar el notebook
