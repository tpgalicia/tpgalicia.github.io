# Urbano de Santiago de Compostela

El transporte urbano de Santiago de Compostela consiste en un servicio de autobuses urbanos gestionados por [Tussa](https://tussa.org) y prestados principalmente por [Tralusa](https://www.monbus.es/es/movilidad/urbanos-y-metropolitanos/transporte-urbano-de-santiago) (Grupo Monbus) y también [Mosquera](https://www.autocaresriasbaixas.com/descargas.aspx?grupo=23) (Grupo Rías Baixas), [Grabanxa](https://autosgrabanxa.es/), [Aucasa](https://arriva.es/es/galicia) (Grupo Arriva) y [Hermanos Ferrín](http://www.grupoferrin.com/); en régimen de concesión por parte del Concello de Santiago de Compostela y en precario desde 2016.

## Datos estáticos

No existe un feed público en un formato estándar (como lo es GTFS) para acceder a las paradas, líneas y horarios.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas API de Tussa, extraídas de la app oficial maisbus.

## Datos en tiempo real

No existe un feed público en un formato estándar (como lo son GTFS-RealTime o SIRI) para acceder a las estimaciones de llegada de los autobuses urbanos en tiempo real. Por tanto, no hay forma de obtener las estimaciones de llegadas a las paradas, ni alertas de servicio ni posiciones de los vehículos.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas API de Tussa, extraídas de la app oficial maisbus.


### Paradas

Llamando por HTTP POST a siguiente URL se obtienen todas las paradas con su código, nombre, zona (barrio, no tarifaria), coordenadas y líneas . Poniendo el parámetro `nombre` vacío se obtienen todas las paradas, aunque se puede hacer una búsqueda por nombre o id {"ids":["691"]}. 

```http
POST https:/tralusa.org/stops


[
	{
        "id": 1,
        "nombre": "A Barcia",
        "coordenadas": {
            "latitud": 42.8734893636941,
            "longitud": -8.58813285827637
        },
        "lineas": [
            {
                "nombre": "LP8",
                "color": "#e28c3a"
            }
        ]
    },
	{ ... }
]
```

También es posible buscar las paradas al rededor de un punto llamando por HTTP POST a siguiente URL, poniendo al final las coordenadas.

```http
POST https://maisbus.santiago.com/stops/42.9301279/-8.5193463


[
	{
        "id": 1,
        "nombre": "A Barcia",
        "coordenadas": {
            "latitud": 42.8734893636941,
            "longitud": -8.58813285827637
        },
        "lineas": [
            {
                "nombre": "LP8",
                "color": "#e28c3a"
            }
        ]
    },
	{ ... }
]
```

### Líneas

Llamando por HTTP GET a siguiente URL se obtienen todas las líneas con su código, sinóptico, nombre, empresa operadora, el número de incidencias que le afectan y su color representativo.

```http
GET https://monbus.es/santiago/lines

```

```http
GET https://monbus.es/santiago/lines/40/sentidos

[
  {
    "id": 44,
    "nombre": "Aeroporto – Hórreo (est. Intermodal)",
    "sentido": "IDA"
  },
  {
    "id": 45,
    "nombre": "Hórreo (est. Intermodal) – Aeroporto",
    "sentido": "VUELTA"
  }
]
```
```http
GET https://monbus.es/santiago/rutas/44/stops

[
  {
    "id": 44,
    "nombre": "Aeroporto – Hórreo (est. Intermodal)",
    "sentido": "IDA"
  },
  {
    "id": 45,
    "nombre": "Hórreo (est. Intermodal) – Aeroporto",
    "sentido": "VUELTA"
  }
]
```

### Alertas de servicio

Llamando por HTTP GET a siguiente URL se obtienen todos los avisos activos con sus respectivas paradas y líneas afectadas, así como las fechas de inicio/fin y la descripción. Poniendo el parámetro `lang` en `es` se devuelven en castellano, usando `gl`, en gallego, y usando `en`, en inglés, aunque suele presentar menos información.

```http
GET hhttps://monbus.es/santiago/avisos.json?lang=es

[
	{
        "id": 578,
        "titulo": "P1 no CamiloDB",
        "descripcion": "Línea P1: los viajes a Figueiras con salida de la pza. de Galicia a las 13:50, \r\n14:40 y 15:30 (lunes a viernes lab.) paran en la rúa Pastoriza, NO accederán\r\n a Anxo Casal y pza. Camilo D. Baliño",
        "inicio": "2024-09-09 00:00",
        "fin": null,
        "lineas": [
        {
            "nombre": "LP1",
            "color": "#537eb3"
        }
        ],
        "paradas": [
        {
            "codigo": "050",
            "nombre": "Anxo Casal (Xunta) 2"
        },
        {
            "codigo": "230",
            "nombre": "Pza. Camilo D. Baliño"
        },
        {
            "codigo": "048",
            "nombre": "Anxo Casal (st. pza.) 2"
        }
        ]
    },
	{ ... }
]
```

### Estimaciones para una parada

Llamando al siguiente endpoint, se pueden obtener las estimaciones de llegada para una parada, ordenadas por tiempo de manera ascendente, junto a datos de la parada como su nombre, la zona (barrio, no tarifaria) en la que está situada, la ubicación. Para escoger la parada, hay que poner el código de parada después de paradas/.

```http
GET https://monbus.es/santiago/rt/stops/500

{
  "id": 500,
  "nombre": "Hórreo (E. Intermodal)",
  "coordenadas": {
    "latitud": 42.8706512,
    "longitud": -8.5461194
  },
  "lineas": [
    {
      "id": 33,
      "nombre": "San Roque / Santa Lucía / Pajuela",
      "color": "#75bd96",
      "minutos": 0
    },
    { ... }
  ]
}
```

!!! warning "¡Cuidado!

    Es común que las estimaciones aumenten, disminuyan o desaparezcan repentinamente.
    El nombre de la línea no está relacionado con el sentido que está tomando si no que es el nombre genérico.

También se pueden obtener las horas de paso programadas de una línea y parada.

```http
GET https://monbus.es/santiago/lines/6/500

[
  "07:31",
  "08:01",
  "08:31",
  "09:01",
  "09:31",
  "10:01",
  "11:01",
  "11:31",
  "12:01",
  "12:31",
  "13:01",
  "13:31",
  "14:01",
  "14:31",
  "15:01",
  "15:31",
  "16:01",
  "16:31",
  "17:01",
  "17:31",
  "18:01",
  "18:31",
  "19:01",
  "19:31",
  "20:01",
  "20:31",
  "21:01",
  "21:31",
  "22:31",
  "22:57",
  "10:28",
  "21:58"
]
```

