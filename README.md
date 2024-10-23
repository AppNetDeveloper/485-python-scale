Control de Básculas Modbus a través de MQTT
Este repositorio permite la comunicación y control de básculas utilizando Modbus y MQTT. A continuación, se detallan los diferentes tópicos y formatos JSON necesarios para interactuar con las básculas en operaciones de lectura de peso, dosificación, cero (tarar), hacer tara y leer el valor de la tara.

1. Lectura del Peso
El sistema publica continuamente el peso de cada báscula en su respectivo tópico MQTT.

Tópico de Publicación:
bash
Copiar código
sensorica/bascula/peso/{direccion}
{direccion}: Dirección Modbus de la báscula (rango: 2 a 7).
Formato del Payload (JSON):
json
Copiar código
{
  "value": <peso_neto_en_kg>
}
value: Peso neto de la báscula en kilogramos.
Ejemplo:
Para la báscula en la dirección Modbus 3, el sistema publicará en el tópico:

bash
Copiar código
sensorica/bascula/peso/3
Con el payload:

json
Copiar código
{
  "value": 123.4
}
2. Dosificación
Este comando permite iniciar el proceso de dosificación en una báscula para alcanzar un peso objetivo específico.

Tópico de Publicación:
bash
Copiar código
sensorica/bascula/dosifica/{direccion}
{direccion}: Dirección Modbus de la báscula.
Formato del Payload (JSON):
json
Copiar código
{
  "value": <peso_objetivo_en_gramos>
}
value: El peso objetivo que deseas alcanzar en gramos.
Ejemplo:
Para iniciar la dosificación en la báscula 4 con un objetivo de 50.0 kg:

bash
Copiar código
sensorica/bascula/dosifica/4
Con el payload:

json
Copiar código
{
  "value": 50000
}
3. Hacer Cero (Tarar)
Este comando ajusta la báscula a cero, eliminando el peso actual.

Tópico de Publicación:
bash
Copiar código
sensorica/bascula/zero/{direccion}
{direccion}: Dirección Modbus de la báscula.
Formato del Payload (JSON):
json
Copiar código
{
  "value": true
}
Ejemplo:
Para hacer cero en la báscula con dirección Modbus 2:

bash
Copiar código
sensorica/bascula/zero/2
Con el payload:

json
Copiar código
{
  "value": true
}
4. Hacer Tara
Este comando registra el peso actual como tara.

Tópico de Publicación:
bash
Copiar código
sensorica/bascula/tara/{direccion}
{direccion}: Dirección Modbus de la báscula.
Formato del Payload (JSON):
json
Copiar código
{
  "value": true
}
Ejemplo:
Para ejecutar una tara en la báscula 5:

bash
Copiar código
sensorica/bascula/tara/5
Con el payload:

json
Copiar código
{
  "value": true
}
5. Leer el Valor de la Tara
Este comando solicita la lectura del valor de la tara actual.

Tópico de Publicación:
bash
Copiar código
sensorica/bascula/tara/{direccion}
{direccion}: Dirección Modbus de la báscula.
Formato del Payload para Solicitar la Tara (JSON):
json
Copiar código
{
  "read": true
}
Formato del Payload de Respuesta (JSON):
json
Copiar código
{
  "tara": <valor_tara_en_kg>
}
Ejemplo:
Para leer el valor de la tara de la báscula 6:

bash
Copiar código
sensorica/bascula/tara/6
Con el payload:

json
Copiar código
{
  "read": true
}
La respuesta en el mismo tópico sería:

json
Copiar código
{
  "tara": 20.5
}
Resumen de Tópicos y JSON
Operación	Tópico Base	Payload de Solicitud	Payload de Respuesta
Lectura de Peso	sensorica/bascula/peso/{direccion}	N/A	{ "value": <peso_en_kg> }
Dosificación	sensorica/bascula/dosifica/{direccion}	{ "value": <peso_en_gramos> }	N/A
Hacer Cero	sensorica/bascula/zero/{direccion}	{ "value": true }	N/A
Hacer Tara	sensorica/bascula/tara/{direccion}	{ "value": true }	N/A
Leer Tara	sensorica/bascula/tara/{direccion}	{ "read": true }	{ "tara": <valor_tara_en_kg> }
Contribuciones
Si deseas contribuir a este repositorio, por favor realiza un fork y envía un pull request con tus cambios o sugerencias.

Licencia
Este proyecto está bajo la licencia MIT. Consulta el archivo LICENSE para más detalles.

Este README está listo para ser utilizado en tu repositorio GitHub, brindando una clara explicación sobre cómo interactuar con las básculas a través de MQTT y Modbus.
