# Node-Red

Node-red se usa para conectar distintas tecnologias. </br>
En este caso se encarga de recivir los datos de mqtt y trasladarselos a la base de datos, todo esto respetando los protocolos de ambos servicio

## En este proyecto se ha utilizado de la siguiente manera
Primero se añade un bloque por cada ascensor (Realmente solo es necesario un bloque que reciba los datos, solo que es mas visual y entendible el flujo si cada ascensor tiene su propio recorrido).
Este primer bloque se encarga de recibir la informacion del MOSQUITTO (MQTT). 
Lo traslada al siguiente bloque, que borra la marca temporal de los datos recibidos, ya que la base de datos genera su propia marca de tiempo cuando se ingestan los datos.
Ademas se añade el dato de que ascensor ha sido el que ha enviado esta información.
Por ultimo trasladan esta infromación a un bloque comun que se encarga de enviar los datos a la base de datos con el protocolo y formato adecuados. 

</br>

![NodeRed](https://user-images.githubusercontent.com/95297676/146219472-f98df916-2b64-4dd9-bd80-5748cd29afac.png)

</br>

El flujo es el que se visualiza en el centro. Rosita la ingesta de datos MQTT, amarillo la modificación y marron clarito el influx.
</br> 

El archivo con esa configuración para poder importarlo en node red se llama ["flows.json"](flows.json). Lo unico que hay que hacer es establecer las IP's del broker MQTT y de la base de datos InfluxDB
