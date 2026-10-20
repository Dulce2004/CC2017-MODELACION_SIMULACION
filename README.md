# Hoja 7 — Simulación de eventos discretos y teoría de colas (UCI)

**Curso:** CC2017 - Modelación y Simulación  
**Notebook principal:** [`Hoja 7.ipynb`](./Hoja%207.ipynb)

## Descripción

Modelo de las camas de cuidados intensivos del Hospital Regional del
Altiplano, con simulación de eventos discretos validada contra la teoría de
colas. Se estudian dos variantes: con espera (M/M/c) y sin espera (M/M/c/c).

Parámetros del Grupo 1: `λ = 3.0`, `μ = 0.25`, `c = 17`, `a = 12`,
`ρ ≈ 0.706`, `k_off = 8`.

## Contenido

- **Task 1:** desempeño teórico (Erlang B y C, ley de Little), simulador base
  generado por IA, auditoría y corrección con siete criterios, y validación
  con 30 réplicas e intervalos de confianza.
- **Task 2:** predicciones (Allen-Cunneen, recuperación tras el cierre de
  camas, Erlang B con estancia +25 %), estancias determinista, exponencial y
  lognormal, cierre parcial de camas y balance de predicciones.
- **Task 3:** camas mínimas por meta, robustez en tres escenarios y
  protección durante el cierre de camas. La recomendación es operar sin espera
  con 19 camas.
- **Task 4:** epidemia SIR acoplada al hospital con llegadas por
  adelgazamiento y camas de contingencia.

Las conclusiones de los Tasks 3.2 y 3.3 están en el documento PDF de entrega.

## Requisitos y ejecución

Python 3 con `numpy`, `scipy`, `matplotlib` y `jupyter`:

```bash
pip install numpy scipy matplotlib jupyter
```

Abrir `Hoja 7.ipynb` y ejecutar las celdas en orden. Las simulaciones largas
(Tasks 1.4, 3.1b) tardan varios minutos.
