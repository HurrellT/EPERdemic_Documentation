# Entrega 2

## Funcionalidades

La meta para la entrega 2 era tener una primera versión del simulador andando. Qué queremos decir con esto? Poder tener algo que juegue y
simule efectivamente el enunciado planteado.

Para poder realizar esto, necesitamos poder crear y visualizar las especies, y poder crear en el backend ubicaciones que tengan vectores que nos permitan contagiar las diferentes especies de patógenos que vamos creando, y 
un mecanismo para que estas se vayan esparciendo a través de las locaciones y los vectores en ellas.

Implementamos toda la lógica de backend para que los vectores se puedan contagiar entre sí y se puedan mover entre locaciones.
Cómo se contagian los vectores? Hay dos formas. 

Una es a través de un pedido de "expansión" en la locación.
Este pedido de expansión toma un vector infectado random de la locación y este vector intenta contagiar a todos los otros vectores presentes en la misma locación.

La otra es a través del movimiento de los vectores. Cuando un vector se mueve a otro lugar, este intenta contagiar a todos los vectores presentes en su nueva locación.

Una vez hecho esto, desde el frontend, se hacen pedidos al backend para que se tomen vectores random, y se muevan a lugares random (para poder ir esparciendo la especie patógena a otras locaciones)
Y tambien se hacen pedidos para "expandir" en todas las locaciones.


## Capa de presentacion Entrega 1

<p align="center">
  <img src="entrega2front.png" />
</p>

## Casos de uso

<p align="center">
  <img src="cdu_concepto.png" />
</p>

`Como Usuario quiero poder crear un agente patógeno.`

El Agente patógeno deberá tener un nombre, y debe de ser posible configurar sus atributos.
De ser Exitosa la creación del patógeno, se debería ver un feedback de que lo fue, de no serlo, deberá haber un feedback de ese error.


`Como Usuario quiero poder recuperar todos los agentes patógenos creados por mi`

Se recuperan todos los agentes patógenos persistidos en el backend y se le muestran al usuario. Si por alguna razón no se puede realizar esta recuperación, dar feedback al usuario.

`Como Usuario quiero poder crear una especie para un Patógeno en una ubicación elegida`
Se debe poder seleccionar un patógeno, mostrar y seleccionar uno de las múltiples locaciones disponibles, y enviar un pedido de creación de la especie para el patógeno seleccionado al cliente backend.
De ser exitoso o no, se debe poder mostrar un feedback al usuario.
Cuando se crea una especie en la ubicación seleccionada, se toma un vector random y se lo mueve a una locación random.

`Como Usuario quiero poder ver la información de las especies creadas para un patógeno`
Dada una lista de patógenos, se debe poder visualizar todas las especies pertenecientes a ese patógeno, y ver también su información

`Como Sistema quiero poder tomar un vector random y moverlo a una ubicación random en un intervalo dado`
De esta manera, los vectores infectados pueden empezar a exparsise a través de las diferentes locaciones.

`Como Sistema quiero poder hacer un pedido de expansión masiva al backend`
De esta manera, los vectores infectados en cada locación comienzan a expandir sus infecciones.



