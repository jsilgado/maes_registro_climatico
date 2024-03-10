# Registro climático

Situación de aprendizaje.
Se creará una aplicación de consulta de datos del clima de diferentes países a lo largo de diversos años. Tratamiento de la información para comprobar los aumentos de temperaturas en los diferentes países y su progresión.

![image](https://img.shields.io/badge/Spring_Boot-F2F4F9?style=for-the-badge&logo=spring-boot)
![image](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)
![image](https://img.shields.io/badge/json-5E5C5C?style=for-the-badge&logo=json&logoColor=white)
![image](https://img.shields.io/badge/Eclipse-2C2255?style=for-the-badge&logo=eclipse&logoColor=white)
![image](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=Postman&logoColor=white)
![image](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)

## Actividad 1 - Creación del proyecto

- Crea un proyecto spring boot utlizando https://start.spring.io/ con las siguientes características:
```bash
Proyect: Maven
Languaje: Java
Spring boot: 3.2.3
Dependencies: Spring Web, Lombok
```
![App Screenshot](https://github.com/jsilgado/maes_registro_climatico/blob/master/images/Spring%20Initializr.png)

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

## Actividad 2 - Modelado de datos
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

## Autor

- [@jsilgado](https://www.github.com/jsilgado)
