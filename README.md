# Laboratorio 2

**Curso:** CC2017 - Modelación y Simulación

**Integrantes:** 
- Dulce Ambrosio - 231143
- Javier Linares - 231135
- Nadissa Vela - 23764

## Descripcion general
Este laboratorio realiza un análisis de Monte Carlo para evaluar la probabilidad de estabilidad de un sistema de reorden. Se muestrean incertidumbres en parámetros clave, se calcula el parámetro de estabilidad $P=\alpha\cdot\tau$, y se interpreta la robustez del sistema respecto al umbral $\pi/2$.

## Contenido desarrollado
1. Implementación Monte Carlo:
	- Definición de distribuciones para `alpha` (uniforme) y `tau` (normal truncada).
	- Generación de `N = 5000` muestras y cálculo de $P = \alpha\cdot\tau$.

2. Análisis estadístico y visual:
	- Histograma del producto $\alpha\cdot\tau$ y sombreado de regiones estable/inestable según $\pi/2$.
	- Cálculo de la probabilidad de estabilidad y su intervalo de confianza (95%).

3. Análisis de sensibilidad:
	- Correlaciones entre `alpha`, `tau` y $P$ para identificar variables influyentes.

4. Interpretación y conclusiones:
	- Evaluación del margen de seguridad y robustez frente a incertidumbres.

## Archivo principal
- Lab2.ipynb — Notebook del Laboratorio 2: Análisis de Monte Carlo para evaluar la probabilidad de estabilidad de un sistema de reorden. Incluye muestreo de parámetros (`alpha` uniforme, `tau` normal truncada), cálculo del parámetro de estabilidad $P=\alpha\cdot\tau$, visualización del histograma con el umbral $\pi/2$, cálculo de correlaciones y un intervalo de confianza para la proporción estable.