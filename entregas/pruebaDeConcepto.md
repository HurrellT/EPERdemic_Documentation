# Prueba de Concepto

## Funcionalidades

Como prueba de concepto decidimos realizar una pequeña demostracion, la cual consistia en que mostrar la funcionalidad global de la aplicacion.
Para eso tomamos como caso de uso la capacidad de crear un Patogeno (solo con el nombre) y la capacidad de poder ver todos los patogenos creados por todos los clientes.

Se consiguio lo propuesto siguiendo la arquitectura descripta en el home de esta wiki; muy resumido, la aplicacion frontend dispara contra localhome para comunicarse con el servidor cliente
(el grupo de alumnos corriendo su TP) y mantiene comunicacion con un servidor backend hosteado aparte con quien hace la conciliacion de datos de todos los diferentes clientes locales.

## Casos de uso

<p align="center">
  <img src="cdu_concepto.png" />
</p>

`Como Usuario quiero poder crear un agente patógeno.`

El usuario ingresa el nombre de un patogeno en un textbox, este se envia tanto al cliente del usuario como al backend externo.


`Como Usuario quiero poder recuperar todos los agentes patógenos y poder ver tanto los creados por mi, como los creados por los otros usuarios. `

La aplicacion de frontend hace un pooling constante de los datos en el servidor backend, de tal forma de poder visualizar todos los patogenos creados.
