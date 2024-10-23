Tutorial: Uso de Tópicos y JSON en MQTT para Control de Básculas Modbus
Este tutorial te guiará a través del uso de tópicos MQTT y los formatos JSON asociados para realizar operaciones de lectura de peso, dosificación, cero (tarar), hacer tara y leer la tara en un sistema de básculas que se comunican utilizando Modbus.

1. Lectura del Peso
El sistema publica continuamente el peso de cada báscula en su respectivo tópico MQTT. Este proceso ocurre de manera automática, y no necesitas enviar comandos para que ocurra.

Tópico de Publicación:
bash
Copiar código
sensorica/bascula/peso/{direccion}
{direccion}: La dirección Modbus de la báscula (rango permitido: 2 a 7).
Formato JSON del Payload:
json
Copiar código
{
  "value": <peso_neto_en_kg>
}
value: Contiene el peso neto de la báscula en kilogramos.
Ejemplo:
Para una báscula en la dirección Modbus 3, el sistema publicará en el tópico:

bash
Copiar código
sensorica/bascula/peso/3
Con un payload como:

json
Copiar código
{
  "value": 123.4
}
Esto indica que el peso leído es de 123.4 kg.

2. Dosificación
La dosificación permite iniciar el proceso en la báscula para alcanzar un valor de peso específico.

Tópico de Publicación:
bash
Copiar código
sensorica/bascula/dosifica/{direccion}
{direccion}: La dirección Modbus de la báscula.
Formato JSON del Payload:
json
Copiar código
{
  "value": <peso_objetivo_en_gramos>
}
value: El peso objetivo que deseas alcanzar en gramos.
Ejemplo:
Para iniciar una dosificación en la báscula con dirección Modbus 4 y un objetivo de 50.0 kg, debes publicar el siguiente JSON en el tópico:

bash
Copiar código
sensorica/bascula/dosifica/4
Con el siguiente payload:

json
Copiar código
{
  "value": 50000
}
Esto ordena a la báscula comenzar una dosificación para alcanzar los 50.0 kg.

3. Hacer Cero (Tarar)
Este comando se utiliza para ajustar la báscula a cero, eliminando cualquier peso que pueda estar presente en el momento.

Tópico de Publicación:
bash
Copiar código
sensorica/bascula/zero/{direccion}
{direccion}: La dirección Modbus de la báscula.
Formato JSON del Payload:
json
Copiar código
{
  "value": true
}
value: Debe ser true para ejecutar el comando de cero.
Ejemplo:
Para ajustar a cero la báscula con dirección Modbus 2, publica el siguiente JSON en el tópico:

bash
Copiar código
sensorica/bascula/zero/2
Con el siguiente payload:

json
Copiar código
{
  "value": true
}
Esto ajustará la báscula a cero.

4. Hacer Tara
Este comando se utiliza para registrar el valor actual del peso como tara.

Tópico de Publicación:
bash
Copiar código
sensorica/bascula/tara/{direccion}
{direccion}: La dirección Modbus de la báscula.
Formato JSON del Payload:
json
Copiar código
{
  "value": true
}
value: Debe ser true para ejecutar el comando de tara.
Ejemplo:
Para ejecutar una tara en la báscula con dirección Modbus 5, publica el siguiente JSON en el tópico:

bash
Copiar código
sensorica/bascula/tara/5
Con el siguiente payload:

json
Copiar código
{
  "value": true
}
Esto registrará el peso actual como tara.

5. Leer el Valor de la Tara
Este comando solicita la lectura del valor de tara almacenado en la báscula.

Tópico de Publicación:
bash
Copiar código
sensorica/bascula/tara/{direccion}
{direccion}: La dirección Modbus de la báscula.
Formato JSON del Payload para Solicitar la Tara:
json
Copiar código
{
  "read": true
}
read: Debe ser true para solicitar la lectura de la tara.
Formato JSON del Payload de Respuesta:
json
Copiar código
{
  "tara": <valor_tara_en_kg>
}
tara: Contiene el valor de la tara en kilogramos.
Ejemplo:
Para solicitar el valor de la tara en la báscula con dirección Modbus 6, publica el siguiente JSON en el tópico:

bash
Copiar código
sensorica/bascula/tara/6
Con el siguiente payload:

json
Copiar código
{
  "read": true
}
Después de enviar este mensaje, el sistema publicará el valor de la tara en el mismo tópico:

bash
Copiar código
sensorica/bascula/tara/6
Con el siguiente payload de respuesta:

json
Copiar código
{
  "tara": 20.5
}
Esto indica que la tara registrada es de 20.5 kg.

Resumen de Tópicos y JSON
Operación	Tópico Base	Payload de Solicitud	Payload de Respuesta
Lectura de Peso	sensorica/bascula/peso/{direccion}	N/A	{ "value": <peso_en_kg> }
Dosificación	sensorica/bascula/dosifica/{direccion}	{ "value": <peso_en_gramos> }	N/A
Hacer Cero	sensorica/bascula/zero/{direccion}	{ "value": true }	N/A
Hacer Tara	sensorica/bascula/tara/{direccion}	{ "value": true }	N/A
Leer Tara	sensorica/bascula/tara/{direccion}	{ "read": true }	{ "tara": <valor_tara_en_kg> }
Conclusión
Este tutorial te proporciona toda la información necesaria para interactuar con tu sistema de básculas a través de MQTT utilizando distintos comandos como lectura de peso, dosificación, hacer cero, hacer tara y leer la tara. Asegúrate de ajustar los valores en gramos o kilogramos según se requiera en cada operación, y utiliza los tópicos correspondientes según la dirección Modbus de cada báscula.
