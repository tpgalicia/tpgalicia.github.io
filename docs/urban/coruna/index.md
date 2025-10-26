# Urbano de A Coruña

El transporte urbano de A Coruña consiste en un servicio de autobuses urbanos prestado por [Tranvias Coruña](https://tranviascoruna.com), en régimen de concesión por parte del Concello de A Coruña.

## Datos estáticos

Los datos de las líneas de autobuses urbanos de A Coruña se pueden obtener en formato GTFS desde el [NAP](../../other/nap.md) del Ministerio de Transportes y Movilidad Sostenible. La URL del dataset es <https://nap.transportes.gob.es/Files/Detail/1376>.

Además, el Concello dispone de un servidor FTP con el historial de feeds GTFS para el ayuntamiento, al que se puede acceder a través de `ftp://tranviasro:TR4nV14S.ro@ftp.coruna.es/`.

El feed GTFS solo incluye los archivos obligatorios `agency.txt`, `routes.txt`, `trips.txt`, `stops.txt`, `stop_times.txt`, `calendar.txt` y `calendar_dates.txt` y, también, `shapes.txt`.

## Datos en tiempo real

Esta sección documenta la API que utiliza la página [iTranvías](https://itranvias.com) de la [Compañía de Tranvías de **La** Coruña](https://tranviascoruna.com). La información ha sido obtenida mediante *ingeniería inversa* durante el desarrollo del proyecto [bus.delthia.com](https://bus.delthia.com) por su autor.

!!! warning "Aviso"
    Es posible que no se haya descubierto toda la funcionalidad, o que existan maneras diferentes de utilizar los parámetros para obtener otros resultados o información adicional. Esta información representa la mejor aproximación sobre el funcionamiento de la API según lo observado a través de la página de *iTranvias* y una pequeña investigación.

### Estimaciones para una parada

Para obtener los próximos buses para una parada se puede utilizar la ruta:

```
https://itranvias.com/queryitr_v3.php?&func=0&dato=10
```

Donde el parámetro `dato` es el identificador de la parada para la que se quieren consultar los buses. La respuesta tendrá esta forma:

```json
{
    "resultado": "OK",
    "fecha_peticion": "20230922152056",
    "peticion": "jbuses?parada=100&version=2",
    "tamaño": 700,
    "buses": {
        "parada": 100,
        "lineas": [
            {
                "linea": 500,
                "buses": [
                    {
                        "bus": 385,
                        "tiempo": "<1",
                        "distancia": "186",
                        "estado": 1,
                        "ult_parada": 203
                    },
                    ...
                ],
                ...
            },
            ...
        ]
    }
}
```

El contenido principal se encuentra bajo la clave `buses['paradas']`, donde existe una entrada para cada línea **activa** (esto es importante, no incluirá aquellas líneas que pasan por la parada pero para las que ya no hay buses activos con ese destino) y, dentro de la clave `buses`, una entrada de diccionario para cada bus con la información:

- Identificador del bus: `id`
- Tiempo que tardará en llegar a la parada: `tiempo`. En minutos pero el valor será _<1_ cuando el bus esté a punto de llegar
- Distancia del bus a la parada en metros: `distancia`
- Estado del bus: `estado`, con los siguientes valores:
    - 0: El bus está en la parada
    - 1: El bus está en movimiento
- Última parada del recorrido por la que pasó el bus: `ult_parada`

## Datos API

Esta sección describe las consultas de API disponibles para obtener información sobre líneas y datos generales del sistema.

### Líneas

#### Información sobre una línea

Para obtener los datos se puede utilizar la ruta:

```
https://itranvias.com/queryitr_v3.php?&func=1&dato=500
```

Donde el parámetro `dato` es el identificador de la línea que se quiere consultar.

**Respuesta:**

```json
{
    "resultado": "OK",
    "fecha_peticion": "20230922222756",
    "peticion": "jlineas?",
    "tamaño": 4644,
    "lineas": [
        {
            "id": "100",
            "nom_comer": "1",
            "color_linea": "982135",
            "orig_linea": "Abente y Lago",
            "dest_linea": "Castrillón"
            "dest_ida": "Pza. Pablo Iglesias",
            "dest_vuelta": "Abente y Lago"
        }
        ...
    ],
    "Origen": "Web_Beta"
}
```

#### Buses para una línea

Se puede obtener información sobre la posición de los buses con respecto al recorrido de una línea, así como su estado.

**Ruta:**

```
https://itranvias.com/queryitr_v3.php?func=2&dato=500
```

Donde el parámetro `dato` es el identificador de la línea que se quiere consultar.

**Respuesta:**

```json
{
    "resultado": "OK",
    "fecha_peticion": "20230922224449",
    "peticion": "jparadas?linea=500&version=2",
    "tamaño": 315,
    "mls": 0,
    "paradas": [
        {
          "sentido": 0,
          "paradas": [
            {
                "parada": 184,
                "buses": [
                    {
                        "bus": 357,
                        "estado": 1
                        "distancia": 0.288
                    },
                    ...
                ]
            },
            ...
          ]
        },
        ...
    ],
    "Origen": "Web_Beta"
}
```

La información principal se encuentra bajo la clave `paradas`, donde existe un diccionario para cada sentido. Cada diccionario contiene una lista de paradas, con un diccionario para cada parada que contiene el identificador de la parada (`parada`) y una lista de buses para esa parada.

Cada bus es un diccionario en esa lista con las entradas:

- `bus`: Identificador del bus
- `estado`: Estado del bus,
    - 0: En la parada
    - 1: En movimiento
    - 16: En una parada de una extensión fuera del itinerario de ida/vuelta normal o en cocheras antes de salir.
    - 17: Incorporando a ruta, en una extensión o fuera del itinerario de ida/vuelta normal.
- `distancia`: Posición del bus en su sentido del recorrido como un tanto por uno de la distancia total de ese recorrido.

!!! warning "¡Cuidado!"
    La posición del bus se representa como una fracción del sentido, pero esta no representa la distancia real entre paradas, si no que el 0 representa la primera parada y el 1 la última y las posiciones del resto de paradas están espaciadas a partes iguales.

#### Posición geográfica de los buses de una línea

También es posible obtener las coordenadas de los buses de una línea para mostrar esta información sobre un mapa:

```
https://itranvias.com/queryitr_v3.php?&func=99&mostrar=B&dato=600
```

**Respuesta:**

```json
{
    "resultado":"OK",
    "fecha_peticion":"20230922231324",
    "peticion":"jmapas?linea=600&mostrar=b",
    "tamaño":199,
    "mapas": [
        {
            "buses": [
                {
                    "sentido": 0,
                    "buses": [
                        {
                            "bus": 342,
                            "posx": -8.413613,
                            "posy": 43.362973
                        },
                        ...
                    ]
                },
                ...
            ],
            ...
        },
        ...
    ],
    "Origen": "Web_Beta"
}
```

#### Posición de las paradas de una línea

```
https://itranvias.com/queryitr_v3.php?&func=99&mostrar=P&dato=600
```

**Respuesta:**

```json
{
    "resultado":"OK",
    "fecha_peticion":"20230922231358",
    "peticion":"jmapas?linea=600&mostrar=p",
    "tamaño":9540,
    "mapas": [
        {
            "paradas": [
                {
                    "sentido":"0",
                    "paradas":[
                        {
                            "id": "570",
                            "parada": "Rda. de Monte Alto, 52",
                            "posx": -8.40657,
                            "posy": 43.380598
                        },
                        ...
                    ]
                },
                ...
            ]
        },
    ],
    "Origen": "Web_Beta"
}
```

#### Trazado del recorrido de una línea

```
https://itranvias.com/queryitr_v3.php?&func=99&mostrar=R&dato=600
```

**Respuesta:**

```json
{
    "resultado":"OK",
    "fecha_peticion":"20230922231404",
    "peticion":"jmapas?linea=600&mostrar=r",
    "tamaño":26731,
    "mapas": [
        {
            "recorridos": [
                {
                    "sentido":"0",
                    "recorrido": "-8.406574518012148,43.3805987842061,0 -8.406662548136888,43.38047546094802,..."
                },
                ...
            ]
        }
    ],
    "Origen": "Web_Beta"
}
```

#### Salidas para una línea

```
https://itranvias.com/queryitr_v3.php?&func=8&dato=500&fecha=20230922
```

**Respuesta:**

```json
{
    "resultado":"OK",
    "fecha_peticion":"20230922232647",
    "peticion":"servicios",
    "tamaño":668,
    "servicios": [
        {
            "fecha":"20230922",
            "tipo":"Especial",
            "ida": [
                635,
                700,
                725,
                543,
                ...
            ],
            "vuelta": [
                700,
                725,
                743,
                757,
                ...
            ]
        }
    ],
    "Origen": "Web_Beta"
}
```

### Información general

Esta sección describe cómo obtener los datos estáticos sobre el sistema de buses de A Coruña. Esto incluye una lista de paradas, una lista de líneas y otros datos como las tarifas.

#### Consulta principal

Todos los datos mencionados se pueden obtener a partir de la ruta:

```
https://itranvias.com/queryitr_v3.php?dato=20160101T000000_gl_0_20160101T000000&func=7
```

La función 7 devuelve novedades sobre la página y, al establecer como parámetro esa fecha, se puede obtener la lista de toda la información.

Es importante mencionar que cambiando \_gl\_ se puede cambiar el idioma de la información sobre las tarifas y de algunas paradas. La información está disponible en los idiomas:

- Gallego: _gl_
- Español: _es_
- Inglés: _en_

#### Estructura de la respuesta

La petición arriba descrita es de gran tamaño, por eso para facilitar su descripción, en este documento se fragmenta.

**Cabeza:**

Esta parte _"exterior"_ de la respuesta incluye información sobre el estado de la petición, la fecha de la misma, la fecha de los datos devueltos y su tamaño.

Los puntos suspensivos, en este caso, simbolizan el lugar donde se encontrará la información descrita en los próximos apartados:

```json
{
    "resultado": "OK",
    "fecha_peticion": "20230921235412",
    "peticion":"itranvias?fecha=20160101t000000&plataforma=www&lenguaje=gl&idnovedad=0&fechanovedad=20160101t000000",
    "tamaño": 72829,
    "iTranvias": {
        "actualizacion": {
            "fecha": "20230832T140825",
            ...
        }
    }
    "Origen": "Web_Beta"
}
```

**Cuerpo:**

El resto de la respuesta incluye toda la información relevante. Se procede a definir la estructura de la misma separándola por tipos de datos, para facilitar su comprensión.

Todas las definiciones que siguen se consideran entradas del diccionario `actualización`.

#### Líneas

Bajo la clave _lineas_ se describe la información relativa a las líneas en una lista con un diccionario para cada línea en el que se incluye la siguiente información:

- ID: `id`
- Nombre de la línea: `lin_comer`
- Nombre del origen: `nombre_orig`
- Nombre del destino: `nombre_dest`
- Color de la línea en hexadecimal (#RRGGBB): `color`
- Lista de rutas (para cada entrada un diccionario con):
    - ID de la ruta: `ruta`
    - Origen de la ruta (normalmente vacío): `nombre_orig`
    - Destino de la ruta (normalmente vacío): `nombre_dest`
    - Lista de identificadores de las paradas por las que pasa el recorrido

!!! note "Nota"
    Aunque algunas líneas contienen 3 rutas diferentes, normalmente la primera entrada corresponde al sentido de IDA, la segunda a VUELTA y las sucesivas se ignoran. El sentido 0 suele ser la IDA, el sentido 1 la VUELTA, los sentidos 2-5 suelen ser variantes o extensiones y el sentido 30 es la retirada a Cocheras.

Ejemplo de respuesta:

```json
"lineas": [
    {
        "id": 100,
        "lin_comer": "1",
        "nombre_orig": "Abente y Lago",
        "nombre_dest": "Castrillón",
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

Ejemplo de respuesta:

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

En proceso.

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
