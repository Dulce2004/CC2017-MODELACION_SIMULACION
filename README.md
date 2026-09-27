# Hoja 5 — Redes y dinámica de contagio

**Curso:** CC2017 - Modelación y Simulación

**Integrantes:**
- Dulce Ambrosio - 231143
- Javier Linares - 231135
- Nadissa Vela - 23764

## Descripción general

Este notebook implementa métricas de redes complejas y simula la propagación de una epidemia mediante el modelo SIR sobre diferentes topologías de red.

## Archivo principal

- `Hoja 5.ipynb` — notebook con la implementación de métricas, generación de redes y simulaciones SIR.

## Contenido desarrollado

### Task 1.3: Métricas de red

Se implementan las siguientes funciones:

- `grado(A)`: calcula el grado de cada nodo.
- `clustering(A)`: calcula el coeficiente de clustering local.
- `distancia_promedio(A)`: calcula la distancia geodésica promedio mediante BFS.

Las funciones se verifican utilizando una matriz de adyacencia definida en el notebook.

### Task 3.1: Generación y análisis de redes sintéticas

Se generan tres topologías utilizando NetworkX:

1. **Erdős-Rényi:** `N=500`, `p=0.02`.
2. **Barabási-Albert:** `N=500`, `m=5`.
3. **Watts-Strogatz:** `N=500`, `k=6`, `p=0.1`.

Para cada red se calculan:

- Grado promedio `⟨k⟩`.
- Segundo momento del grado `⟨k²⟩`.
- Coeficiente de clustering promedio `⟨C⟩`.
- Distancia promedio `⟨d⟩`.
- Umbral epidémico crítico.

También se grafica la distribución de grado `P(k)` para cada topología.

### Task 3.2: Simulación SIR

Se simula la propagación de una epidemia sobre las tres redes con los siguientes parámetros:

- Probabilidad de transmisión: `β = 0.04`.
- Probabilidad de recuperación: `γ = 0.03`.
- Infectados iniciales: `5`.
- Número de realizaciones: `50`.
- Tamaño de la red: `N = 500`.

Se reportan:

- Tamaño final promedio del brote.
- Intervalo de confianza del 95%.
- Trayectorias de la fracción de infectados `I(t)/N`.
- Comparación visual entre las distintas topologías.

## Cómo ejecutar el notebook

1. Abrir `Hoja 5.ipynb` en Jupyter Notebook o Visual Studio Code.
2. Instalar las dependencias requeridas.
3. Ejecutar las celdas en orden.
4. Revisar las métricas, tablas y gráficas generadas.

## Requisitos

- Python 3.x
- Jupyter Notebook o Visual Studio Code
- NumPy
- Pandas
- Matplotlib
- NetworkX

Para instalar las librerías:

```
pip install numpy pandas matplotlib networkx jupyter
```