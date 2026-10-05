# Lab 5 — Modelado espacial y cobertura hospitalaria

**Curso:** CC2017 - Modelación y Simulación
**Notebook principal:** [`Lab 5.ipynb`](./Lab%205.ipynb)

## Integrantes

- Dulce Ambrosio — 231143
- Javier Linares — 231135
- Nadissa Vela — 23764

## Descripción

El laboratorio analiza la cobertura y accesibilidad de servicios hospitalarios
en California mediante datos espaciales reales. El notebook combina
GeoPandas, análisis geométrico y redes viales de OpenStreetMap para comparar
buffers circulares con isocronas basadas en tiempo de viaje.

El código contiene comentarios que relacionan cada etapa con los contenidos de
las presentaciones **S12 - Redes P1** y **S13 - Redes P2**.

## Datos utilizados

Los archivos deben estar en la carpeta `data/`:

- `hospitales_eeuu.geojson`: ubicación, tipo y capacidad de los hospitales.
- `condados_eeuu.geojson`: límites y códigos de los condados.
- `estados_eeuu.geojson`: límites estatales.
- `poblacion_condados.csv`: población por condado.

El análisis selecciona California mediante el código de estado FIPS `06` y
utiliza el CRS `EPSG:3310` (NAD83 / California Albers) para realizar cálculos
de distancias, áreas y buffers en metros.

## Contenido del laboratorio

### 1. Preparación y análisis base

- Carga y limpieza de archivos GeoJSON y CSV.
- Estandarización de identificadores FIPS.
- Filtrado de hospitales, condados y población de California.
- Reproyección de las capas espaciales.
- Mapa base con condados, hospitales y límite estatal.

### 2. Estadísticas hospitalarias por condado

Se calculan y reportan:

- Número de hospitales.
- Camas totales y camas UCI.
- Población total.
- Camas totales y camas UCI por cada 10,000 habitantes.
- Distribuciones de camas hospitalarias.

### 3. Análisis de cobertura mediante buffers

Se generan áreas de cobertura de **10 km, 25 km y 50 km** alrededor de los
hospitales. Luego se calcula la población cubierta y se clasifican los
condados según su cobertura espacial.

### 4. Distancia al hospital más cercano

Se calcula la distancia desde el centroide de cada condado hasta el hospital
más cercano y se construye una curva de cobertura acumulada. Esta aproximación
permite evaluar la sensibilidad de los resultados frente al uso de buffers
circulares.

### 5. Índice compuesto de vulnerabilidad

Se combinan tres componentes normalizados:

1. Distancia mínima al hospital.
2. Escasez de camas hospitalarias per cápita.
3. Ocupación hospitalaria promedio en un radio de 50 km.

El índice permite identificar los condados con mayor vulnerabilidad relativa.

### 6. Localización de cobertura máxima (MCLP)

Se implementa un algoritmo voraz para proponer la ubicación de tres nuevos
hospitales entre puntos candidatos separados por 50 km. El objetivo es
maximizar la población adicional cubierta dentro del radio definido.

### 7. Isocronas con OSMnx

Para los condados más vulnerables se descarga la red vial de OpenStreetMap y
se calculan isocronas de tiempo de viaje alrededor de hospitales. El análisis
compara:

- Cobertura geométrica mediante buffers.
- Cobertura basada en la red vial y el tiempo de viaje.

La descarga de la red requiere conexión a Internet y puede depender de la
disponibilidad temporal de los servicios de OpenStreetMap/Overpass.

## Requisitos

- Python 3.x
- Jupyter Notebook o Visual Studio Code
- GeoPandas
- Pandas
- NumPy
- Matplotlib
- Shapely
- NetworkX
- OSMnx
- Matplotlib Scalebar
- Mapclassify

Instalación:

```bash
pip install geopandas pandas numpy matplotlib shapely networkx osmnx matplotlib-scalebar mapclassify jupyter
```

En un notebook de Jupyter o VS Code también puede utilizarse:

```python
%pip install geopandas pandas numpy matplotlib shapely networkx osmnx matplotlib-scalebar mapclassify
```

## Ejecución

1. Verificar que los cuatro archivos de datos estén en `data/`.
2. Abrir [`Lab 5.ipynb`](./Lab%205.ipynb) en Jupyter o Visual Studio Code.
3. Seleccionar el entorno de Python donde se instalaron las dependencias.
4. Ejecutar las celdas en orden.
5. Revisar las tablas, mapas, métricas de cobertura, índice de vulnerabilidad,
   ubicaciones candidatas e isocronas generadas.
