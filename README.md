**My First Data Cleaning**

Este proyecto consiste en la limpieza y preparación de una base de datos de coches para análisis y modelado. La tarea fue asignada por Nuclio Digital School-Barcelona, donde actualmente curso el Máster en Ciencia de Datos.

*1. Objetivo del Proyecto*
Preparar una base de datos de automóviles para futuros análisis, asegurando la calidad y consistencia de los datos mediante técnicas de limpieza, manejo de valores nulos, codificación y normalización.

2. Principales tareas realizadas
Tratamiento de valores nulos
Codificación de variables categóricas (One Hot Encoding)
Conversión de variables booleanas a numéricas
Normalización de datos (Min-Max Scaling)
Eliminación de filas duplicadas
3. Detalles del proceso de limpieza
3.1 Columnas eliminadas
asientos_traseros_plegables (70.02% de nulos)
marca (valor repetitivo)
fecha_registro (más del 50% de nulos)
3.2 Manejo de valores nulos
modelo, km, potencia, tipo_gasolina, volante_regulable, camara_trasera, elevalunas_electrico, precio, fecha_venta: Porcentaje bajo de nulos, se eliminaron las filas correspondientes.
color (10% de nulos): Imputado como "desconocido".
tipo_coche (30% de nulos): Imputado como "desconocido".
aire_acondicionado, alerta_lim_velocidad: Imputados como "desconocido" (entre 10%-30% de nulos).
bluetooth: Convertida a booleana, nulos imputados como False.
gps: Sin nulos.
4. Análisis univariable
Modelo: Agrupación en tres listas, indexación con pandas.
Color: Agrupación y nulos imputados como "desconocido" por su impacto en el precio.
Tipo de coche: Agrupación y nulos imputados como "desconocido".
Tipo de gasolina: Simplificación a dos categorías principales ("diésel" y "petrol").
5. Análisis de correlación inicial
Precio vs Potencia (+0.645): Los autos más potentes son más caros.
Cámara trasera (+0.256): Autos con cámara trasera suelen tener precios más altos.
Elevalunas eléctrico (+0.266): Relación positiva con el precio.
Alerta de límite de velocidad (+0.387): Relación positiva con el precio.
Kilometraje (-0.408): Más kilómetros, menor precio.
Aire acondicionado (+0.288): Presente en modelos avanzados.
Volante regulable (+0.326): Relación con potencia y precio.
Bluetooth (+0.204) y GPS (+0.155): Relación baja con el precio.
Fecha de venta: Menor correlación con el precio.
6. Análisis variable vs target (precio)
Modelo: Alta demanda = precios más caros y variables; baja demanda = precios estables.
Tipo coche: Categoría "desconocido" incluida para mantener la información.
Color: Colores vivos = precios más altos; colores claros = precios más bajos y consistentes; "desconocido" para no perder datos.
7. Transformación de variables
Categóricas a numéricas:

One-hot encoding (get_dummies()) para modelo, color, tipo_coche, gasolina.
Transformación con .astype() para aire_acondicionado, camara_trasera, elevalunas_electrico, alerta_lim_velocidad.
Normalización/Escalado:

MinMaxScaler aplicado a variables numéricas relevantes.
Eliminación de variables redundantes (ej. gasolina diésel, modelo media demanda).
Correlaciones relevantes observadas entre precio y potencia, alerta de límite de velocidad y log(precio).
8. Resumen
Se ha creado la categoría "desconocido" para los valores nulos en color y tipo de coche, manteniendo así la mayor cantidad de información posible para futuros análisis y modelos.

Autor:
Sara Blanz
Nuclio Digital School - Máster en Ciencia de Datos
