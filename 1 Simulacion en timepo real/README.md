# Simulación de sensores de ascensor
Debido a que los sensores realies no estaban instalados en el momento del desarrollo de este proyecto. 
Se ha tenido que simular el comportamiento en tiempo real de los sensores.
Para ello se ha implementado el siguiente codigo que envia de forma aleatoria los datos del achivo simulado que se nos fue proporcionado ["Datos_ascensores_dic_2021.xlsx"](Datos_ascensores_dic_2021.xlsx).

El codigo utilizado es se encuentra en el arhcivo ["ExcelToJSON.ipynb"](ExcelToJSON.ipunb), compuesto por las siguientes partes:

```ruby
import json
import pandas

excel_Ascensor_1 = pandas.read_excel('/content/drive/MyDrive/Master/Tecnologías Industriales/IMH TRABAJO TECNOLOGIAS INDUSTRIALES/Datos_ascensores_dic_2021.xlsx',sheet_name='Ascensor_1')
excel_Ascensor_2 = pandas.read_excel('/content/drive/MyDrive/Master/Tecnologías Industriales/IMH TRABAJO TECNOLOGIAS INDUSTRIALES/Datos_ascensores_dic_2021.xlsx',sheet_name='Ascensor_2')
excel_Ascensor_3 = pandas.read_excel('/content/drive/MyDrive/Master/Tecnologías Industriales/IMH TRABAJO TECNOLOGIAS INDUSTRIALES/Datos_ascensores_dic_2021.xlsx',sheet_name='Ascensor_3')

Ascensor_1 = excel_Ascensor_1.to_json(orient='records')
Ascensor_2 = excel_Ascensor_2.to_json(orient='records')
Ascensor_3 = excel_Ascensor_3.to_json(orient='records')
```


