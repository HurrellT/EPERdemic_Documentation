## Proposito

Durante la cursada de la materia 'Estrategias de Persistencia' en la universidad de Quilmes, se les presenta a los alumnos un trabajo practico de varias iteraciones a resolver.
Este trabajo practico consta de un enunciado en el que se presentan las interfaces de multiples servicios, y los alumnos dan practica a la teoria de la materia, haciendo
implementacion de estos servicios que interactuan tanto con la capa de modelo de la aplicacion como la capa de persistencia.

Sin embargo, una problematica recurrente es la dificultad de comprension por parte de los alumnos de como encajaria el trabajo que estan haciendo dentro de una aplicacion de uso real.

Con Eperdemic nos proponemos darle una solucion a esa problematica, dando realmente un uso real a esos trabajos practicos; proveyendo un servidor con una capa de presentacion real,
a la cual los alumnos pueden conectarse desde sus computadoras con sus trabajos practicos, ver como el flujo de datos llega hasta el service que estuvieron trabajando para implementar, 
y tambien ver como los datos que estan manejando en sus TPs interactuan con los datos que otros alumnos estan manejando en sus otros TPS al estar conectados al mismo servidor.

## Arquitectura 

<p align="center">
  <img src="Arquitectura.png" />
</p>

La aplicacion esta dividida en dos grandes partes, una parte de clientes y una de servidor.
A grandes rasgos,  los clientes estan conformados por los trabajos practicos de los alumnos, a los cuales ya se les provee un proyecto con la capa de controladores armada, lista para
interactuar con la capa de servicios y recibir informacion del servidor. 

Recordemos que la capa de servicios y las bases de datos no estarian implementadas, ya que es el trabajo que deberian realizar los alumnos para completar sus trabajos practicos.  
Sin embargo, una vez completada su implementacion, los controladores ya estarian listos para que se pueda llevar a cabo la coneccion e interaccion con el servidor principal.

Cuando se corre el proyecto, este realizaria un pedido de subscripcion al servidor, para poder comenzar con la interaccion entre ambas partes.

El servidor recibe este pedido, y asignaria un identificador al cliente, de tal manera que cada cliente pueda acceder y realizar pedidos a su propio backend.
Asi mismo, el servidor tendria un area publica en la cual se mostrarian datos de todos los clientes, y de necesitarse se podrian realizar operaciones que impacten sobre todos los clientes tambien.

Por ultimo, el servidor de querer realizar operaciones con todos los datos de los clientes, o de necesitar realizar permutaciones de datos mas complejas, contaria con su propio backend, con el cual podria interactuar
y llevar a cabo esas operaciones.



## Repositorios
Actualmente existen 3 repositorios distintos

Cliente
Existen dos repositorios de cliente, uno publico y otro privado de pruebas. Nos hace falta tener otro repositorio privado de pruebas, ya que para testear que el servidor se comporta
como esperamos, necesitamos implementar los trabajos practicos nosotros y ver que las pruebas de integracion son exitosas. Obviamente, de ser publico este repositorio los alumnos 
podrian copiarse y eso derrotaria la razon de ser del trabajo practico.

Repositorio de cliente publico:
https://github.com/fedes112/EPERdemic_Controllers

Repositorio de cliente privado y de pruebas:
https://github.com/EPERS-UNQ/TP_EPERDEMIC

Repositorio de servidor
https://github.com/fedes112/EPERdemic_Frontend


## Tecnologias - Fede

## CI - Ivar

## Casos de uso - Fede

## Conectividad Servidor - Cliente - TODO

## Deployment - TODO

## TODO Actualizar Trello


Tarea:
Como usuario quiero poder crear un agente patógeno

1er paso:

En el template, el usuario ingresa el nombre del nuevo patógeno que desea crear en el form definido en el Hook Formulary (form.js).

-----------------

function Formulary() {
    const [pathogen,setPathogen] = useState();
    const {
         register, handleSubmit
      } = useForm();
    const [submitPathogen, setSubmitPathogen] = useState(false);
    const sendPathogen = (usePost)('/patogeno', pathogen);


    useEffect(() => {
        if (!submitPathogen) return;
        sendPathogen();
        console.log(pathogen);
        setSubmitPathogen(false);
    }, [submitPathogen]);

    const handleSendPathogen = data => {
        setPathogen({ ...pathogen, nombre: data.name });
        setSubmitPathogen(true);
        console.log(data);
    };

  
    return ( 
       <Container fluid>
            <Card className="text-center">
                <Card.Header></Card.Header>
                <Card.Body>
                <Form onSubmit={ 
                                handleSubmit(handleSendPathogen)
                                }>
                                <Form.Group>
                                    <Form.Label className="alert alert-danger" role="alert">Nombre Agente Patógeno</Form.Label>
                                    <Form.Control ref= {register} name ='name' placeholder="" />
                                </Form.Group>
                                <Button variant="primary" type="submit">
                                Submit
                                </Button>
                            </Form>
                    <Card.Title></Card.Title>
                </Card.Body>
                <Card.Footer className="text-muted"></Card.Footer>
            </Card>
        </Container> 
    );
    
};

---------------


El json que se manda por medio de un método POST(API REST) a traves de axios el cual se utiliza en el hook usePost(useFetch.js) le llega 
a nuestro PatogenoControllerREST el cual tiene un método definido para interceptar 
dicho envío de datos .


@ServiceREST
@RequestMapping("/patogeno")
class PatogenoControllerREST(private val patogenoService: PatogenoService) {

  @PostMapping
  fun create(@RequestBody patogeno: Patogeno): ResponseEntity<Int> {
    val patogenoId = patogenoService.crearPatogeno(patogeno)
    return ResponseEntity(patogenoId, HttpStatus.CREATED)
  }


Este PatogenoControllerREST tomara los datos necesarios del body que recibe y
mandara un mensaje a su colaborador interno del tipo PatogenoService.

Dicho service debe implementar los respectivos métodos de la interfaz:

interface PatogenoService {
    fun crearPatogeno(patogeno: Patogeno): Int
    fun recuperarPatogeno(id: Int): Patogeno
    fun recuperarATodosLosPatogenos(): List<Patogeno>
    fun agregarEspecie(id: Int, nombreEspecie: String, paisDeOrigen : String) : Especie
}

El patógeno service mandara a su colaborador interno del tipo PatogenoDAO 
el mensaje crear para que este impacte a la base datos y se inserte un nuevo
patógeno en la base de datos que se esté utilizando, el colaborador interno 
puede responder a la interfaz que PatogenoDao que implementa

interface PatogenoDAO {
    fun crear(patogeno: Patogeno)
    fun actualizar(patogeno: Patogeno )
    fun recuperar(idDelPatogeno: Int): Patogeno
    fun recuperarATodos() : List<Patogeno>
}




-----
Prueba de concepto 


Vamos a cumplir con el objetivo del tp de jdbc.....