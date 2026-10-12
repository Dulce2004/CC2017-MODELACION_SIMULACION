# Hoja 6 — Espacio de estados, equilibrios y estabilidad

**Curso:** CC2017 - Modelación y Simulación  
**Notebook principal:** [`Hoja 6.ipynb`](./Hoja%206.ipynb)

## Descripción

Esta hoja estudia un sistema dinámico no lineal de competencia entre dos
plataformas. El modelo representa la evolución de los usuarios de las
plataformas A y B mediante las variables de estado `x` y `y`:

```text
dx/dt = r1*x*(1 - x - alpha12*y)
dy/dt = r2*y*(1 - y - alpha21*x)
```

El trabajo conecta el análisis matemático del espacio de estados con
simulaciones numéricas. Se calculan equilibrios, se determina su estabilidad
mediante la matriz jacobiana y sus valores propios, y se comprueban las
predicciones con trayectorias generadas desde diferentes condiciones iniciales.

El notebook contiene comentarios que relacionan cada sección del código con
los contenidos de la presentación sobre trayectorias, equilibrios y
estabilidad.

## Parámetros del modelo

Para el Grupo 1 se utilizan:

- `r1 = 1.0`: tasa de crecimiento de la plataforma A.
- `r2 = 0.5`: tasa de crecimiento de la plataforma B.
- `alpha12 = 0.5`: efecto de B sobre A.
- `alpha21 = 0.6`: efecto de A sobre B.

Los equilibrios analizados son:

- `E1 = (0, 0)`: ausencia de usuarios en ambas plataformas.
- `E2 = (0, 1)`: exclusión de A.
- `E3 = (1, 0)`: exclusión de B.
- `E4 = (5/7, 4/7)`: equilibrio interior de coexistencia.

## Contenido de la hoja

### 1. Cálculo de equilibrios

Se calculan los parámetros del grupo y las coordenadas de los cuatro
equilibrios del sistema. También se verifica la factibilidad biológica del
equilibrio interior, comprobando que sus coordenadas sean positivas.

### 2. Jacobiana y clasificación de equilibrios

Para cada equilibrio se evalúa la matriz jacobiana:

```text
J(x, y) = [ df1/dx  df1/dy ]
          [ df2/dx  df2/dy ]
```

Con la traza, el determinante, el discriminante y los valores propios se
clasifica cada equilibrio como:

- Nodo estable.
- Nodo inestable.
- Punto silla.
- Foco estable o inestable.
- Centro.
- Caso frontera cuando el determinante es cero.

También se construye el plano traza-determinante, incluyendo la curva
`tau^2 = 4*Delta` que separa nodos y focos.

### 3. Predicción de convergencia

Se definen cuatro estados iniciales:

- `P1 = (0.05, 0.05)`.
- `P2 = (0.80, 0.30)`.
- `P3 = (0.30, 0.80)`.
- `P4 = (0.60, 0.60)`.

Para cada uno se estudia hacia cuál equilibrio converge la trayectoria del
sistema.

### 4. Integradores Euler y Runge-Kutta

Se implementan desde cero los métodos de:

- Euler.
- Runge-Kutta de cuarto orden (RK4).

Los resultados se comparan con una solución de referencia calculada mediante
`solve_ivp` con el método `DOP853`. Se mide el error global para distintos
tamaños de paso y se grafica el error en escala log-log para estimar el orden
de convergencia de cada integrador.

### 5. Retrato de fases

Se construye un retrato de fases en el cuadrante
`[0, 1.5] x [0, 1.5]`, incluyendo:

- Campo vectorial normalizado.
- Nulclinas de `x` y `y`.
- Equilibrios del sistema.
- Más de doce trayectorias desde distintos estados iniciales.
- Trayectorias destacadas de `P1`, `P2`, `P3` y `P4`.

Esta visualización permite comparar el comportamiento observado con la
clasificación de estabilidad obtenida mediante la jacobiana.

### 6. Cuencas de atracción

Se simula una malla de `60 x 60` estados iniciales. Cada punto se clasifica
según el equilibrio al que converge después de la integración con RK4.

El resultado es un mapa de cuencas de atracción que muestra qué regiones del
espacio de estados conducen a cada equilibrio y permite calcular la fracción
del dominio que pertenece a la cuenca del equilibrio interior `E4`.

### 7. Perturbaciones y estabilidad numérica

Se aplican perturbaciones pequeñas en ocho direcciones alrededor de `E4`.
Las tasas de decaimiento observadas se comparan con las tasas predichas por
los valores propios de la jacobiana.

Además, se utiliza una búsqueda por bisección para estimar el paso máximo
`h_max` con el que Euler conserva la convergencia. Esto permite observar que un
paso demasiado grande puede producir inestabilidad numérica aunque el
equilibrio del sistema continuo sea estable.

### 8. Cambio de régimen por rivalidad

Se modifica el parámetro `alpha21` para comparar:

- Un régimen de coexistencia.
- Un régimen de exclusión de la plataforma B.

El análisis muestra cómo una variación de la rivalidad puede cambiar
cualitativamente el destino del sistema mediante una bifurcación transcrítica.

### 9. Histéresis en un modelo de lago

Se estudia un modelo escalar de concentración de nutrientes:

```text
dx/dt = a - b*x + x^2/(x^2 + 1)
```

Se encuentran numéricamente los puntos donde `g'(x) = 0`, se identifican las
cargas críticas de colapso y recuperación, y se construye el diagrama de
equilibrios con forma de S.

Las simulaciones deterministas aumentan y disminuyen lentamente la carga
externa para mostrar:

- Estado estable de aguas claras.
- Estado estable de aguas turbias.
- Rama inestable entre ambos estados.
- Colapso.
- Recuperación.
- Histéresis, donde el camino de regreso no coincide con el camino de caída.

### 10. Simulación estocástica y alertas tempranas

Se utiliza Euler-Maruyama para agregar ruido al modelo del lago mientras la
carga de nutrientes aumenta gradualmente. Se calculan indicadores de alerta
temprana mediante:

- Varianza móvil.
- Autocorrelación de retardo uno.
- Detrendización mediante media móvil.

Finalmente se realizan 100 simulaciones en dos escenarios:

1. Carga dinámica que se acerca al umbral de colapso.
2. Carga estática utilizada como control para medir falsas alarmas.

La prueba de tendencia se realiza mediante el tau de Kendall para evaluar si
la varianza y la autocorrelación aumentan significativamente antes del cambio
de régimen.

## Requisitos

- Python 3.x.
- Jupyter Notebook o Visual Studio Code con soporte para notebooks.
- NumPy.
- SciPy.
- Matplotlib.
- Pandas.

Instalación:

```bash
pip install numpy scipy matplotlib pandas jupyter
```

En una celda de Jupyter también puede utilizarse:

```python
%pip install numpy scipy matplotlib pandas
```

## Ejecución

1. Abrir [`Hoja 6.ipynb`](./Hoja%206.ipynb) en Jupyter o Visual Studio Code.
2. Seleccionar un entorno de Python con las dependencias instaladas.
3. Ejecutar las celdas en orden.
4. Revisar los valores de los equilibrios, las clasificaciones de estabilidad
   y los errores de los integradores.
5. Analizar los retratos de fase, el plano traza-determinante y las cuencas
   de atracción.
6. Revisar las gráficas de bifurcación, histéresis y alertas tempranas.
