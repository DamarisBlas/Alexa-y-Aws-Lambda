![Logo](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4a/Amazon_Alexa_logo.svg/2560px-Amazon_Alexa_logo.svg.png)
# Alexa skill y AWS Lambda

En este proyecto se creo una una habilidad de Alexa (Skill) personalizada junto con su backend en AWS Lambda. La Skill ayudara a memorizar preguntas de la materia de arquitectura del software. 


## 🛠 ¿Qué se necesita?
- Cuenta en Amazon developer 
- Cuenta en AWS



## ¿Cómo funciona?
Al igual que en la programación de una pagina web. Existe el backend y frontend. Pero la parte de frontend no sera visible para el usuario sino sera una interfaz de voz.

- **Frontend :** La skill que se armara desde la pagina de Amazon-developer
- **Backend :** Funcion AWS lambda
![foto1](https://i.postimg.cc/Vkz0gr8r/Descricpcion.png)  
    
#### Diagrama de la arquitectura
El usuario hablara y todo lo que este diga sera escuhado por el dispositivo Alexa. Esta informacion se llevara al Alexa Voice Service donde se encargara de tranformar lo que dijo el usuario en texto. Alexa skill se encargara dar un significado a este texto, por ejemplo si un usuario dice "Alexa, divide 10 entre 2" en Alexa Skill se definira que el texto ira al Intent DividirIntent tambien en Alexa Skill se configurara todas las posibles oraciones que podria decir el usuario por ejemplo "Alexa divide 10 entre 2, hazme la division de 10 entre 2, dividir 10 entre 2" y por ultimo Aws lambda es en donde se da la funcionalidad, todo el calculo que se necesita se hara en esta seccion. 

![foto2](https://i.postimg.cc/pLkh6WW0/arquitectura-D.png)  
    

## Pasos para crear una Skill de Alexa
Todo esto es desde la web de Amazon-developer
- Crear el nombre de invocacion  

![Foto3](https://i.postimg.cc/XYsFvTHD/paso1.png)
- Añadir los Intents que sea necesario
![Foto4](https://i.postimg.cc/d0DCZ4gQ/paso2.png)
  
## Codigo principal en el lambda de AWS
Con este codigo va a dar como resultado la cantidad de preguntas que desea el usuario
 
```javascript
const IniciarHandler = {
  canHandle(handlerInput) {
    const request = handlerInput.requestEnvelope.request;
    return request.type === 'IntentRequest'
      && request.intent.name === 'Iniciar';
      //Iniciar es el nombre del Inten que dimos en el paso anterior
  },
  handle(handlerInput) {
    const requestAttributes = handlerInput.attributesManager.getRequestAttributes();
    const cantidadPreguntas =  handlerInput.requestEnvelope.request.intent.slots.CantidadPreguntasSlot.value;
    //Se captura el valor que dijo el usuario
    var cantidad;
    let p=[];
    if (cantidadPreguntas != undefined){
      cantidad = cantidadPreguntas;
     console.log('La cantidad de preguntas es: ' + cantidad);
     for (var i = 0; i < cantidad; i++) {
       let randomFact = requestAttributes.t('FACTS');
       //Se crea una pregunta aleatoria 
       let nuevo = p.push(randomFact)
               }
    }
    return handlerInput.responseBuilder
      .speak("Aca tienes tus "+cantidad+" preguntas para memorizar    "+p)
      //Respuesta que se dara al usuario
      .reprompt() 
      .getResponse();
  },
};

//Donde se tiene las preguntas
const esData = {
  translation: {
    SKILL_NAME: 'Preguntas para el examen de arquitectura',
    GET_FACT_MESSAGE: 'Aquí está tu pregunta: ',
    HELP_MESSAGE: 'Puedes decir dime una pregunta para repasar para tu examen o puedes decir salir... Cómo te puedo ayudar?',
    HELP_REPROMPT: 'Como te puedo ayudar?',
    FALLBACK_MESSAGE: 'La skill preguntas  no te puede ayudar con eso.  Te puede ayudar a descubrir curiosidades sobre el espacio si dices dime una curiosidad del espacio. Como te puedo ayudar?',
    FALLBACK_REPROMPT: 'Como te puedo ayudar?',
    ERROR_MESSAGE: 'Lo sentimos, se ha producido un error.',
    STOP_MESSAGE: 'Adiós!',
    FACTS:
        [
          
          'El comando que se utiliza para detener un contenedor en Docker es     DOCKER STOP',
          'El comando para crear un contenedor a partir de una imagen en Docker es    DOCKER BUILD',
          'DOCKERFILE es   un archivo de texto que define cómo construir una imagen Docker',
          'Mediante un volumen Docker se comparte información entre un contenedor y el sistema anfitrión',
          'Una imagen de docker es  una plantilla de sistema de archivos y configuración para la creación de contenedores',
          'El comando que se utiliza para listar los contenedores en ejecución en Docker es   DOCKER PS',
        ],
    RESONDER:[
      'El comando que se utiliza para detener un contenedor en Docker +DockerStop',
      'El comando para crear un contenedor a partir de una imagen en Docker es  +DOCKER BUILD',
          'Es   un archivo de texto que define cómo construir una imagen Docker +DOCKERFILE',
          'Mediante que se comparte información entre un contenedor y el sistema anfitrión +volumen',
          'Que es  una plantilla de sistema de archivos y configuración para la creación de contenedores +Imagen',
          'El comando que se utiliza para listar los contenedores en ejecución en Docker es +DOCKERPS',
      ],
  },
};
```



## Demo

![foto5](https://i.postimg.cc/y6thH4g1/demo.png)



### ¿Quieres saber mas sobre Skills de Alexa? 👋
Te recomiendo entrar a estos links 
 - [Alexa Skills Desde Cero](https://www.udemy.com/share/101zoC3@YU0t38kYWM2OKc3HQafPCVF4e_OiL34kuIOZswAVeb2mM8RtkGH2oAkr_R3TZVtR/)
 - [Amazon developer](https://developer.amazon.com/alexa)




## Autor

- [@damarisblas](https://www.github.com/damarisblas)
