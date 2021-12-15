# MOSQUITTO
Mosquitto es un servidor de mqtt
Se ha instalado este ser broquer mqtt en la raspberry del integrante del equipo llamado Gorka.

Para instalarlo se han realizado los siguientes pasos:

### Primero  se actualiza la raspberry y se instala el cliente y el broker msoquitto

```ruby
sudo apt update
sudo apt upgrade
sudo apt install mosquitto mosquitto-clients
```
</br>

### Una vez instalado comprobamos que esta en ejecución 


```ruby
sudo systemctl status mosquitto
```

La salida de este comando si todo ha ido bien es este:

![Mosquitto](https://user-images.githubusercontent.com/95297676/146216385-0abe3e1b-0c78-4d9c-ae0a-552c115d212d.png)
