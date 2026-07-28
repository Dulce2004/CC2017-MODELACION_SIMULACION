# Laboratorio 1

**Curso:** CC2017 - Modelación y Simulación

**Integrantes:** 
- Dulce Ambrosio - 231143
- Javier Linares - 231135
- Nadissa Vela - 23764

## Descripcion general
Este laboratorio implementa y analiza un modelo dinamico de adopcion usando ecuaciones diferenciales ordinarias (EDOs), con integracion numerica por Euler y Runge-Kutta de cuarto orden (RK4).

## Contenido desarrollado
1. Implementacion del sistema en Python:
	- Definicion de parametros del modelo y condiciones iniciales.
	- Funcion de derivadas para los stocks S, A y R.
	- Implementacion manual de los metodos de Euler y RK4.

2. Corridas de simulacion y comparacion de metodos:
	- Ejecucion de Euler con pasos dt = 1.0, 0.5 y 0.1.
	- Ejecucion de RK4 con dt = 1.0.
	- Comparacion del valor final A(T) para evaluar precision.

3. Verificacion de conservacion de la poblacion:
	- Comprobacion numerica de la invariante S + A + R = N.
	- Cuantificacion del error maximo de redondeo en punto flotante.

4. Conclusiones:
	- RK4 ofrece mayor precision que Euler con pasos de tiempo grandes.
	- El tamano del paso influye directamente en el error numerico.
	- La validacion de invariantes es clave para asegurar consistencia del modelo.

## Archivo principal
- Lab1.ipynb