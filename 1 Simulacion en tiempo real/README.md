# Simulación de sensores de ascensor
Debido a que los sensores realies no estaban instalados en el momento del desarrollo de este proyecto. 
Se ha tenido que simular el comportamiento en tiempo real de los sensores.
Para ello se ha implementado el siguiente codigo que envia de forma aleatoria los datos del achivo simulado que se nos fue proporcionado ["Datos_ascensores_dic_2021.xlsx"](Datos_ascensores_dic_2021.xlsx).

El codigo utilizado es se encuentra en el arhcivo ["ExcelToJSON.ipynb"](ExcelToJSON.ipunb), compuesto por las siguientes partes:

En la primera etapa se lee el documento excel y se convierten los datos a JSON.
```ruby
import json
import pandas
from paho.mqtt import client as mqtt_client
from random import randint
from random import choice
import time

excel_Ascensor_1 = pandas.read_excel('Datos_ascensores_dic_2021.xlsx',sheet_name='Ascensor_1')
excel_Ascensor_2 = pandas.read_excel('Datos_ascensores_dic_2021.xlsx',sheet_name='Ascensor_2')
excel_Ascensor_3 = pandas.read_excel('Datos_ascensores_dic_2021.xlsx',sheet_name='Ascensor_3')

Ascensor_1 = excel_Ascensor_1.to_json(orient='records')
Ascensor_2 = excel_Ascensor_2.to_json(orient='records')
Ascensor_3 = excel_Ascensor_3.to_json(orient='records')

Ascensor1 = json.loads(Ascensor_1)
Ascensor2 = json.loads(Ascensor_2)
Ascensor3 = json.loads(Ascensor_3)

Ascensores=[Ascensor1,Ascensor2,Ascensor3]
```
</br> Por otro lado se implementan las funciones asociadas al envio de los datos por MQTT.
```ruby
broker = 'localhost'
broker1 = 'casaeibar.ddns.net'
port = 1883

topic = ["Ascensor1","Ascensor2","Ascensor3"]
last =[0.0,0.0,0.0]
client_id = f'python-mqtt-{randint(0, 1000)}'

def connect_mqtt():
    def on_connect(client, userdata, flags, rc):
        if rc == 0:
            print("Connected to MQTT Broker!")
        else:
            print("Failed to connect, return code %d\n", rc)
    # Set Connecting Client ID
    client = mqtt_client.Client(client_id)
    #client.username_pw_set(username, password)
    client.on_connect = on_connect
    client.connect(broker, port)
    return client
    
def publish(client):
    time.sleep(1)
    while True:
        i = randint(0,2)
        asPublish(client,Ascensores[i],topic[i],i)      
```
</br>
Tambie se han escrito funciones de eleccion de datos de forma automatica que envian datos en intervalos de tiempo aleatorios entre 0 y 10 segundos.

```ruby
def comp(json,i):
    global last
    print(json["Piso"])
    piso = json["Piso"]
    if piso == last[i]:
        return None
    if piso > last[i]:
        json["Viaje"] = "subida"
    else:
        json["Viaje"] = "bajada"
    last[i] = piso
    return json   
    
    
def asPublish(client, Ascensores, topic, i):
    msg = None
    while msg == None:
        msg = comp(choice(Ascensores),i)
    msg = json.dumps(msg, indent=4, sort_keys=True)
    result = client.publish(topic, msg)
    # result: [0, 1]
    status = result[0]
    if status == 0:
        print(f"Send `{msg}` to topic `{topic}`")
    else:
        print(f"Failed to send message to topic {topic}")
    time.sleep(randint(0,10))
```

</br>
Por ultimo se ejecuta para que comienze el envio de los datos

```ruby
def run():
    client = connect_mqtt()
    client.loop_start()
    publish(client)
    
run()
```
