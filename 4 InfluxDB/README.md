![image](https://user-images.githubusercontent.com/95297676/146227237-21789dc8-9eda-4019-8376-45740a9f2f76.png)


# InfluxDB
Se ha decidido utilizar una base de datos influx DB por que estructura sus datos en fucion de la marca temporal que se le añade al ingresar el dato a la base de datos. Esto hace que sea muy util para las consultas en funcion de la fecha de generación o la reccopilacion del ultimon dato, las que se utilizan para las herramientas en tiempo real.
Tambien cuanta con una utilidad para que pasado untiempo se reduzcan los datos en función a los criterios que establezcas. Por ejemplo no tiene sentido saber la presione en el dato x de hace tres años, sin embargo si que nos puede interesar tener el numero de veces que subio ese dia. 

## Instalación

Para usar influx se ha intentado utilizado una raspberry. En primera instancia un docker, pero se encontraron problemas ya que no existe el fichero de configuración necesario para ese docker en un sistema de arquitectura ARM de 64 bits que no soporta 32bits.

Por ello se ha obtado por instalarlo localmente. Ha sido costoso encontrar una compilación compatible con ARM.
Finalemente se ha encontrado el siguiente repostitorio:

``` 
curl https://repos.influxdata.com/influxdb.key | gpg --dearmor | sudo tee /usr/share/keyrings/influxdb-archive-keyring.gpg >/dev/null

echo "deb [signed-by=/usr/share/keyrings/influxdb-archive-keyring.gpg] https://repos.influxdata.com/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/influxdb.list

sudo apt update

sudo apt install influxdb

sudo systemctl unmask influxdb
sudo systemctl enable influxdb

sudo systemctl start influxdb

```

Tras ello se ha creado la base de datos:

```
CREATE DATABASE ascensores
```
Y listo la base de datos esta en fucninamiento.

![INFLUX](https://user-images.githubusercontent.com/95297676/146226950-28ffa4d4-0c20-4593-a8a5-316aae1b678c.png)

