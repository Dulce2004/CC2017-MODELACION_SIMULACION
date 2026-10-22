# Lab 6 — Modelado híbrido y sincronización

**Curso:** CC2017 - Modelación y Simulación  
**Notebook:** [`Lab 6.ipynb`](./Lab%206.ipynb)

## Descripción

Este laboratorio implementa y verifica un modelo híbrido que combina:

- **System Dynamics (SD):** evolución diaria de los usuarios activos de una
  plataforma de video.
- **Discrete Event Simulation (DES):** llegadas, colas, servicios, latencias y
  rechazos de solicitudes en un conjunto de servidores.
- **Política de autoescalado:** incorporación de servidores cuando la
  utilización prevista supera un umbral.

El notebook relaciona la implementación con las presentaciones:

- **S15 - DES e Hbridos P1:** entidades, colas, recursos, procesos de llegada y
  servicio, teoría M/M/c, ley de Little y verificación de simulaciones.
- **S16 - DES e Hbridos P2:** modelado híbrido, retroalimentación, interfaces
  entre tasas y entidades, sincronización de relojes y ventanas de
  intercambio.

## Contenido del notebook

### Task 1.3 — Línea base del modelo híbrido

Se implementa una primera versión del modelo acoplado:

- La capa DES simula una cola M/M/c/K durante ventanas de tiempo en segundos.
- La tasa de llegada depende del número de usuarios activos:
  `lambda = a * U`.
- La latencia promedio `W` y la fracción de rechazo `r` alimentan la capa SD.
- La capa SD actualiza los usuarios mediante una ecuación diferencial
  discretizada con Euler.
- Se solicitan dos servidores cuando la utilización prevista supera
  `theta = 0.7`; los servidores llegan después de un retardo `D = 3` días.

### Task 2.1 — Verificación aislada de la capa DES

Se verifica el simulador de eventos discretos bajo diferentes condiciones:

1. Cola M/M/4 estable, con comparación de `W`, `Wq` y `rho` contra la teoría.
2. Cola M/M/c/K sobrecargada, con medición de la fracción rechazada.
3. Ley de Little, comparando el número promedio de entidades medido
   directamente con `L = lambda_efectiva * W`.

Se utilizan réplicas independientes, periodo de calentamiento e intervalos
de confianza para evaluar los resultados de la simulación.

### Task 2.2 — Verificación aislada de la capa SD

Se estudia la ecuación diferencial de usuarios activos con abandono constante:

```text
dU/dt = (p + q * (U/M)) * (M - U) - delta_0 * U
```

La implementación compara:

- Método de Euler.
- Método de Runge-Kutta de cuarto orden (RK4).
- Solución de referencia de `scipy.integrate.solve_ivp`.

También se analiza cómo disminuye el error al reducir el paso temporal y se
selecciona un paso adecuado para el acoplamiento con DES.

### Task 2.3 — Eventos de estado y política de autoescalado

Se compara una detección ingenua de eventos con una detección más precisa:

- Cruce del umbral de utilización prevista.
- Búsqueda del instante del evento mediante bisección.
- Programación de la llegada de servidores después del retardo `D`.
- Reordenamiento de la política cuando llegan nuevos servidores.

El objetivo es sincronizar correctamente los eventos discretos con la
evolución continua de la capa SD.

### Task 2.4 — Verificación de la interfaz entre capas

Se valida la comunicación entre SD y DES mediante:

- Verificación estadística de llegadas Poisson.
- Conservación de entidades en cada ventana de simulación.
- Balance:

```text
llegadas = terminadas + entidades_en_sistema + rechazadas
```

Esta comprobación garantiza que las solicitudes no desaparezcan durante el
acoplamiento.

### Task 3.1 — Dependencia del tamaño de la ventana de intercambio

Se evalúan diferentes tamaños de ventana `H`:

```text
H = [0.25, 0.5, 1, 2, 4, 7] días
```

Para cada valor se ejecutan réplicas del modelo híbrido y se calculan:

- Usuarios finales `U(100)`.
- Latencia máxima.
- Error cuadrático medio (RMSE) de la trayectoria de usuarios.
- Intervalos de confianza de las métricas.

El caso `H = 0.25` se utiliza como referencia para estudiar el efecto de la
frecuencia de sincronización. Una ventana pequeña suele representar mejor el
acoplamiento, pero requiere más intercambios y tiempo de ejecución.

## Requisitos

- Python 3.x.
- Jupyter Notebook o Visual Studio Code con soporte para notebooks.
- NumPy.
- SimPy.
- SciPy.
- Matplotlib.

Las librerías pueden instalarse con:

```bash
pip install numpy simpy scipy matplotlib jupyter
```

## Ejecución

1. Abrir [`Lab 6.ipynb`](./Lab%206.ipynb) en Jupyter o Visual Studio Code.
2. Seleccionar un entorno de Python con las dependencias instaladas.
3. Ejecutar las celdas en orden.
4. Revisar las comparaciones entre teoría y simulación de la capa DES.
5. Analizar los errores de Euler y RK4 en la capa SD.
6. Comparar la detección de eventos y la política de autoescalado.
7. Revisar la conservación de entidades en la interfaz SD-DES.
8. Analizar el efecto del tamaño de ventana `H` mediante la tabla de
   resultados y la gráfica RMSE.

> La ejecución de `Task 3.1` puede tardar varios minutos porque ejecuta
> múltiples réplicas del modelo híbrido para cada tamaño de ventana.
