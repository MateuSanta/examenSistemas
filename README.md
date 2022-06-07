# examenSistemas
examen

### Introducción

En este documento explicaré los pasos que he realizado para hacer el examen práctico de sistemas, consistirá en usar docker-compose para crear 3 imagenes que puedan desplegar mi proyecto.

Las 3 imágenes consistirán en:

  1- tomcat:9.0
  
  2- nginx
  
  3- mysql:8.0.29
 
 Por tanto este proyecto consta de 3 capas:
   La capa de presentación: Usaremos nginx para el despliegue de la página web.
   La capa de proceso: El servidor de aplicaciones utilizado será tomcat:9.0
   La capa de datos: El servidor de datos usado será mysql server
   
   
 ### Configuración del docker-compose.yml
 
 ![Captura desde 2022-06-07 19-48-28](https://user-images.githubusercontent.com/91744614/172449066-7cf739a7-18b9-4331-9a79-f0bc16cbe96f.png)
 
 En ``services`` estableceremos las tres nombres con las respectivas imágenes que queramos utilizar.
 
 ``images``: 
  Utilizaremos la imagen de mysql:8.0.29.
 
 ``volumes``: 
   La primera ruta indica la ruta en el host. 
   La segunda ruta indica el contenedor.(Ahí estarán los archivos de creación de la base de datos)
 
 ``environment``: 
  Establece las variables de entorno con su respectivo valor.
 
 ``ports``: 
   EL primer puerto indica el puerto del host.

   El segundo puerto indica el puerto de cada contenedor.
  
 

 
 
 ### Pasos para el despliegue de la aplicación
 
 ## 1. Eliminar contenedores existentes
 
 Primero eliminar contenedores para que no haya conflicto de ningún tipo.
 
 ![1-eliminarContenedores](https://user-images.githubusercontent.com/91744614/172451846-ae9e305a-7778-4529-8539-5fb23f7ada16.png)

 
 ## 2. Elminar todas las imagenes
 
Eliminar imagenes previas para poder descargar nuevamente las correspondientes.
 
![2-eliminarImagenes](https://user-images.githubusercontent.com/91744614/172451855-a7c28d2e-aa0c-4be5-b499-8d7731dbb79d.png)

 
 ## 3. Ejecutar docker-compose.yml
 
 Con el comando ``sudo docker-compose up -d`` ejecutaremos el archivo docker-compose.yml de la carpeta en que estemos.
 Como no tenemos las imagenes se descargarán de nuevo en docker hub automáticamente.
 
 ![3-docker-composeup](https://user-images.githubusercontent.com/91744614/172451862-88e0953b-f74a-43ad-896c-06421f3706d1.png)

 
 ## 4. Hacer login en docker hub
 
 Usar el comando ``sudo docker login`` para logearse en docker hub.
 
 ![4-docker-login](https://user-images.githubusercontent.com/91744614/172452712-9a16786b-b7d9-4082-b3a7-a07befb24651.png)

 
  ## 5. Subir las imagenes a Docker Hub
  
  Utilizaremos los siguientes comandos en las 3 imagenes para agregar un tag a nuestra imagen para despues poder hacer un push
  
   ``sudo docker tag tomcat:9.0 msantandreu/sic.tomcat``
   ``sudo docker push msantandreu/sic.tomcat``

   
   
   ![Captura desde 2022-06-07 20-17-49](https://user-images.githubusercontent.com/91744614/172454321-7d84f296-b568-47b9-9a36-817db262fcc6.png)
   
   ## Enlaces para descargar las imagenes

   https://hub.docker.com/repository/docker/msantandreu/sic.mysql
   
   https://hub.docker.com/repository/docker/msantandreu/sic.tomcat
   
   https://hub.docker.com/repository/docker/msantandreu/sic.nginx
   
   ### Conclusiones y pruebas
   
   Vemos que en localhost gracias al ``nginx`` nos conecta a nuestra página web.
   ![Captura desde 2022-06-07 20-36-14](https://user-images.githubusercontent.com/91744614/172457449-23a1ebe6-365d-45df-9319-253bfebbd25c.png)
   
   Aqui comprobamos que efectivamente podemos entrar en la aplicación (el ``tomcat`` funciona correctamente con el app.war)y buscar un producto en la base de datos que empieze por la letra "t"(el servicio de ``mysql``server está activo y se conecta perfectamente).
   
  ![Captura desde 2022-06-07 20-36-40](https://user-images.githubusercontent.com/91744614/172457546-4c0ed70f-7bd8-4bc5-8027-66ee6670d73b.png)

   
   
   
