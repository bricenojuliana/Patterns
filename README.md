# LABORATORIO 2 - PATTERNS

#### TALLER 2
##### PATTERNS - FACTORY

## PRE-RREQUISITOS
- Java OpenJDK Runtime Environment: 17.x.x
- Apache Maven: 3.9.x

## OBJETIVOS
1. Entender qué es Maven
2. Usar comandos de generación de arquetipos, compilación y ejecución de un proyecto usando Maven
3. Obtener puntos adicionales por PR qué corrijan o mejoren los laboratorios

## LA HERRAMIENTA MAVEN
La herramienta [Apache Maven](https://maven.apache.org/what-is-maven.html) se usa para gestionar y manejar proyectos de software. La base de maven para un proyecto es el concepto de un modelo de objeto de proyecto (POM), Maven puede gestionar la compilación, los informes y la documentación de un proyecto a partir de este modelo, que se concreta en el archivo `pom.xml`.

Ingresar a la página de la herramienta y entender:
- Cuál es su mayor utilidad: 
Maven proporciona una forma estandarizada y eficiente de gestionar proyectos de software. Sus principales utilidades incluyen la gestión de dependencias, la construcción de proyectos, la generación de informes, y la gestión de ciclos de vida del proyecto.
- Fases de maven:  
  Maven organiza la construcción de un proyecto en fases. Algunas de las fases más comunes incluyen:
    - validate: Valida que el proyecto es correcto y que toda la información necesaria está disponible.
    - compile: Compila el código fuente del proyecto.
    - test: Ejecuta las pruebas unitarias del proyecto.
    - package: Empaqueta el proyecto en un formato específico, como JAR o WAR.
    - install: Instala el artefacto en el repositorio local para su uso como dependencia en otros proyectos.
    - deploy: Copia el artefacto en un repositorio remoto para su distribución.
- Ciclo de vida de la construcción:  
  El ciclo de vida de construcción de Maven define las fases por las que pasa un proyecto desde su inicio hasta su finalización. Este ciclo de vida incluye tres fases principales:
    - Clean: Borra cualquier artefacto generado previamente.
    - Default (o Build): Construye el proyecto, incluyendo compilación, pruebas y empaquetado.
    - Site: Genera la documentación del proyecto y otros informes.
- Para qué sirven los plugins:  
  Los plugins en Maven son componentes que proporcionan funcionalidades adicionales al proceso de construcción del proyecto. Pueden extender las capacidades de Maven o ejecutar tareas específicas durante el ciclo de vida del proyecto. Los plugins se configuran en el archivo pom.xml del proyecto y se utilizan para realizar tareas como la ejecución de pruebas, la generación de informes, la integración con sistemas de control de versiones, entre otros.
- Qué es y para qué sirve el repositorio central de maven:  
  El Repositorio Central de Maven es un repositorio público que almacena artefactos de software Java, como bibliotecas, frameworks y utilidades, que pueden ser utilizados como dependencias en proyectos Maven. El repositorio central es la principal fuente de dependencias para los proyectos Maven y está disponible para todos los usuarios de Maven de forma gratuita. Los artefactos en el repositorio central pueden ser fácilmente referenciados en los archivos de configuración de Maven, lo que simplifica la gestión de dependencias en los proyectos.

## EJERCICIO DE LAS FIGURAS
### CREAR UN PROYECTO CON MAVEN
Buscar cómo se crea un proyecto maven con ayuda de los arquetipos (archetypes).

*Con el comando ```mvn archetype:generate```. En la ejecución se ponen los parámetros de abajo.*

Busque cómo ejecutar desde línea de comandos el objetivo "generate" del plugin "archetype", con los siguientes parámetros:
```yml
ProjectId: org.apache.maven.archetypes:maven-archetype-quickstart:1.0
Id del Grupo: edu.eci.cvds
Id del Artefacto: Patterns
Paquete: edu.eci.cvds.patterns.archetype
```

Se debió haber creado en el directorio, un nuevo proyecto `Patterns` a partir de un modelo o arquetipo, que crea un conjunto de directorios con un conjunto de archivos básicos.

Cambie al directorio `Patterns`:
```sh
$ cd Patterns
```

Para ver el conjunto de archivos y directorios creados por el comando `mvn` ejecute el comando `tree`.
```sh
$ cmd //c tree
Folder PATH listing
Volume serial number is F671-CE19
C:.
▒▒▒▒.idea
▒▒▒▒src
    ▒▒▒▒main
    ▒   ▒▒▒▒java
    ▒       ▒▒▒▒edu
    ▒           ▒▒▒▒eci
    ▒               ▒▒▒▒cvds
    ▒                   ▒▒▒▒patterns
    ▒                       ▒▒▒▒archetype
    ▒▒▒▒test
        ▒▒▒▒java
            ▒▒▒▒edu
                ▒▒▒▒eci
                    ▒▒▒▒cvds
                        ▒▒▒▒patterns
                            ▒▒▒▒archetype

```

En algunos sistemas operativos, este comando no funciona correctamente o puede requerir un parámetro (por ejemplo: `tree /f`). En caso que funcione, la
salida muestra la estructura del proyecto, similar a como se muestra a continuación:
```sh
.
│ pom.xml
└───src
├───main
│ └───java
│ └───edu
│ └───eci
│ └───cvds
│ └───patterns
  └───archetype
│ App.java
│
└───test
└───java
└───edu
└───eci
└───cvds
└───patterns
└───archetype
AppTest.java
```

## AJUSTAR ALGUNAS CONFIGURACIONES EN EL PROYECTO
Edite el archivo `pom.xml` y realize la siguiente actualización:

Hay que cambiar la version del compilador de Java a la versión 8, para ello, agregue la sección `properties` antes de la sección de
dependencias:
```xml
<properties>
  <maven.compiler.target>1.8</maven.compiler.target>
  <maven.compiler.source>1.8</maven.compiler.source>
</properties>
```
![img.png](imagenes/imagen.png)

## COMPILAR Y EJECUTAR
Para compilar ejecute el comando:
```sh
$ mvn package
```
![img_1.png](imagenes/imagen_1.png)

Si maven no actualiza las dependencias utilice la opción `-U` así:
```sh
$ mvn -U package
```

Busque cuál es el objetivo del parámetro "package" y qué otros parámetros se podrían enviar al comando `mvn`.

Busque cómo ejecutar desde línea de comandos, un proyecto maven y verifique la salida cuando se ejecuta con la clase `App.java` como parámetro en "mainClass". Tip: https://www.mojohaus.org/exec-maven-plugin/usage.html

![img_2.png](imagenes/img_2.png)

Realice el cambio en la clase `App.java` para crear un saludo personalizado, basado en los parámetros de entrada a la aplicación.


Utilizar la primera posición del parámetro que llega al método "main" para realizar elsaludo personalizado, en caso que no sea posible, se debe mantener el saludo como se encuentra actualmente:

Buscar cómo enviar parámetros al plugin "exec".

Ejecutar nuevamente la clase desde línea de comandos y verificar la salida: Hello World!

Ejecutar la clase desde línea de comandos enviando su nombre como parámetro y verificar la salida. Ej: Hello Pepito!

![img_5.png](imagenes/img_5.png)

Ejecutar la clase con su nombre y apellido como parámetro. ¿Qué sucedió?

Verifique cómo enviar los parámetros de forma "compuesta" para que el saludo se realice con nombre y apellido.

Ejecutar nuevamente y verificar la salida en consola. Ej: Hello Pepito Perez!

![img.png](imagenes/img.png)

## HACER EL ESQUELETO DE LA APLICACIÓN
Cree el paquete `edu.eci.cvds.patterns.shapes` y el paquete `edu.eci.cvds.patterns.shapes.concrete`.

![img_1.png](imagenes/img_1.png)

Cree una interfaz llamada `Shape.java` en el directorio `src/main/java/edu/eci/cvds/patterns/shapes` de la siguiente manera:
```java
package edu.eci.cvds.patterns.shapes;

public interface Shape {
    public int getNumberOfEdges();
}
```

Cree una enumeración llamada `RegularShapeType.java` en el directorio `src/main/java/edu/eci/cvds/patterns/shapes` así:

```java
package edu.eci.cvds.patterns.shapes;

public enum RegularShapeType {
    Triangle, Quadrilateral, Pentagon, Hexagon
}
```

En el directorio `src/main/java/edu/eci/cvds/patterns/shapes/concrete` cree las diferentes clases (Triangle, Quadrilateral, Pentagon, Hexagon), que implementen la interfaz creada y retornen el número correspondiente de vértices que tiene la figura. 

Siguiendo el ejemplo del triángulo:
```java
package edu.eci.cvds.patterns.shapes.concrete;

import edu.eci.cvds.patterns.shapes.Shape;

public class Triangle implements Shape {
    public int getNumberOfEdges() {
        return 3;
    }
}
```

Cree el archivo `ShapeMain.java` en el directorio `src/main/java/edu/eci/cvds/patterns/shapes` con el metodo main:
```java
package edu.eci.cvds.patterns.shapes;

public class ShapeMain {

  public static void main(String[] args) {
    if (args == null || args.length != 1) {
      System.err.println("Parameter of type RegularShapeType is required.");
      return;
    }
    try {
      RegularShapeType type = RegularShapeType.valueOf(args[0]);
      Shape shape = ShapeFactory.create(type);
      System.out.println(
        String.format(
          "Successfully created a %s with %s sides.",
          type,
          shape.getNumberOfEdges()
        )
      );
    } catch (IllegalArgumentException ex) {
      System.err.println(
        "Parameter '" + args[0] + "' is not a valid RegularShapeType"
      );
      return;
    }
  }
}
```

Analice y asegúrese de entender cada una de las instrucciones que se encuentran en todas las clases que se crearon anteriormente. Cree el archivo `ShapeFactory.java` en el directorio `src/main/java/edu/eci/cvds/patterns/shapes` implementando el patrón fábrica (Hint: https://refactoring.guru/design-patterns/catalog), haciendo uso de la instrucción switch-case de Java y usando las enumeraciones.

¿Cuál fábrica hiciste? y ¿Cuál es mejor?
Usamos Simple Factory. Dependiendo del contexto cada una tiene sus ventajas:
Simple Factory: Es el más básico de los tres. Se utiliza para crear objetos sin exponer la lógica de creación al cliente. Es útil cuando la creación de objetos no es compleja y no se espera que cambie con frecuencia. 

Factory Method: Permite a una clase delegar la responsabilidad de la creación de instancias a sus subclases. Esto proporciona una mayor flexibilidad que Simple Factory, ya que cada subclase puede proporcionar su propia implementación de cómo se crea un objeto. Es útil cuando se espera que haya varias implementaciones del mismo tipo de objeto.

Abstract Factory: Proporciona una interfaz para crear familias de objetos relacionados o dependientes sin especificar sus clases concretas. Se utiliza cuando se necesita crear múltiples objetos que están interrelacionados de alguna manera. 

- Simple Factory:

![imagen](https://github.com/PDSW-ECI/labs/assets/4140058/0788a0b7-a071-4b90-ac3f-5982289ff3b3)

- Factory Method:

![imagen](https://github.com/PDSW-ECI/labs/assets/4140058/cd82548d-347b-4a10-88bd-2d203dac12bd)
- Abstract Factory:

![imagen](https://github.com/PDSW-ECI/labs/assets/4140058/1c79a12b-21d4-46be-8f19-40f3b62b6af7)

Ejecute múltiples veces la clase ShapeMain, usando el plugin exec de maven con los siguientes parámetros y verifique la salida en consola para cada una:
- Sin parámetros
![img_6.png](imagenes/img_6.png)
- Parámetro: qwerty
![img_7.png](imagenes/img_7.png)
- Parámetro: pentagon
![img_8.png](imagenes/img_8.png)
- Parámetro: Hexagon
![img_9.png](imagenes/img_9.png)

¿Cuál(es) de las anteriores instrucciones se ejecutan y funcionan correctamente y por qué?
Se ejecuta solo la de Hexagon, porque es de los RegularShapeType definidos. Sin parmetros no se puede, son un requisito; qwerty no es un parámetro válido y pentagon tampoco, por que la *p* está en minúscula.

## ENTREGAR
- Se espera al menos que durante la sesión de laboratorio, se termine el ejercicio del saludo y haya un avance del ejercicio de las figuras.
Dentro del directorio del proyecto, cree un archivo de texto integrantes.txt con el nombre de los dos integrantes del taller.
- Crear un repositorio para este proyecto y agregar la url del mismo, como entrega del laboratorio.
- Enviar un correo con el asunto **CVDS-lab-2** a ivan.lemus@escuelaing.edu.co con la URL de su repositorio antes del comienzo del otro laboratorio.
- NOTA: Investigue para qué sirve "gitignore" y cómo se usa. Para futuras entregas, debe estar configurado.

<!-- https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax -->
