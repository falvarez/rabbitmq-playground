# RabbitMQ playground

Código para implementar los tutoriales de RabbitMQ: https://www.rabbitmq.com/getstarted.html

Documentación Docker RabbitMQ: https://hub.docker.com/_/rabbitmq/

Arrancar RabbitMQ dockerizado: ./startrabbit.sh

Consola web: http://localhost:8080/#/

Instancia RabbitMQ: localhost:5672

## Notas sobre RPC

(referencia: https://www.rabbitmq.com/tutorials/tutorial-six-php.html)

* Si se puede, mejor evitar RPC. Mejor usar un pipeline asíncrono.
* El resultado de las RPC debe ser (idealmente) idempotente. Esto es porque el servidor se puede morir después de devolver el resultado pero antes de devolver el ACK, por lo que la RPC se volverá a procesar al rearrancar el servidor. Es por esto que el cliente también debe simplemente ignorar las respuestas cuyo `correlation_id` desconozca.

Cuestiones a considerar en la implementación:

* ¿Cómo debe reaccionar el cliente si no hay servidores disponibles?
* ¿Debería definirse un `timeout`?
* Si se produce algún error en el servidor y se lanza una excepción, ¿debería enviarse al cliente?
* Añadir protección para mensajes de cliente mal formados.

