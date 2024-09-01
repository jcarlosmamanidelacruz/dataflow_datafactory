# Creación de un Dataflow en Azure Data Factory

<br><img src="https://i.postimg.cc/TPYMVnFH/Title.png" alt="">

## Introducción

En el mundo actual, donde la gestión y transformación de datos es fundamental para la toma de decisiones empresariales, Azure Data Factory se ha consolidado como una herramienta poderosa para el desarrollo de procesos de integración y transformación de datos en la nube. Este proyecto tiene como objetivo demostrar cómo configurar un Dataflow en Azure Data Factory, un componente esencial para llevar a cabo transformaciones de datos complejas sin necesidad de escribir código personalizado.

## Objetivo del Proyecto

El principal objetivo de este proyecto es crear un pipeline de datos en Azure Data Factory que procese un conjunto de datos almacenado en Blob Storage, aplique una serie de transformaciones y almacene los resultados en un contenedor de salida. Se busca mostrar cómo se pueden realizar operaciones comunes como la derivación de columnas, el agregado de datos y la optimización de la salida de datos utilizando el entorno de Azure Data Factory.

## Recursos Utilizados

Para la ejecución de este proyecto, se han utilizado los siguientes recursos y servicios de Azure:

- Azure Resource Group: Un contenedor lógico que agrupa los recursos relacionados, en este caso, Azure Data Factory y Blob Storage.

- Azure Blob Storage: Servicio de almacenamiento de objetos que permite guardar grandes cantidades de datos no estructurados, como archivos y documentos.

- Azure Data Factory: Un servicio de integración de datos basado en la nube que permite crear, programar y administrar flujos de trabajo de datos.

- Linked Services: Conexiones que definen cómo los servicios externos, como Blob Storage, se integran dentro de Azure Data Factory.

- Datasets: Representaciones estructuradas de los datos que se encuentran en fuentes de datos como Blob Storage, necesarias para realizar operaciones de transformación.

- Mapping Data Flow: Un entorno visual dentro de Azure Data Factory para diseñar transformaciones de datos y aplicar lógica empresarial sobre ellos.

- Scala: Lenguaje utilizado para definir expresiones personalizadas dentro de las transformaciones de datos.

## Propósito del ProyectoPropósito del Proyecto

El propósito de este proyecto es ilustrar un caso práctico de cómo transformar datos dentro de Azure utilizando Data Factory. El proyecto se centra en un archivo CSV que contiene información sobre películas. La tarea principal es separar una columna que contiene el título y el año concatenados en dos columnas diferentes: una para el título y otra para el año. Posteriormente, se agrupan las películas por año para obtener una vista agregada del número de películas por cada año.

Los pasos detallados muestran cómo cargar datos en un entorno seguro, aplicar estas transformaciones específicas para preparar la información, y finalmente, cómo almacenar los resultados de manera eficiente. Este tipo de procesamiento es común en escenarios donde se necesita preparar datos para su análisis, generar informes o alimentar otros sistemas empresariales.

Además de servir como un tutorial, este proyecto es una guía práctica para cualquier profesional que busque implementar flujos de datos robustos y eficientes en la nube utilizando Azure Data Factory.

## CREACIÓN DE UN DATAFLOW EN AZURE DATA FACTORY

Generando Dataset, linked service, y el pipeline para el Mapping Data Flow

1. Inicie el explorador web Microsoft Edge o Google Chrome.
2. Iniciar Sesión en Azure Portal
3. Dirígete a la sección Create a resource y dale clic
4. En el buscador escribe Resource group, una vez lo ubiques dale clic
5. Clic en Create
Para crear el Grupo de recursos, realice los siguientes pasos:
Nombre grupo de recursos: rg-azuredatafactory
6. Clic en Review + create
7. Clic en Create

<br><img src="https://i.postimg.cc/500D3q00/1-input-container.png" alt="">


## Crear Blob Storage

1. Dirígete a la sección Create a resource y dale clic
2. En el buscador escribe Storage account, una vez lo ubiques dale clic
3. Clic en Create
	Para crear el Blob Storage, realice los siguientes pasos:
	Resource group: Seleccione el grupo de recursos creado en el paso anterior rg-azuredatafactory
	Storage account name: covidbsjmdc01
	Region: (US) East US
	Performance: Standard
	Redundancy: Locally-redundant storage (LRS)
4. Clic en Review + create
5. Clic en Create
<br><img src="https://i.postimg.cc/TPdfmbv7/4-Create-a-storage-account.png" alt="">

6. Nos dirigimos al Storage browser y damos clic en Bloc containers
7. Damos clic en Add container y le damos el nombre de input
<br><img src="https://i.postimg.cc/500D3q00/1-input-container.png" alt="">
8. Damos clic en Add container y le damos el nombre de output
<br><img src="https://i.postimg.cc/cH0k97LY/2-output-container.png" alt="">
9. Al contenedor input, subimos el archivo movies.csv y damos clic en Upload
<br><img src="https://i.postimg.cc/HxSwHbdf/3-upload-movies.png" alt="">
10. Creamos linked service, no dirigimos a Manage y le damos a New
11. Buscamos Blob Storage y le damos a continue
<br><img src="https://i.postimg.cc/XvLFc9Gp/4-linked-service.png" alt="">
12. Asignamos el nombre de blobmovies al linked service 
<br><img src="https://i.postimg.cc/J4XkYfHw/5-create-linked-service.png" alt="">
13. Nos dirigimos a Author y creamos un Dataset
14. Seleccionamos el Dataset de Blob Storage, damos a continue y seleccionamos csv
<br><img src="https://i.postimg.cc/cHjhqPRp/6-create-dataset.png" alt="">
15. Le asignamos un nombre inputcsv, seleccionamos el linked service creado anteriormente y en el filename seleccionamos movies.csv
16. Clic en ok
<br><img src="https://i.postimg.cc/5t9WjQhx/7-inputcsv.png" alt="">
17. Nos dirigimos a Author y creamos un Dataset para el output
18. Seleccionamos el Dataset de Blob Storage, damos a continue y seleccionamos csv
19. Le asignamos un nombre outputcsv, seleccionamos el linked service creado anteriormente y en el filename seleccionamos el contenedor output
20. Clic en ok
<br><img src="https://i.postimg.cc/15DkHKPm/8-outputcsv.png" alt="">
21. Creamos un nuevo pipeline con el nombre moviesMappinDataFlow
22. Nos dirigimos a la opciones de Factory Resources y creamos un nuevo Data Flow, este nos generará un nuevo Data Flow vacío
23. En el Output stream name asignamos: Movies
24. En el Source type seleccionamos la opción Dataset
25. En la opción Dataset seleccionamos el Linked service con nombre inputcsv
26. En options mantenemos activa la opción Allow schema drift
27. Activamos la opción de Data flow debug, el cual no permitirá validar todo el proceso y ejecutarlo y damos clic en ok.
<br><img src="https://i.postimg.cc/MTM6KjBn/9-Create-Data-Flow.png" alt="">
28. Nos dirigimos a la opción Data preview del dataflow y damos clic en la opción Refresh
<br><img src="https://i.postimg.cc/JzxYt63F/10-dataflow-preview.png" alt="">
29. Generamos una columna derivada, dando clicn el el símbolo mas de la actividad dataflow
<br><img src="https://i.postimg.cc/pTWFrCZs/11-derevid-columns.png" alt="">
30. le asignamos el nombre YearExtraccion
31. En la opción Column seleccionamos la columna title y en expresión damos clic en open expression builder
32.Asignamos el nombre tittleExtraction y colocamos el siguiente código en scala dentro de expression: toInteger(trim(right(title, 0) ‘()’))
33. para validar le damos clic a Refreshen la parte izquierda inferior 
34. Clic en Save and finish
<br><img src="https://i.postimg.cc/fTG5y405/12-expression.png" alt="">
35. Volvemos a Data preview y damos click en Refresh para ver la nueva columna
<br><img src="https://i.postimg.cc/rwWTRLZp/13-Refresh.png" alt="">
36. En YearExtraccion añadimos una nueva columna para separar el título y eliminar el año que qua no hace falta,, en Deriv columns settings añadimos una nueva columna con Add Columns y le damos el nombre del title
37. Abrirmos el expression builder y añadimos el código para eliminar el año de título toString(left(title, length(title)-6))
38. Damos clic en Data preview para para visualizar la nueva columna
39. Clic en Save and finish
<br><img src="https://i.postimg.cc/d3ksWZ62/14-new-columns-title.png" alt="">
## Guardamos los Datos Transformados en el Outputcsv

1. Damos clic al símbolo mas de YearExtraccion y damos clic en Sink
<br><img src="https://i.postimg.cc/NFFM3f84/15-guardar-sink.png" alt="">
3. Asiganamos el nombre MoviesClean
4. En la opción Incoming stream seleccionamos YearExtraction
5. En la opción Sink type va a ser una Dataset
6. En la opción Dataset seleccionamos el contenedor destino Outputcsv
<br><img src="https://i.postimg.cc/N0QrNtnN/16-sink-configuration.png" alt="">
8. En la opción Setting seleccionamos en file  name option la opción Output to single file
9. Le asignamos un nombre al archivo de salida de moviesclean.csv
<br><img src="https://i.postimg.cc/qqtT4tN1/19-Output-to-single-file.png" alt="">
8. En la opción Optimize seleccionamos la opción Single partition
<br><img src="https://i.postimg.cc/KjytPTtW/20-Single-partition.png" alt="">

## Añadiendo el Dataflow en Azure Data Factory

1. Nos dirigimos a nuestro pipeline moviesMappinDataFlow 
2. seleccionamos la actividad Data flow y en la opción Settings seleccionamos el dataflowMovies
3. Clic en Validate
<br><img src="https://i.postimg.cc/mZw0PyYK/17-Dataflow-Movies.png" alt="">
5. Damos clic a Debug para que se ejecute
<br><img src="https://i.postimg.cc/4xdH9GYV/18-Debug.png" alt="">
7. Verificamos en el contenedor outputcsv los múltiples archivos que se hayan generado con la ejecución de Data Factory
<br><img src="https://i.postimg.cc/kGN0vLpd/21-verificando-container-outputcsv.png" alt="">

## Agregando un nuevo Branch y Aggregate 

1. Nos dirigimos a la opción de Yearextraccion en nuestro dataflow y damos clic al símbolo más y damos clic en New branch.
<br><img src="https://i.postimg.cc/DzkLGDLg/22-new-branch.png" alt="">
2. Agregamos una transformación de agregate.
<br><img src="https://i.postimg.cc/9fd8wyRD/23-Transformacion-aggregate.png" alt="">
3. En la sección de Group by en la parte de colmns seleccionamos year.
4. En Aggregates generamos una nueva columna que se va a llamar MoviesCount e introducimos la siguiente expresión count().
5. Damos a Save and finish.
<br><img src="https://i.postimg.cc/xjBf9bmw/24-columns-agregate.png" alt="">
6. Agregamos un nuevo Sink.
7. Al nuevo sink le ponemos de nombre MoviesbyYear.
8. En Dataset seleccionamos nuestro contenedor outputcsv.
9. En la sección Settings seleccionamos Output to single file.
10. Le damos el nombre de MoviesbyYear.csv a nuestro archivo de salida.
11. En la sección de Optimize seleccionamos Single partition.
12. Damos clic a Data preview para ver los resultados.
13. Volvemos al pipeline y damos a Debug para ejecutar todo el proceso.
14. Damos clic en publish all.
<br><img src="https://i.postimg.cc/3RKyC01S/25-Debug-Pipeline-final.png" alt="">
