## Proposito y descripcion - Ivar

## Arquitectura - Ivar

## Tecnologias - Fede

## CI - Ivar

## Casos de uso - Fede

## Conectividad Servidor - Cliente - TODO

## Deployment - TODO




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