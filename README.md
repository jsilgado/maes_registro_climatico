# Registro climático

Situación de aprendizaje.
Se creará una aplicación de consulta de datos del clima de diferentes países a lo largo de diversos años. Tratamiento de la información para comprobar los aumentos de temperaturas en los diferentes países y su progresión.

![image](https://img.shields.io/badge/Spring_Boot-F2F4F9?style=for-the-badge&logo=spring-boot)
![image](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)
![image](https://img.shields.io/badge/json-5E5C5C?style=for-the-badge&logo=json&logoColor=white)
![image](https://img.shields.io/badge/Eclipse-2C2255?style=for-the-badge&logo=eclipse&logoColor=white)
![image](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=Postman&logoColor=white)
![image](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)

## Actividad 1 - Fundamentos de RESTful APIs

- Un API **Application Programming Interface** es un conjunto de funcionalidades o recursos que nos expone un sistema para poder interactuar con él desde otro sistema. Sin importar el lenguaje en el que esté programado.
- Rest: **Representational State Transfer**, es un estilo de arquitectura de software para realizar una comunicación cliente-servidor. Se apoya en el protocolo HTTP para la comunicación al servidor y los mensajes que se envían y reciben pueden estar en XML o JSON.

Por lo tanto: API RESTful es un API que fue diseñada usando la arquitectura REST.

![Api rest](https://github.com/jsilgado/maes_registro_climatico/blob/master/images/450px-API-Rest.png) 

Imagen: API REST- Autor: [Seobility](https://www.seobility.net/es/wiki/API_REST) - Licencia: [CC BY-SA 4.0](https://www.seobility.net/es/wiki/Creative_Commons_License_BY-SA_4.0) 

Api rest públicas: 
- [Platzi Fake Store API](https://fakeapi.platzi.com/en/rest/users/)
- [Quotes](https://quotes.rest/) con Swagger (Necesita registrar)
- [Random User](https://randomuser.me/)
- [Pokeapi](https://pokeapi.co/)
- [The Rick and Morty API](https://rickandmortyapi.com/) 
- [Fake Store API](https://fakestoreapi.com)
- [Unsplash](https://unsplash.com/developers) (Necesita registrar)


## Actividad 2 - Creación del proyecto

- Crea un proyecto spring boot utlizando https://start.spring.io/ con las siguientes características:
```bash
Proyect: Maven
Languaje: Java
Spring boot: 3.2.3
Dependencies: Spring Web, Lombok
```
![Imagen](https://github.com/jsilgado/maes_registro_climatico/blob/master/images/Spring%20Initializr.png)

- Impórtalo en eclipse.
- Crear un package "controller" en com.maes, quedando com.maes.controller.
- Crear un método String hello() que devuelva “Hello world”. Anotarlo con @GetMapping
- Crear una clase controller Bienvenida.java con la anotación @RestController y @RequestMapping("/")

```bash
@RestController
@RequestMapping("/")
public class Bienvenida {

	@GetMapping
	public String hello() {
		return "Hello World";
	}
}
```
- Fichero de propiedades: En la ruta src/main/resources se encuentra el fichero de propiedades **application.properties**
Por defecto el puerto de despliegue es 8080. Si queremos modificarlo añadir al archivo:
```bash
server.port=8090 
```
Nota: se puede cambiar la extensión del fichero application.properties a application.yml para cambiar la configuración de tu aplicación de un archivo de propiedades clave-valor a un archivo yml. La notación yml es la más usada en la actualidad. 
[Más información](https://www.baeldung.com/spring-boot-yaml-vs-properties) 

- Desplegar la aplicación y acceder a [localhost:8090](http://localhost:8090/) y visualizar el resultado en el navegador y en Postman

#### Entrega: Sube el código a tu carpeta git con tu nombre en https://github.com/jsilgado/maes_registro_climatico/tree/master/alumnos

## Actividad 3 - Modelado de datos

### Dependencias
- Volviendo a https://start.spring.io/ selecciona las dependencias:
![image](https://github.com/jsilgado/maes_registro_climatico/blob/master/images/SpringInitializrBBDD.png)

Descarga el proyecto, accede a archivo pom.xml, copias la dependencia maven a nuestro proyecto.


### Dominio
- Crear un package "domain" quedando com.maes.domain
- Crear las clases de entidades de dominio con sus atributos:

#### Pais

| Attribute | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `pais_id` | `Integer` | **Required**. Identificador de país |
| `nombre` | `String` | **Required**. Nombre del país |

#### Ciudad

| Attribute | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `ciudad_id` | `Integer` | **Required**. Identificador de ciudad |
| `cuidad_id` | `Integer` | **Required**. FK Pais |
| `nombre` | `String` | **Required**. Nombre de la ciudad |

#### Registro

| Attribute | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `registro_id` | `Integer` | **Required**. Identificador de registro |
| `pais_id` | `Integer` | **Required**. FK Pais |
| `ciudad_id` | `Integer` | **Required**. FK Ciudad |
| `anyo` | `Integer` | **Required**. Año del registro |
| `mes` | `Integer` | **Required**. Mes del registro |
| `temperatura` | `Double` | **Required**. Temperatura |

- En nuestras clases de dominio Grupo y Contacto añadiremos las anotaciones de JPA (Java Persistence API)
  

```bash
En la clase
@Entity
@Table(name = “nombre_de_tabla“)

Por cada atributo
@Column(name = “nombre_columna“)
```

### Repositorio: 
- Crear un package repository quedando com.maes.repository.
- Por cada tabla crear una interfaz tal que:
  
```bash
@Repository
public interface NombreTablaRepository extends JpaRepository<NombreTabla, Integer>
```
### Servicio: 
- Crear un package service quedando com.maes.service.
- Crear una clase PaisService,  con un método:

```bash
List<Pais> getPaises().
```
- Crear una clase controller PaisController,  con un método: 
```bash
@GetMapping("/paises")
public ResponseEntity<List<Pais>> getAll() {
   return Optional.ofNullable(paisService.getAll()).map(lst ->  ResponseEntity.ok().body(lst)) // 200 OK
      .orElseGet(() -> ResponseEntity.notFound().build()); // 404 Not found
}
```

- Desplegar la aplicación y acceder a [localhost:8090/paises](http://localhost:8090/paises) y visualizar el resultado en el navegador y en Postman
- Realizar esta misma actividad pero para la entidad Ciudad.

#### Entrega: Sube el código a tu carpeta git con tu nombre en https://github.com/jsilgado/maes_registro_climatico/tree/master/alumnos

## Actividad 4 - Estándares y buenas prácticas

Crea un grupo de 3 personas por cercanía en el aula. Cada grupo elige una aplicación móvil o página web que les interese. Una vez elegida tendrán que elegir 4 funcionalidades que podría tener esa aplicación de tipo: obtención de datos con filtro y paginación, inserción, modificación o borrado de datos. Actividad similar realizada en la unidad 2.

Posteriormente se indica a cada persona del grupo a que rol de expertos van a pertenecer: A (Request), B (Response), C (Pruebas). 

[Documentación de experto](https://github.com/jsilgado/maes_registro_climatico/blob/master/Actividad4.pdf) 

- Estudio individual:  Cada estudiante desde su asiento, estudia en profundidad su parte, asegurándose de comprenderla completamente. Se recomienda tomar notas, realizar resúmenes y preparar preguntas.
- Grupos de expertos: Los estudiantes del mismo grupo se reúnen en una parte del aula. Comparten sus conocimientos, debaten, resuelven dudas y se convierten en especialistas en su tema.
- Intercambio de información: Los estudiantes regresan a sus grupos originales y se convierten en docentes de su pieza.

Ejercicio: A partir de las funcionalidades seleccionadas anteriormente.

**A. Request**: El objetivo es diseñar las llamadas request hacia el servidor para obtener datos, persistir o modificar. Por cada petición se requiere: URL, parámetros requeridos, parámetros opcionales y verbo http (GET, POST, UPDATE o DELETE).

**B. Response**: Desarrollo de la lógica de negocio. Por cada petición:	json de salida, vódigos http posibles y qué entidades de la base de datos podrían estar involucradas.

**C. Pruebas**: Desarrollo de las pruebas de las llamadas. Por cada petición hay que indicar que pruebas se realizarían indicando:  Contexto (given). Estado inicial. Acción (when). Qué se quiere probar. Resultado (then): Verificar el resultado esperado.

El grupo generará un documento pdf con el ejercicio resuelto que se enviará por correo electrónico al docente hasta el día antes de la fecha de presentación. En la clase siguiente el grupo expondrá durante 10 minutos sus funcionalidades y el desarrollo de las peticiones, pudiendo ser preguntado por el docente y los demás estudiantes.


## Autor

- [@jsilgado](https://www.github.com/jsilgado)
