PRÁCTICA POWER BI.  
Primero se carga el fichero Airbnb-Listing Madrid csv como fuente de datos y se transforma. Para ello, se eliminan las columnas que no son necesarias, como Listing url, el nombre o el resumen. Además, se borra la columna ‘Experiences offered’ porque tiene un porcentaje muy alto de valores 'none', y no aporta valor. 

Además, se añade un filtro para trabajar únicamente con los airbnbs en Madrid (filtramos por las que contienen “Mad”, vemos que el resultado es correcto, y aceptamos), como se muestra en la siguiente imagen.

 ![image](https://github.com/user-attachments/assets/8dd26489-f250-4686-836f-cd1e1adef397)

Puesto que se necesitan solo los datos relacionados con los airbnbs de Madrid/ Comunidad de Madrid, se eliminan también las columnas Country Code, Market (siempre es Madrid), Country, etc, que son innecesarias.

A continuación, se carga el fichero Nveces_alquilado.csv como fuente de datos y, por último, se añade la relación entre ambos archivos cargados, como se muestra en la siguiente imagen.

 ![image](https://github.com/user-attachments/assets/27d3d7a5-1890-400c-853f-ac71479e2041)
 
En este nuevo fichero, se crea una nueva columna nueva que es el número de amenities que tiene cada Airbnb a alquilar.

Una vez se cargan los ficheros y se eliman las columnas innecesarias, se van a añadir las columnas calculadas que se usarán en la creación del Dashboard.

La primera columna del fichero ‘airbnb-listings Madrid’ a crear es ‘Number of amenities’, que calcula cuántas amenities tiene un Airbnb a partir del listado de amenities.

 ![image](https://github.com/user-attachments/assets/9ee54c9e-933c-43e9-bf71-0c454e71a591)

Las partes de la fórmula son las siguientes:
LEN('YourTableName'[amenities]) -> Calcula la longitud de la cadena en la columna amenities.

SUBSTITUTE('YourTableName'[amenities], ",", "") -> Elimina todas las comas de la cadena.

LEN('YourTableName'[amenities]) - LEN(SUBSTITUTE('YourTableName'[amenities], ",", "")) -> Encuentra la diferencia en longitud, que es el número de comas en la cadena.

+ 1-> Añade 1 al resultado para contar el número total de amenities, ya que el número de comas es siempre uno menos que el número de items listados.

Otra columna calculada para el fichero ‘airbnb-listings Madrid’ quw se añade es ‘Number of Host Verification’, que, de la misma forma en la que se calcula la columna anterior, muestra cuántas verificaciones tiene cada host.

![image](https://github.com/user-attachments/assets/ba77ec25-d885-4717-ad7e-0d5133505c25)

 
Por último, se crea la columna calculada ‘RentalCategory’ en el fichero ‘Nveces_alquilado’ para clasificar los airbnbs por el número de veces que se ha alquilado, agrupándolos en tres grupos: Recién estrenado, veterano de alquiler y estrella del alquiler.
 
 ![image](https://github.com/user-attachments/assets/51755843-3eba-417c-b191-830208f91570)


*Explicación del Dashboard creado.*

Con este dashboard se busca estudiar cómo afectan las distintas características del Airbnb en alquiler y el host de este con respecto a las notas que reciben en las valoraciones.
-	Página 1 - Tasa de reviews
 ![image](https://github.com/user-attachments/assets/d5a10c60-952a-4e47-a648-e68a8502b9a3)

En esta página se crean todos los gráficos necesarios para estudiar cómo afectan las características de los hosts y de los airbnbs a las reviews recibidas por los usuarios. 
Como conclusiones, se pueden obtener las siguientes:
o	La valoración de la respuesta de los host afecta proporcionalmente a la valoración de los reviews. 
o	 

	
-	Página 2 - Comparación por reviews de los airbnbs con peor y mejor reviews.

  ![image](https://github.com/user-attachments/assets/9189cac6-c796-44be-83af-fe843761aeed)

En esta página se hace la comparación del resultado del promedio de las distintas características de los Airbnb para los pero valorados y los mejor valorados con más reviews.
 

-	Conclusiones:
El número de comodidades, el porcentaje de respuesta del host y el número de veces que se alquila, de los Airbnb mejor valorados tienen un promedio mayor, por lo que son características que favorecen que los Airbnb sean mejores. Estas características afectan proporcionalmente a la nota que los usuarios ponen a los airbnbs.
Por otro lado, la tasa de limpieza es más alta en los airbnbs mejor valorados, por lo que seguramente haga que los airbnbs estén más limpios y esto a su vez favorezca la nota del Airbnb. Esto mismo ocurre con el precio, que, es mayor en airbnbs mejor valorados seguramente por las características que tiene. 
Por último, el número de verificaciones del host, la disponibilidad y el número de estancias en los airbnbs es menor en los airbnbs mejor valorados, pero son características que no deben afectar proporcionalmente a la score review.

-	Página 3 - Pronostico de reviews.

![image](https://github.com/user-attachments/assets/3e293fe7-e7cc-4529-aa2f-445c9a852414)

En esta página se muestra un gráfico de líneas de la suma de las reviews de los host ids a lo largo de los años. Además, se calcula el valor máximo, mínimo y medio, y se hace el pronóstico de los siguientes meses.
Debido a que esta línea es muy variada en la zona de valores existentes, la línea generado de pronóstico no es muy buena.
