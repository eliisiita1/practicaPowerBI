PRÁCTICA POWER BI.  
**Pasos a seguir**

Primero se carga el fichero Airbnb-Listing Madrid csv como fuente de datos y se transforma. Para ello, se eliminan las columnas que no son necesarias, como Listing url, el nombre o el resumen. Además, se borra la columna ‘Experiences offered’ porque tiene un porcentaje muy alto de valores 'none', y no aporta valor. 

Además, se añade un filtro para trabajar únicamente con los airbnbs en Madrid (filtramos por las que contienen “Mad”, vemos que el resultado es correcto, y aceptamos), como se muestra en la siguiente imagen.

 ![image](https://github.com/user-attachments/assets/8dd26489-f250-4686-836f-cd1e1adef397)

Puesto que se necesitan solo los datos relacionados con los airbnbs de Madrid/ Comunidad de Madrid, se eliminan también las columnas Country Code, Market (siempre es Madrid), Country, etc, que son innecesarias.

A continuación, se carga el fichero Nveces_alquilado.csv como fuente de datos y, por último, se añade la relación entre ambos archivos cargados, como se muestra en la siguiente imagen.

 ![image](https://github.com/user-attachments/assets/27d3d7a5-1890-400c-853f-ac71479e2041)
 

Una vez se cargan los ficheros y se eliman las columnas innecesarias, se van a crear las columnas calculadas que se usarán en la creación del Dashboard.

La primera columna del fichero ‘airbnb-listings Madrid’ creada es ‘Number of amenities’, que calcula cuántas amenities tiene un Airbnb a partir del listado de amenities, con la fórmula DAX de la siguiente imagen.

 ![image](https://github.com/user-attachments/assets/9ee54c9e-933c-43e9-bf71-0c454e71a591)

Las partes de la fórmula son las siguientes:
+ LEN('YourTableName'[amenities]) -> Calcula la longitud de la cadena en la columna amenities.

 + SUBSTITUTE('YourTableName'[amenities], ",", "") -> Elimina todas las comas de la cadena.

+ LEN('YourTableName'[amenities]) - LEN(SUBSTITUTE('YourTableName'[amenities], ",", "")) -> Encuentra la diferencia en longitud, que es el número de comas en la cadena.

+ +1-> Añade 1 al resultado para contar el número total de amenities, ya que el número de comas es siempre uno menos que el número de items listados.

Otra columna calculada para el fichero ‘airbnb-listings Madrid’ que se añade es ‘Number of Host Verification’, que, de la misma forma en la que se calcula la columna anterior, muestra cuántas verificaciones tiene cada host. La fórmula utilizada con DAX se muestra en la siguiente imagen:

![image](https://github.com/user-attachments/assets/ba77ec25-d885-4717-ad7e-0d5133505c25)

 
Por último, se crea la columna calculada ‘RentalCategory’ en el fichero ‘Nveces_alquilado’ para clasificar los airbnbs por el número de veces que se ha alquilado, agrupándolos en tres grupos: Recién estrenado, veterano de alquiler y estrella del alquiler. En la siguiente imagen se muestra la fórmula calculada con DAX:
 
 ![image](https://github.com/user-attachments/assets/51755843-3eba-417c-b191-830208f91570)


**Explicación del Dashboard creado.**

Con este dashboard se busca estudiar cómo afectan las distintas características del Airbnb en alquiler y el host de este con respecto a las notas que reciben en las valoraciones.

-	Página 1 - Tasa de reviews
 ![image](https://github.com/user-attachments/assets/d5a10c60-952a-4e47-a648-e68a8502b9a3)

En esta página se crean todos los gráficos necesarios para estudiar cómo afectan las características de los hosts y de los airbnbs a las reviews recibidas por los usuarios. 

A continuación se detalla cada gráfico creado en esta página.


* Informe Host Id, Host Listing, Reviews rate y rental category. ![image](https://github.com/user-attachments/assets/8d6a89f3-8475-4939-a946-bc0d88b03fd9)

Este informe es muy útil para visualizar los top 100 host ids con sus reviews, las categorías de alquiler y los host listings. 
Además, las tres últimas columnas están configuradas para tener un color de fondo condicional segúm su valor, lo cual facilita su lectura y comprensión.
 
+ **Relación entre la tasa de respuesta del anfitrión y la calificación de las reseñas**:
![image](https://github.com/user-attachments/assets/6a5c085a-20d2-48cd-b090-6b229264887a)

Este gráfico de dispersión muestra que parece haber una correlación clara entre el **Host Response Rate** (tasa de respuesta del anfitrión) y el **Review Scores Rating** (calificación de las reseñas). Los datos indican que la mayor parte de anfitriones que tienen una tasa de respuesta muy alta, se refleja en mejores calificaciones.
  

 ÷ **Relación entre el tipo de propiedad y el tipo de habitación con el promedio de valor de las reseñas**.

 ![image](https://github.com/user-attachments/assets/c0875ab5-212a-470d-9067-1539bec1a57e)

Aquí se puede ver la comparación del **Review Scores Value** entre diferentes tipos de propiedades y tipos de habitaciones. Los alojamientos de tipo **Entire home/apt** y **Private room** parecen tener un rango de puntuaciones más altas que los alojamientos compartidos (**Shared room**).
Los **Apartments**, **Lofts** y **Townhouses** tienden a tener mayores puntuaciones, mientras que propiedades como **Hostels** y **Boutique Hotels** tienden a tener puntuaciones más bajas.
Como conclusión, las propiedades más privadas como **apartamentos completos** o **lofts** tienden a recibir mejores valoraciones en comparación con habitaciones compartidas o propiedades más comunes como hostales.

÷ **Ranking de barrios con las calificaciones más bajas**.
![image](https://github.com/user-attachments/assets/e909a651-a853-44f1-bc87-f83824d71170)

Este gráfico de barras clasifica los barrios que han recibido las calificaciones más bajas. Los barrios de **Moncloa**, **Valdeacederas** y **Nueva España** son los que tienen los puntajes más bajos en promedio.
Como conclusión, estos barrios podrían necesitar mejoras en cuanto a la calidad de sus alojamientos o en los servicios que ofrecen, ya que reciben las calificaciones más bajas en el dataset.


+ **Comparación de factores clave en las evaluaciones**.

![image](https://github.com/user-attachments/assets/e11017a3-70f7-4b26-bc40-0988381dc188)

Este gráfico de radar compara cuatro factores clave en las evaluaciones: **Número de Amenidades**, **Precio**, **Tarifa de Limpieza** y **Noche Mínima**.
Como conclusión, los **precios** y las **tarifas de limpieza** tienden a recibir puntajes más bajos en comparación con las demás categorías, lo que sugiere que los usuarios encuentran que estos dos factores no son tan satisfactorios. Además, el **número de amenidades** y las **noches mínimas** parecen recibir evaluaciones más equilibradas.


-	Página 2 - Comparación por reviews de los airbnbs con peor y mejor reviews.

  ![image](https://github.com/user-attachments/assets/9189cac6-c796-44be-83af-fe843761aeed)

En esta página se hace la comparación del resultado del promedio de las distintas características de los Airbnb para los pero valorados y los mejor valorados con más reviews.
 
Como conclusión, el número de comodidades, el porcentaje de respuesta del host y el número de veces que se alquila, de los Airbnb mejor valorados tienen un promedio mayor, por lo que son características que favorecen que los Airbnb sean mejores. Estas características afectan proporcionalmente a la nota que los usuarios ponen a los airbnbs.
Por otro lado, la tasa de limpieza es más alta en los airbnbs mejor valorados, por lo que seguramente haga que los airbnbs estén más limpios y esto a su vez favorezca la nota del Airbnb. Esto mismo ocurre con el precio, que, es mayor en airbnbs mejor valorados seguramente por las características que tiene. 
Por último, el número de verificaciones del host, la disponibilidad y el número de estancias en los airbnbs es menor en los airbnbs mejor valorados, pero son características que no deben afectar proporcionalmente a la score review.


- Página 3 - Pronostico de reviews.

![image](https://github.com/user-attachments/assets/3e293fe7-e7cc-4529-aa2f-445c9a852414)

En esta página se muestra un gráfico de líneas de la suma de las reviews de los host ids a lo largo de los años. Además, se calcula el valor máximo, mínimo y medio, y se hace el pronóstico de los siguientes meses.
Debido a que esta línea es muy variada en la zona de valores existentes, la línea generado de pronóstico no es muy buena.
