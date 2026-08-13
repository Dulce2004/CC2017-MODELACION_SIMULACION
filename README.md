# Laboratorio 3

**Curso:** CC2017 - Modelación y Simulación

**Integrantes:** 
- Dulce Ambrosio - 231143
- Javier Linares - 231135
- Nadissa Vela - 23764

## Descripción general
Este laboratorio se centra en la modelación de la dinámica de contagio usando el modelo SIR, con enfoque en la calibración, comparación con datos observados y análisis de sensibilidad del parámetro de transmisión $\beta$. El trabajo incluye una simulación numérica del avance de una epidemia y una herramienta interactiva para explorar cómo cambian las métricas clave según la variación de parámetros.

## Archivos del proyecto
- `Lab3.ipynb` — notebook principal con la implementación del modelo SIR, el método RK4, la calibración con datos reales y el análisis de sensibilidad.
- `simulacion_sir.html` — visualización interactiva del modelo SIR con sliders para modificar $R_0$, $\gamma$ y la fracción inicial infectada.

## Contenido desarrollado en Lab3.ipynb
1. Implementación del modelo SIR:
   - Definición de la población total, infectados iniciales, recuperados iniciales y susceptibles iniciales.
   - Ecuaciones diferenciales para $S(t)$, $I(t)$ y $R(t)$.
   - Parámetros $\beta$ (transmisión) y $\gamma$ (recuperación).

2. Simulación numérica con RK4:
   - Implementación manual del método de Runge-Kutta de cuarto orden.
   - Proyección diaria de la epidemia durante 28 días.
   - Comparación con datos observados en los días 7, 14, 21 y 28.

3. Cálculo del error de calibración:
   - Evaluación del ajuste del modelo mediante la suma de cuadrados del error (SCE).
   - Interpretación de qué tan bien aproxima el modelo la realidad observada.

4. Análisis de sensibilidad:
   - Variación del parámetro $\beta$ en $\pm 20\%$.
   - Evaluación del pico de infectados, el tiempo al pico y el tamaño final de la epidemia.
   - Cálculo del cambio porcentual en el pico frente a la variación de $\beta$.

5. Criterios teóricos aplicados:
   - Relación entre $R_0$ y la respuesta del sistema.
   - Uso del umbral de crecimiento/extinción de la epidemia.
   - Validación cualitativa y cuantitativa del modelo.

## Contenido desarrollado en simulacion_sir.html
1. Simulador interactivo del modelo SIR:
   - Control deslizante para $R_0$.
   - Control deslizante para el período infeccioso $1/\gamma$.
   - Control deslizante para la fracción inicial infectada $I(0)/N$.

2. Visualización de resultados:
   - Gráfica de susceptibles, infectados y recuperados a lo largo del tiempo.
   - Línea de capacidad hospitalaria para contextualizar el pico de infectados.
   - Métricas: valor actual de $R_0$, estado de crecimiento/extinción, umbral de inmunidad, pico máximo y tiempo al pico.

3. Interpretación visual:
   - Permite observar cómo cambian los resultados ante distintos supuestos epidemiológicos.
   - Facilita la comprensión del impacto de la transmisión y la duración infecciosa en la propagación.

## Cómo ejecutar Lab3.ipynb
1. Abrir el archivo `Lab3.ipynb` en Jupyter Notebook o VS Code con soporte para notebooks.
2. Asegurarse de tener instalado Python y las librerías necesarias, especialmente `numpy`.
3. Ejecutar las celdas en orden desde la primera hasta la última.
4. Se imprimirán los resultados de la simulación base y del análisis de sensibilidad.

## Cómo ejecutar simulacion_sir.html
1. Ubicar el archivo `simulacion_sir.html` en la carpeta del proyecto.
2. Abrirlo en un navegador web (Chrome, Edge, Firefox, etc.).
3. Ajustar los controles deslizantes para observar cómo cambia la dinámica de la epidemia.
4. La gráfica y las métricas se actualizan automáticamente en tiempo real.

## Requisitos
- Python 3.x
- Jupyter Notebook o VS Code con soporte de notebooks
- Navegador web moderno para abrir `simulacion_sir.html`
- Librería `numpy` para ejecutar el notebook
