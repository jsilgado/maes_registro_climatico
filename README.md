# Registro climático

Situación de aprendizaje.
Se creará una aplicación de consulta de datos del clima de diferentes países a lo largo de diversos años. Tratamiento de la información para comprobar los aumentos de temperaturas en los diferentes países y su progresión.

## Actividad 1 - Creación del proyecto

- Crea un proyecto spring boot utlizando https://start.spring.io/ con las siguientes características:
```bash
Proyect: Maven
Languaje: Java
Spring boot: 3.2.2
Dependencies: Spring Web Lombok
```

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




## Autor

- [@jsilgado](https://www.github.com/jsilgado)
