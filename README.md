My first procesing consistió en limpiar una base de datos de coches, preparándola para futuros análisis. Las principales tareas realizadas fueron el tratamiento de valores nulos, la codificación de variables categóricas mediante One Hot Encoding, la conversión de valores booleanos a numéricos, la normalización de datos con Min-Max Scaling y la eliminación de filas duplicadas. Este proceso dejó los datos listos para su posterior análisis y modelado."

  Columnas eliminadas 
*asientos_traseros_plegables (70.02%) alto porcentaje de nulos elimino columna 
*marca porque es un valor repetitivo
*fecha_registro:mas del 50% de nulos

  Manejo de nulos
*modelo: 0,6% bajo porcentaje de nulos, elimino filas su porcentaje es bajo;
*km: 0,04% porcentaje bajo de nulos, elimino filas;
*potencia: 0,02%, porcentaje bajo de nulos, elimino filas;
*tipo_gasolina: 0,10% elimino filas  con nulos;
*color: 10% de nulos, decido imputarlo con valor desconocido para evitar el sesgo significativo;
*tipo_coche: con un 30% de nulos imputo desconocido porque me parece relevante la información. Había pensado en la  moda, pero sería contaminar el modelo;
*volante_regulable: 0.08%  porcentaje bajo de nulos, elimino filas;
*aire_acondicionado:desconocido,  porque tiene un valor de nulos entre el 10% y 30%;       
*camara_trasera  1% en este caso elimino las filas;
*elevalunas_electrico :1% eliminar filas. Maneje los nulos de forma directa;
*bluetooth:como es una variable de tipo objeto, la he convertido a booleano para imputarlo los nulos con false;
*gps  sin nulos;
*alerta_lim_velocidad: desconocido,  porque tiene un valor de nulos entre el 10% y 30%    
 precio:1% eliminar filas;    
 fecha_venta: convierto al formato pd.to_datime y elimino filas. Bajo porcentaje de nulos;

  Análisis univariable
1 Modelo: Agrupé los modelos en tres listas y apliqué una indexación con pandas.
2. Color: Apliqué el mismo procedimiento de agrupación, pero imputé los valores nulos como "desconocido" debido a que la columna tenía un 30% de valores faltantes. Decidí crear esta categoría aparte para evitar que los nulos afectaran el análisis, ya que el color influye considerablemente en los precios de los coches.
3. Tipo de coche: Traté esta columna de la misma manera que el color, agrupando las categorías y gestionando los nulos.
4. Tipo de gasolina: Simplifiqué las categorías en dos opciones, basándome en un umbral de 10, donde los combustibles más frecuentes fueron diésel y petrol. Este tratamiento refleja la tendencia de los vehículos según la fecha de venta.


  Análisis de correlación inicial
1. La relación entre precio:
*Potencia (+0.645): Los autos más potentes son más costosos; esta es la característica que más impacta en el precio;
*Cámara trasera (+0.256): Los autos con cámara trasera suelen tener un precio un poco más alto; es lógico al ser un aporte tecnológico para los coches nuevos;
*Elevalunas eléctrico (+0.266): Los vehículos modernos que incluyen elevalunas eléctricos tienden a ser más caros;
*Alerta de límite de velocidad (+0.387): Los coches con sistemas avanzados, como la alerta de velocidad, son más caros;
*Kilometraje (-0.408): Los vehículos con más kilómetros recorridos suelen ser más baratos. (En algunos países, esto puede variar, como en Venezuela):
*Aire acondicionado (+0.288): Los autos con aire acondicionado están presentes en modelos más avanzados, pero actualmente no siempre afecta mucho el precio.
2. La potencia también es una variable interesante para analizar la correlación en este estudio: 
*Volante regulable (+0.326): Los autos más potentes suelen tener accesorios extra, como los que tienen Alerta de límite de velocidad (+0.427), ya que  los autos modernos y potentes suelen incluir esta característica de seguridad.
*Elevalunas eléctrico (+0.342): Los vehículos potentes tienden a tener sistemas eléctricos avanzados, como los elevalunas.
3. En cuanto a la tecnología, los autos que incluyen:
*Bluetooth (+0.204),  suelen incluir otras características modernas, como elevalunas eléctricos, pero no afectan mucho el precio;
*De igual manera, la variable GPS (+0.155): Aunque el GPS es un accesorio avanzado, que en este caso no influye mucho en el precio.
4. Menos correlacionada
Fecha_ventaMes$año:menos correlacionada, no influye en la el precio del coche.


  Análisis variable vs target
1. Modelo: Los vehículos de baja demanda tienen precios más estables, mientras que los de alta demanda muestran una mayor variedad de precios, con algunos más caros y otros más baratos. Esto indica que los autos de alta demanda tienden a ser más caros, pero con más diferencias en sus precios. Los de media_demanda con un 0.131, parecen estar relacionados con los precios altos, pero es por sus accesorios.
2. Tipo coche: imputé la categoría 'Desconocido' para los datos nulos, ya que quiero incluirlos en el análisis sin omitirlos. Por ahora, no puedo hacer un análisis con esta categoría, ya que no ofrece información clara. Los autos de baja demanda tienen precios más estables, mientras que los de alta demanda tienen una mayor variedad de precios, con algunos muy caros y otros más baratos. Los autos de media demanda tienen precios intermedios, menos variados que los de alta demanda. Los tipos coche alto demanda, tiene una leve correlación+, quizás porque sean atractivos.
3. Color: Imputé la categoría 'Desconocido' para color y tipo de coche para no perder esos datos en el análisis. Los vehículos de color oscuro tienen una variedad de precios, con autos que van desde los más económicos hasta los de lujo. Los de color claro muestran precios más consistentes y generalmente más bajos. Los de color vivo tienden a estar asociados con precios más altos, típicos de autos deportivos o de lujo. En cuanto al color desconocido, 

En resumen, he creado una categoría llamada 'Desconocido' para los valores nulos en las columnas de color y tipo de coche, con el fin de no excluir estos datos del modelo. Esto me permite mantener toda la información disponible hasta que pueda tratar estos valores de manera más específica

  
  Transformación de categóricas a numéricas
1. One-hot encoding binario modelo utilizare la funccion get_dummies() 
color
tipo_coche
modelo
gasolina
 2. Astype para las sigueintes variables, ya las habia transformado a booleanas
aire_acondicionado
camara_trasera
elevalunas_electrico
alerta_lim_velocidad

  Escalar variables (usando minmaxscaler) 
1. tipo_gasolina: correlacion negativa alta. las variables redundan, elimino gasolina diesel
2. modelo_m_demanda: elimino la variable modelo media demanda, porque las otras variables explican mejor la relacion.
3. Precio&potencia con 0.644, muestra que ha medida que aumenta la potencia del coches asimismo el precio
4. precio&alerta_lim_velocidad: exixte una correlacion positiva medianamente baja con el precio
5. logprecio&potencia:0.509 muestra que la potencia teien una relacion positiva y moderada con el log precio, a medida que aumenta la potencia el logaritmo del precio lo hace.


He compartido este primer ejercico para mostrar mis inicios en los manejos de valores nulos, ya sea eliminando filas o rellenándolos con la media, mediana o moda. También entendí cómo la codificación de variables y la normalización son claves para preparar los datos para modelos de machine learning. Aunque fue un primer paso, este entregable me dio una buena base para continuar aprendiendo y seguir mejorarando mis habilidades en las ciencia de datos.
