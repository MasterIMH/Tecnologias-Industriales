# Web Data Connector

Los Web Data Connectors son herramientas que permiten conectar las bases de datos con aplicaciones externas. 

El único Web Data Connector libre que existe para Influx DB requiere que la consulta se realize a través de https. Sin embargo, al ser esta una práctica educativa no se ha considerado oportuno comprar los certificados necesarios. 

Por ello, se ha generado un código en Python que genera un .csv dentro de un directorio de Google Drive cada 15 segundos. Este archivo es el que se utiliza como entrada de datos en Tableau.

``` ruby
from google.colab import drive
drive.mount('/content/drive')

!python3 -m pip install influxdb

from influxdb import InfluxDBClient
import json
import pandas as pd
import time
client = InfluxDBClient(host='casaeibar.ddns.net', port=8086, username='pi', password='raspberry')

i =0
while True:
  i= i+1
  results = client.query('SELECT * FROM "Datos"' ,database = 'ascensores').get_points()
  df = pd.DataFrame.from_records(results)
  #df.to_csv('/content/drive/MyDrive/Master/Tecnologías Industriales/IMH TRABAJO TECNOLOGIAS INDUSTRIALES/Datos_ascensores.csv',index = None)
  df.to_csv('/content/drive/MyDrive/Master/Tecnologías Industriales/Datos_ascensores.csv',index = None)
  print("Actualizado {0} veces ".format(i))
  
  time.sleep(15)
  ```
