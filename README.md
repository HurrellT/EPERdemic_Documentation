<p align="center">
  <img src="Icono.jpg" />
</p>

## Proposito

Durante la cursada de la materia `Estrategias de Persistencia` en la universidad de Quilmes, se les presenta a los alumnos un trabajo practico de varias iteraciones a resolver.
Este trabajo práctico consta de un enunciado en el que se presentan las interfaces de múltiples servicios, y los alumnos dan práctica a la teoría de la materia, haciendo
implementación de estos servicios que interactúan tanto con la capa de modelo de la aplicación como la capa de persistencia.

Sin embargo, una problemática recurrente es la dificultad de comprensión por parte de los alumnos de cómo encajaría el trabajo que están haciendo dentro de una aplicación de uso real.

Con Eperdemic nos proponemos darle una solución a esa problemática, dando realmente un uso real a esos trabajos prácticos; proveyendo un servidor con una capa de presentación real,
a la cual los alumnos pueden conectarse desde sus computadoras con sus trabajos prácticos, ver como el flujo de datos llega hasta el service que estuvieron trabajando para implementar,
y también ver como los datos que están manejando en sus TPs interactúan con los datos que otros alumnos están manejando en sus otros TPS al estar conectados al mismo servidor.

## Arquitectura

<p align="center">
  <img src="Arquitectura.png" />
</p>

La aplicación está dividida en dos grandes partes, una parte de clientes y una de servidor.
A grandes rasgos, los clientes están conformados por los trabajos prácticos de los alumnos, a los cuales ya se les provee un proyecto con la capa de controladores armada, lista para interactuar con la capa de servicios y recibir información del servidor.

Recordemos que la capa de servicios y las bases de datos no estarian implementadas, ya que es el trabajo que deberían realizar los alumnos para completar sus trabajos prácticos.  
Sin embargo, una vez completada su implementación, los controladores ya estarían listos para que se pueda llevar a cabo la conexión e interacción con el servidor principal.

El servidor web esta configurado para que todos los pedidos de comunicacion con el cliente se realizen a travez de llamadas a localhost, de tal manera que cada alumno corriendo su TP en su maquina va a ver como el frontEnd interactua con su backend.

Como se logra la interaccion entre todos los TPS entonces?

El frontend dispone de un área pública en la cual se mostrarán datos de todos los diferentes clientes. Esto se logra con la utilizacion de un servidor backend que sirve para conciliar los datos de todos los clientes en comunicacion, y con el cual el frontend se comunica para para visualizar esta data.

## Repositorios

Actualmente existen 4 repositorios distintos; repo de servidor frontend, repo de servidor backend, repo de cliente público, y repo de cliente privado de pruebas. Nos hace falta tener un repositorio privado de pruebas, ya que para testear que el servidor se comporta
como esperamos, necesitamos implementar los trabajos prácticos nosotros y ver que las pruebas de integración son exitosas. Obviamente, de ser público este repositorio los alumnos
podrían copiarse y eso derrotaría la razón de ser del trabajo práctico.

- [Repositorio de cliente publico](https://github.com/fedes112/EPERdemic_Controllers)

- [Repositorio de cliente privado y de pruebas](https://github.com/EPERS-UNQ/TP_EPERDEMIC)

- [Repositorio de servidor frontend](https://github.com/fedes112/EPERdemic_Frontend)

- [Repositorio de servidor backend](https://github.com/Dominikowivan/EPERdemic_Backend)

## Tecnologias

- **[React](https://reactjs.org/docs/getting-started.html):** para el desarrollo del frontend utilizamos React (biblioteca escrita en JavaScript), facilita la creación de componentes interactivos y reutilizables.
- **[Spring](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/index.html):** Como framework para el desarrollo de la aplicación por todas las herramientas que disponibiliza para facilitar el "cableado" entre las capas de servicios y controllers, simplificación de sintaxis y orquestado de la arquitectura backend.
- **[Kotlin](https://kotlinlang.org/docs/reference/):** Utilizamos Kotlin como el lenguaje de nuestro backend por su flexibilidad como lenguaje, su integración con Spring y por estar montado sobre la JVM (siendo Java un lenguaje al que estamos acostumbrados).
- **SQL DB:** A priori utilizamos como Base de Datos SQL Server tal y como hacemos en la mayoría de los casos en la materia Estrategias de Persistencia (podríamos por ej variar y usar MariaDB, Postgres, etc).
- **[NodeJs](https://nodejs.org/en/docs/):** El servidor web estará montado sobre nodejs sobre su compatibilidad con proyectos react, su amplia documentación y la gran mayoría de los problemas recurrentes ya se encuentran resueltos.

## CI

Como herramienta de integracion continua estamos utilizando [GitHub Actions](https://github.com/features/actions) por su facilidad de uso, configuración e integración con el repositorio.

## Conectividad Servidor - Cliente

El servidor front realiza toda su comunicacion con el cliente a travez de llamadas HTTP Rest a localhost, siendo la primera llamada un pedido de nombre del grupo al backend para poder asi indexar toda la data que venga de este cliente en el backend con el nombre del grupo. A partir de ese momento, el front hace un Pulling continuo de la data en el servidor backend para enriqueser la data presentada en el area de informacion global de la aplicacion.
Para mantener el servidor backend y el servidor cliente sincronizados, el servidor frontend se asegura de que cada vez que envie data de importancia al servidor cliente, esta se replique en el servidor backend.

## Deployment

Como host y herramienta de deeployment estamos usitlizando [Zeit](https://zeit.co/) para el frontend y [Heroku](https://www.heroku.com) para el backend. Tomas la decision de utilizar diferentes host, ya que cada una de estas herramientas tiene su propia especialidad, que facilita su uso si se utiliza para ese proposito, siendo el de Zeit las aplicaciones nodeJS que usan react, y el de Heroku aplicaciones backend en general.

## Entregas

- [Prueba de concepto](entregas/pruebaDeConcepto.md)
- [Entrega 1](entregas/entrega1.md)
- [Entrega 2](entregas/entrega2.md)
- [Entrega 3 ](entregas/entrega3.md)
- [Entrega 4 ](entregas/entrega4.md)
