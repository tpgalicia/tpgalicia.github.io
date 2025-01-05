# Líneas

Esta sección describe cómo obtener información sobre los buses de una línea y, por tanto, son datos en tiempo real. La primera ruta que se trata devuelve una lista de todas las líneas con la información descrita en el apartado [general](general/) y, por tanto, no se describe más lejos del ejemplo de respuesta.

## Información sobre una línea

### Ruta
Para obtener los datos se puede utilizar la ruta

```
https://itranvias.com/queryitr_v3.php?&func=1&dato=500
```

Donde el parámetro `dato` es el identificador de la línea que se quiere consultar.

### Respuesta

```json
{
    "resultado": "OK",
    "fecha_peticion": "20230922222756",
    "peticion": "jlineas?",
    "tama\u00f1o": 4644,
    "lineas": [
        {
            "id": "100",
            "nom_comer": "1",
            "color_linea": "982135",
            "orig_linea": "Abente y Lago",
            "dest_linea": "Castrill\u00f3n"
            "dest_ida": "Pza. Pablo Iglesias",
            "dest_vuelta": "Abente y Lago"
        }
        ...
    ],
    "Origen": "Web_Beta"
}
```

## Buses para una línea

Se puede obtener información sobre la posición de los buses con respecto al recorrido de una línea, así como su estado.

### Ruta

```
https://itranvias.com/queryitr_v3.php?func=2&dato=500
```

Donde el parámetro `dato` es el identificador de la línea que se quiere consultar.

### Respuesta

```json
{
    "resultado": "OK",
    "fecha_peticion": "20230922224449",
    "peticion": "jparadas?linea=500&version=2",
    "tama\u00f1o": 315,
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

Donde la información principal se encuentra bajo la clave `paradas`, donde existe una un diccionario para cada sentido.
Cada diccionario contiene una lista de paradas, con un diccionario para cada parada que contiene el identificador de la parada (`parada`) y una lista de buses para esa parada.
Cada bus es un diccionario en esa lista con las entradas:

- `bus`: Identificador del bus
- `estado`: Estado del bus,
    - 0: En la parada
    - 1: En movimiento
    - 17: Incorporando a ruta, en una extensión o fuera del itinerario de ida/vuelta normal.
- `distancia`: Posición del bus en su sentido del recorrido como un tanto por uno de la distancia total de ese recorrido.

!!! warning "¡Cuidado!"
    La posición del bus se representa como una fracción del sentido, pero esta no representa la distancia real entre paradas, si no que el 0 representa la primera parada y el 1 la última y las posiciones del resto de paradas están espaciadas a partes iguales.

## Posición geográfica de los buses de una línea

También es posible obtener las coordenadas de los buses de una línea para mostrar esta información sobre un mapa, esto se puede hacer con la ruta:

```
https://itranvias.com/queryitr_v3.php?&func=99&mostrar=B&dato=600
```

```json
{
    "resultado":"OK",
    "fecha_peticion":"20230922231324",
    "peticion":"jmapas?linea=600&mostrar=b",
    "tama\u00f1o":199,
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


## Posición de las paradas de una línea

```
https://itranvias.com/queryitr_v3.php?&func=99&mostrar=P&dato=600
```

### Respuesta

```json
{
    "resultado":"OK",
    "fecha_peticion":"20230922231358",
    "peticion":"jmapas?linea=600&mostrar=p",
    "tama\u00f1o":9540,
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

## Trazado del recorrido de una línea

```
https://itranvias.com/queryitr_v3.php?&func=99&mostrar=R&dato=600
```

### Respuesta

```json
{
    "resultado":"OK",
    "fecha_peticion":"20230922231404",
    "peticion":"jmapas?linea=600&mostrar=r",
    "tama\u00f1o":26731,
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

## Salidas para una línea

```
https://itranvias.com/queryitr_v3.php?&func=8&dato=500&fecha=20230922
```

```json
{
    "resultado":"OK",
    "fecha_peticion":"20230922232647",
    "peticion":"servicios",
    "tama\u00f1o":668,
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
