# Web Data Connector

Los Web Data Connectors son herramientas que permiten conectar las bases de datos con aplicaciones externas. 

El único Web Data Connector libre que existe para Influx DB requiere que la consulta se realize a través de https. Sin embargo, al ser esta una práctica educativa no se ha considerado oportuno comprar los certificados necesarios. 

Por ello, se ha generado un código en Python que genera un .csv dentro de un directorio de Google Drive cada 15 segundos. Este archivo es el que se utiliza como entrada de datos en Tableau.
