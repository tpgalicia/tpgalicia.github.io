# General

Esta sección describe cómo obtener los datos estáticos sobre el sistema de buses de Coruña. Esto incluye una lista de paradas, una lista de líneas y otros datos como las tarifas.

## Rutas

Todos los datos arriba mencionados se pueden obtener a partir de la ruta:

```
https://itranvias.com/queryitr_v3.php?dato=20160101T000000_gl_0_20160101T000000&func=7
```

Donde la función 7 devuelve novedades sobre la página y, al establecer como parámetro esa fecha, se puede obtener la lista de toda la información.

Es importante mencionar que cambiando \_gl\_ se puede cambiar el idioma de la información sobre las tarifas y de algunas paradas. La información está disponible en los idiomas:

- Gallego: _gl_
- Español: _es_
- Inglés: _en_

## Salida

La petición arriba descrita es de gran tamaño, por eso para facilitar su descripción, en este documento se fragmenta.

### Cabeza

Esta parte _"exterior"_ de la repuesta incluye información sobre el estado de la petición, la fecha de la misma, la fecha de los datos devueltos y su tamaño.

Los puntos suspensivos, en este caso, simbolizan el lugar donde se encontrará la información descrita en los próximos apartados

```json
{
    "resultado": "OK",
    "fecha_peticion": "20230921235412",
    "peticion":"itranvias?fecha=20160101t000000&plataforma=www&lenguaje=gl&idnovedad=0&fechanovedad=20160101t000000",
    "tama\u00f1o": 72829,
    "iTranvias": {
        "actualizacion": {
            "fecha": "20230832T140825",
            ...
        }
    }
    "Origen": "Web_Beta"
}
```

### Cuerpo

El resto de la respuesta incluye toda la información que nos interesa. Se procede a definir la estructura de la misma separándola por tipos de datos, para facilitar su _"digestión"_

Todas las definiciones que siguen a esta se consideran entradas del diccionario `actualización`

#### Líneas

Bajo la clave _lineas_ se describe la información relativa a las líneas en una lista con un diccionario para cada línea en el que se incluye la siguiente información:

- ID: `id`
- Nombre de la línea: `lin_comer`
- Nombre del origen: `nombre_orig`
- Nombre del destino: `nombre_dest`
- Color de la línea en hexadeximal (#RRGGBB): `color`
- Lista de rutas (para cada entrada un diccionario con):
    - ID de la ruta: `ruta`
    - Origen de la ruta (normalmente vacío): `nombre_orig`
    - Destino de la ruta (normalmente vacío): `nombre_dest`
    - Lista de identificadores de las paradas por las que pasa el recorrido

!!! note "Nota"
    Aunque algunas líneas contienen 3 rutas diferentes, aún no he tenido problemas utilizando la primera entrada como sentido de IDA, la segunda como VUELTA e ignorando las sucesivas. El sentido 0 suele ser la IDA, el sentido 1 la VUELTA, los 2-5 suelen ser variantes o extensiones y el sentido 30 es la retirada a Cocheras.

A continuación se muestra un ejemplo de respuesta de este bloque:

```json
"lineas": [
    {
        "id": 100,
        "lin_comer": "1",
        "nombre_orig": "Abente y Lago",
        "nombre_dest": "Castrill\u00f3n",
        "color": "982135",
        "rutas": [
            {
                "ruta": 10000,
                "nombre_orig": "",
                "nombre_dest": "",
                "paradas": [
                    523,
                    180,
                    1,
                    2,
                    3,
                    4,
                    5,
                    ...
                ]
            },
            ...
        ]
    }
    ...
]
```

#### Paradas

Bajo la clave _paradas_ se describe la información relativa a las paradas en una lista con un diccionario para cada parada en la que se incluye la siguiente información:

- ID: `id`
- Nombre: `nombre`
- Coordenadas:
    - Eje X en `posx`
    - Eje Y en `posy`
- Lista de identificadores de las líneas que pasan por la parada

A continuación se muestra un ejemplo de respuesta de este bloque:

```json
"paradas": [
    {
        "id": 1,
        "nombre": "Porta Real",
        "posx": -8.39585,
        "posy": 43.370115,
        "enlaces": [
            100,
            1900,
            200,
            800,
            ...
    }
    ...
]
```

#### Enlaces

En proceso

#### Precios

Bajo la clave _tarifas_ se describe la información relativa a los precios de los billetes en una lista con un diccionario para cada tarifa en la que se incluye el nombre de la tarifa y el precio en euros.

Ejemplo:

```json
"tarifas": [
    {
        "tarifa": "Tarifa ordinaria",
        "precio": 1.3
    ]
    ...
]
```
