# AWS-SQS-DLQ
Este repositorio se crea para aprender cómo funciona la funcionablidad de Dead Letter Queue.



## 1. Creación de un DLQ en SQS. 

1. Primero de todo, vamos a SQS y creamos un queue. En el tipo de SQS, en este tutorial seleccionaremos el "Standard" y como nombre le daremos:

```
DemoQueueDLQ
```
2. Configuración del queue. 

-Visibility timeout: 30 segundos
- message retention period: 14 days
Al final queremos analizar los bugs, por lo que necesitamos que el mensaje esté ahi durante un buen rato.

4. Access Policies: 
Lo dejamos en basic

Entonces, en el emisor lo dejamos como "Only the queue owner". 

Y en el receptor tambien lo dejamos ocmo "Only the queue owner". 

5. Encryption: 

Loo dejamos en basic

6. Creamos el queue.

## 2. Creacion del queue en SQS: 

Ahora vamos a crear el queue que desencadenara en el DLQ: 

1. Primero de todo, vamos a SQS y creamos un queue. En el tipo de SQS, en este tutorial seleccionaremos el "Standard" y como nombre le daremos:

```
DemoQueue
```
2. Configuración del queue. 

-Visibility timeout: 5 segundos,para que se reproduzca muy rápido.
- message retention period: 4 days
Al final queremos analizar los bugs, por lo que necesitamos que el mensaje esté ahi durante un buen rato.

4. Access Policies: 
Lo dejamos en basic

Entonces, en el emisor lo dejamos como "Only the queue owner". 

Y en el receptor tambien lo dejamos ocmo "Only the queue owner". 

5. Encryption: 

Loo dejamos en basic

6. Dead letter queue: 

Enable, para que se pueda enlazar una cosa con la otra.

'Choose a dead-letter queue'

Elegimos a dedo el que acabamos de crear. 

En el Maximum receives: tenemos que tener en cuenta en nuestro problema cuantas veces se podra recrear el bug, para que podamos mandar un mensaje al DLQ. 
Nosotros, lo dejamos en un 3.


6. Creamos el queue.

## Lo ponemos en práctica: 

1. Voy a  mi DLQ y le doy a "Receive ans send messages" y abajo a "Poll Messages". Commo resultado no deberia de tener nada. 
2. Voy a mi queue bueno y en "Receive and send messages", escribo un mensaje: 

```
hello world, poison pill
```
Le damos a Send Message 

Abajo en Receive messages, le damos a "Poll for messages", y vemos que este mensaje ha llegado. 

Va a lelgar una vez y la cantidad va a poner 1. 
A los 3 segundos, volvera a llegar y la cantidad sera 2, 
A los 3 segundos, volvera a llegar y la cantidad sera 3, 
pero a los 3 segundos no llegara, es mas desaparecera el aviso. 

Vuelvo a mi SQS pero del DLQ, y le doy a "Poll for messages". Entonces, ahñi vere donde se genera el mensaje del SQS sano, pero por 4 vez o las vecs que sean. 


