# Taller 4 : TALLER DE ARQUITECTURAS DE SERVIDORES DE APLICACIONES, META PROTOCOLOS DE OBJETOS, PATRÓN IOC, REFLEXIÓN

En este taller, el objetivo es construir un servidor web en Java utilizando el framework Spring, el cual permite crear aplicaciones web de una manera sencilla y eficiente. Debe ser capaz de atender solicitudes HTTP y entregar páginas HTML e imágenes.

Para lograr esto, se debe crear una clase principal que inicie el servidor y un controlador que maneje las solicitudes HTTP. Además, se utilizará una anotación personalizada que indique que una clase es un componente y se cargará automáticamente en el servidor. También se debe mostrar cómo cargar un POJO desde la línea de comandos y asignarlo a una propiedad de un objeto.

El servidor debe ser capaz de atender múltiples solicitudes no concurrentes y manejar diferentes tipos de contenido, como HTML y PNG. Al final del taller, se habrá construido un servidor web funcional que demuestre las capacidades reflexivas de Java y el uso de POJOs en el desarrollo de aplicaciones web.

## Empezando

El proyecto contiene:

--> En la carpeta [arep](https://github.com/cristiandavid0124/AREMLab3/tree/main/src/main/java/edu/eci/arep).

- La clase HttpServer es un servidor HTTP simple que implementa la inversión de control para mapear rutas HTTP: [HttpServer](https://github.com/cristiandavid0124/AREMLab3/blob/main/src/main/java/edu/eci/arep/HttpServer.java).
- La clase ServerStarter es la clase principal del servidor web y se encarga de iniciar el servidor HTTP. Utiliza la clase HttpServer, que es un singleton, para crear una instancia del servidor y luego llama al método start para iniciarlo. Está es la clase que va a correr el laboratorio. [ServerStarter](https://github.com/cristiandavid0124/AREMLab3/blob/main/src/main/java/edu/eci/arep/ServerStarter.java).

--> En la carpeta [loC](https://github.com/cristiandavid0124/AREMLab3/tree/main/src/main/java/edu/eci/IoC).

- @Component es una anotación personalizada utilizada en el framework IoC (Inversión de Control) para indicar que una clase es un componente. [Component](https://github.com/cristiandavid0124/AREMLab3/blob/main/src/main/java/edu/eci/IoC/Component.java).
-  Clase que gestiona los archivos del componente [ComponentFileManager](https://github.com/cristiandavid0124/AREMLab3/blob/main/src/main/java/edu/eci/IoC/ComponentFileManager.java).
-  La anotación @GetMapping es una anotación personalizada utilizada en el framework IoC para mapear una URL a un método específico en una clase.[GetMapping](https://github.com/cristiandavid0124/AREMLab3/blob/main/src/main/java/edu/eci/IoC/GetMapping.java).
- la anotacion @RestController: Es una anotación personalizada que indica que la clase es un controlador RESTful. Esta anotación, similar a @Component en el contexto de Spring, marca a la clase para ser gestionada por el framework IoC para manejar solicitudes HTTP.[RestController](https://github.com/cristiandavid0124/AREMLab3/blob/main/src/main/java/edu/eci/IoC/RestController.java).
- la anotacion @RequestParam  es una Anotación que marca los parámetros de método que deben ser extraídos de los parámetros de la solicitud HTTP en el contexto de la aplicacion.[RequestParam](https://github.com/cristiandavid0124/AREMLab3/blob/main/src/main/java/edu/eci/IoC/RequestParam.java).
- GreetingController : Es una clase que actúa como un controlador en el contexto del framework IoC. Está anotada con @RestController, usa greeting(@RequestParam(value = "name", defaultValue = "World") String name): Método que maneja la solicitud HTTP GET a /greeting. Usa @RequestParam para obtener el valor del parámetro name de la solicitud. Si no se proporciona el parámetro name, se utiliza el valor predeterminado "World". Luego, devuelve un saludo formateado con el nombre proporcionado.[GreetingController](https://github.com/cristiandavid0124/AREMLab3/blob/main/src/main/java/edu/eci/IoC/GreetingController.java).

--> En la carpeta [resource](https://github.com/cristiandavid0124/AREMLab3/tree/main/src/main/resource). contiene los archivos con los cuales se comprueba el funcionamiento pedido

- Archivo PNG [Imagen](https://github.com/cristiandavid0124/AREMLab3/blob/main/src/main/resource/Kit.png)
- Archivo HTML [Pagina](https://github.com/cristiandavid0124/AREMLab3/blob/main/src/main/resource/PruebaHtml.html)

--> En la carpeta [Pruebas](https://github.com/cristiandavid0124/AREMLab3/tree/main/src/test/java/edu/eci/arep).

- [ComponentFileManagerTest](https://github.com/cristiandavid0124/AREMLab3/blob/main/src/test/java/edu/eci/arep/ComponentFileManagerTest.java). En la presente están las pruebas unitarias planteadas.



## Requisitos previos

[Maven](https://maven.apache.org/) : Con esta herramienta se creo la estructura del proyecto y se manejan las dependencias que se necesitan

[Git](https://git-scm.com/) : Se basa en un sistema de control de versiones distribuido, donde cada desarrollador tiene una copia completa del historial del proyecto.

Para asegurar una correcta instalación de Maven, es crucial confirmar que la versión del JDK de Java sea compatible. Si el JDK no está actualizado, la instalación de las versiones actuales de Maven podría fallar, generando problemas durante el uso de la herramienta.
```
java -version 
```

## Instalando

Para poder ver el funcionamiento de este taller se debe hacer lo siguiente:

Clonar el repositorio en su maquina local. Para esto utilice el siguiente comando y ejecutelo.

```
git clone https://github.com/cristiandavid0124/AREMLab3.git
```

Por consiguiente se debe ingresar al directorio del proyecto 

```
cd AREMLab3
```
Ya teniendo lo anterior es momento de compilar con Maven , se debe ejecutar el siguiente el comando
```
mvn clean install
```

Ya por último debemos ejecutar la clase que nos permitira ver el funcionamiento de la aplicación
```
java -cp target/classes edu.eci.arep.ServerStarter
```

- Los siguientes links corresponden a las paginas para hacer las pruebas:
  
Pagina Presentación - Prueba HTML
```
http://localhost:35000/host
```
Prueba archivo PNG
```
http://localhost:35000/image
```
Prueba Saludo
```
http://localhost:35000/hello
```
Pagina greeting 
```
http://localhost:35000/greeting
```


- Par ver la ejecución de las pruebas , se debe usar el siguiente comando dentro del directorio del proyecto
```
mvn test
```
  
## Arquitectura

 El código proporcionado implementa un servidor HTTP simple que utiliza la inversión de control (IoC) para manejar las solicitudes HTTP. La clase `HttpServer` es responsable de iniciar el servidor HTTP y manejar las solicitudes HTTP. La anotación `Component` se utiliza para indicar que una clase es un componente de Spring, lo que permite que el contenedor de Spring inyecte dependencias en la clase. La anotación `GetMapping` se utiliza para mapear una solicitud HTTP GET a un método en una clase.

La clase `ComponentFileManager` es un ejemplo de un componente de Spring que puede ser inyectado en otras clases. La clase proporciona métodos para leer y escribir archivos en el servidor HTTP. La clase `ServerStarter` es el punto de entrada de la aplicación y es responsable de crear una instancia de `HttpServer` y llamar al método `start` para iniciar el servidor HTTP.

La arquitectura del código se basa en la inversión de control (IoC), lo que significa que el contenedor de Spring es responsable de crear y gestionar las instancias de las clases. El contenedor de Spring inyecta dependencias en las clases utilizando las anotaciones `Component` y `Autowired`. Esto permite una mayor flexibilidad y modularidad en la aplicación, ya que las clases pueden ser reutilizadas y configuradas de manera diferente según las necesidades de la aplicación. Además, la arquitectura basada en IoC permite una mejor prueba de las clases, ya que las dependencias pueden ser inyectadas de forma explícita en lugar de crearlas dentro de las clases.

- El código implementa un servidor HTTP simple que utiliza la inversión de control (IoC) y las anotaciones de Spring para gestionar las solicitudes HTTP. La arquitectura basada en IoC permite una mayor flexibilidad y modularidad en la aplicación, ya que las clases pueden ser reutilizadas y configuradas de manera diferente según las necesidades de la aplicación. Además, la arquitectura basada en IoC permite una mejor prueba de las clases, ya que las dependencias pueden ser inyectadas de forma explícita en lugar de crearlas dentro de las clases.



## Pruebas Realizadas

- Archivo HTML - Host (En la presente se puede dirigir a la Imagen , Pagina Html (El mismo host) y el saludo)
![alt text](image.png)

- Saludo
![alt text](img/image-2.png)


- Archivo PNG 
![alt text](img/image-1.png)

- Prueba  greeting
![alt text](img/image-3.png)

- Pruebas unitarias 
![alt text](img/image-4.png)



## Construido con

* [Maven](https://maven.apache.org/) - Gestión de dependencias
* [Java](https://www.java.com/es/) - Lenguaje Utilizado
* [GitHub](https://git-scm.com/) - Control de Versiones



## Autores

* **Cristian Naranjo** - *Arep* - [cristiandavid0124](https://github.com/cristiandavid0124)
