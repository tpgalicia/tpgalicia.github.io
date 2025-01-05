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
POST https://app.tussa.org/tussa/api/paradas

    {"nombre":""}

[
	{
        "id": 1,
        "codigo": "001",
        "nombre": "A Barcia",
        "zona": "Roxos / Villestro",
        "coordenadas": {
            "latitud": 42.8734893636941,
            "longitud": -8.58813285827637
        },
        "lineas": [
            {
                "sinoptico": "LP8",
                "estilo": "#e28c3a"
            }
        ]
    },
	{ ... }
]
```

También es posible buscar las paradas al rededor de un punto llamando por HTTP POST a siguiente URL, poniendo al final las coordenadas.

```http
POST https://app.tussa.org/tussa/api/paradas/42.9301279/-8.5193463

[
    {
        "id": 682,
        "codigo": "682",
        "nombre": "Bálsoma 2",
        "zona": null,
        "distancia": 2.4016941753545837,
        "coordenadas": {
            "latitud": 42.9301279,
            "longitud": -8.5193463
        },
        "lineas": [
            {
                "sinoptico": "L1",
                "estilo": "#f32621"
            },
            {
                "sinoptico": "LP2",
                "estilo": "#d23354"
            }
        ]
    },
	{ ... }
]
```

### Líneas

Llamando por HTTP GET a siguiente URL se obtienen todas las líneas con su código, sinóptico, nombre, empresa operadora, el número de incidencias que le afectan y su color representativo.

```http
GET https://app.tussa.org/tussa/api/lineas


[
    {
        "id": 1,
        "codigo": "1",
        "sinoptico": "L1",
        "nombre": "Cemiterio de Boisaca / hospital Clínico",
        "empresa": "TRALUSA",
        "incidencias": 0,
        "estilo": "#f32621"
    },
	{ ... }
]
```

Llamando por HTTP GET a siguiente URL poniendo su respectivo código se obtienen los detalles sobre una línea determinada: id, sinóptico, nombre, información horaria, color representativo, incidencias y las diferentes rutas con sus paradas (que pueden ser ocasionales) y nombres.Poniendo el parámetro `lang` en `es` se devuelven en castellano, usando `gl`, en gallego, y usando `en`, en inglés, aunque suele presentar menos información.

```http
GET https://app.tussa.org/tussa/api/lineas/1?ang=es


[
    {
    "id": 1,
    "codigo": "1",
    "sinoptico": "L1",
    "nombre": "Cemiterio de Boisaca / hospital Clínico",
    "informacion": "\u003Cp\u003E\u003C/p\u003E\u003Cp\u003E\u003C/p\u003E\u003Cp\u003E\u003Cu\u003E\u003Cb\u003ECemiterio de Boisaca – Hospital Clínico\u003C/b\u003E\u003C/u\u003E\r\n\r\n\u003C/p\u003E\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003Cb\u003EL-V laborables\u003C/b\u003E\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003EDe 7:10 a 22:06 (cada 16 min.)\u003C/p\u003E\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E22:30 22:50\u003Cbr\u003E\u003C/p\u003E\r\n\r\n\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003Cb\u003ESábados laborables\u003C/b\u003E\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003EDe 7:00 a 15:00 (cada 20 min.)\u003Cbr\u003E\u003C/p\u003E\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003EDe 15:00 a 22:30 (cada 30 min.).\r\n\r\n\u003C/p\u003E\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003Cb\u003EDomingos, festivos\u003C/b\u003E\u003C/p\u003E\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E7:20\u003Cbr\u003E\u003C/p\u003E\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003EDe 8:00 a 22:30 (cada 30 min.).\r\n\r\n\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003Cu\u003E\u003Cb\u003EHospital Clínico – Cemiterio de Boisaca\u003C/b\u003E\u003C/u\u003E\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003Cb\u003EL-V laborables\u003C/b\u003E\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E6:30 7:20 7:40\u003Cbr\u003E\u003C/p\u003E\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003EDe 8:06 a 23:02 (cada 16')\u003C/p\u003E\r\n\r\n\r\n\r\n\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003Cb\u003ESábados laborables\u003C/b\u003E\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003EDe 7:30 a 15:30 (cada 20 min.)\u003C/p\u003E\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003EDe 15:30 a 23:00 (cada 30 min.)\u003Cbr\u003E\u003C/p\u003E\r\n\r\n\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003Cb\u003EDomingos, festivos\u003C/b\u003E\u003C/p\u003E\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003EDe 8:00 a 14:30 (cada 30 min.)\u003C/p\u003E15:10\u003Cbr\u003E\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003EDe 15:30 a 23:00 (cada 30 min.)\u003Cbr\u003E\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003Cb\u003E\u003Cu\u003ENotas horario\u003C/u\u003E\u003C/b\u003E\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003Cb\u003EProlongación aparcadoiro de Santa Marta (L-V laborables): \u003C/b\u003Ede 7:20 a 15:18\u003Cb\u003E\u003Cbr\u003E\u003C/b\u003E\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003Cb\u003EProlongación a Son (L-V laborables):\u003C/b\u003E\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003EDesde Garabal, 7:25\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003EPasos aproximados por rúa da Senra a Son, 7:52 14:40\u003Cbr\u003E\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003Cb\u003EProlongación a Son (sábados laborables):\u003C/b\u003E\u003C/p\u003E\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003EDesde Garabal, 7:25\u003C/p\u003E\r\n\r\n\r\n\r\n\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003Cb\u003EProlongación por rúa Manuel María:\u003C/b\u003E\u003C/p\u003E\r\n\r\nL-V laborables, 7:58 9:02 10:06 11:10 14:54 15:58 17:02 18:06\u003Cp class=\"MsoNormal\" style=\"margin-bottom: 0.0001pt;\"\u003E\u003C/p\u003E\r\n\r\n\u003Cp\u003E\u003C/p\u003E\u003Cp\u003E\u003C/p\u003E",
    "estilo": "#f32621",
    "trayectos": [
        {
        "nombre": "Cemiterio Boisaca - Hospital Clínico",
        "sentido": "IDA",
        "paradas": [
            {
            "id": 538,
            "codigo": "538",
            "nombre": "Garabal (cruce)",
            "zona": "Son",
            "extraordinaria": true,
            "coordenadas": {
                "latitud": 42.9164167,
                "longitud": -8.5154668
            }
            },
            {...}
        ]
        },
        {
        "nombre": "Hospital Clínico - Cemiterio Boisaca",
        "sentido": "VUELTA",
        "paradas": [
           {
            "id": 278,
            "codigo": "278",
            "nombre": "Hospital Clínico",
            "zona": "Choupana",
            "extraordinaria": false,
            "coordenadas": {
                "latitud": 42.8692620288852,
                "longitud": -8.56517851352692
            }
            },
            {...}
        ]
        }
    ],
    "incidencias": [
        {
      "id": 556,
      "titulo": "Desvíos Pombal",
      "descripcion": "\u003Ch3\u003E\u003Cu\u003EModificacións nas liñas con motivo do corte ao tráfico da rúa do Pombal (a partir do martes 25/6/2024)\u003C/u\u003E\u003C/h3\u003E\r\n     \r\n    \u003Cdiv class=\"entradtxt\"\u003E\u003Cp\u003ECó inicio das obras na rúa do Pombal o \r\nmartes 25 de xuño, as liñas 4, 8, 9, C2, C4, P1 e P7 modificarán os seus\r\n horarios e percorridos. \u003C/p\u003E\u003C/div\u003E\r\n    \u003Cdiv class=\"txtnova\"\u003E\u003Cp\u003ENa web www.tussa.org poden consultar os \r\nnovos percorridos e horarios por liña, así como as paradas anuladas e a \r\nalternativa máis próxima en cada caso.\u003C/p\u003E\u003Cp\u003EDesculpen as molestias que estas alteracións lles poidan ocasionar. \u003C/p\u003E\u003C/div\u003E",
      "inicio": "2024-06-21 00:00",
      "fin": null
    }
    ]
    }
]
```

```http
GET https://app.tussa.org/tussa/api/lineas/40/trayectos

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
GET https://app.tussa.org/tussa/api/trayectos/44/paradas

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
GET https://app.tussa.org/tussa/api/incidencias?lang=es

[
	{
        "id": 578,
        "stamp": 1725868539000,
        "titulo": "P1 no CamiloDB",
        "descripcion": "Línea P1: los viajes a Figueiras con salida de la pza. de Galicia a las 13:50, \r\n14:40 y 15:30 (lunes a viernes lab.) paran en la rúa Pastoriza, NO accederán\r\n a Anxo Casal y pza. Camilo D. Baliño",
        "inicio": "2024-09-09 00:00",
        "fin": null,
        "lineas": [
        {
            "sinoptico": "LP1",
            "estilo": "#537eb3"
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
GET https://app.tussa.org/tussa/api/paradas/691

{
  "id": 691,
  "codigo": "691",
  "nombre": "Hórreo (E. Intermodal)",
  "zona": "Zona RENFE",
  "coordenadas": {
    "latitud": 42.8706512,
    "longitud": -8.5461194
  },
  "lineas": [
    {
      "id": 33,
      "sinoptico": "LP3",
      "nombre": "San Roque / Santa Lucía / Pajuela",
      "estilo": "#75bd96",
      "proximoPaso": "2025-01-05 20:41",
      "minutosProximoPaso": 0
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
GET https://app.tussa.org/tussa/api/horario/6/691

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

### Otros

También es posible obtener otra información como puntos de interés con su nombre, dirección, imagen (que se obtiene poniendo el id a continuación de https://app.tussa.org/tussa/api/imagenes/) y coordenadas.

```http
GET https://app.tussa.org/tussa/api/lugares-interes

[
  {
    "id": 1,
    "nombre": "Catedral / Praza do Obradoiro",
    "direccion": "Praza do Obradoiro, s/n, 15704",
    "imagen": "b6ed7f3c-d3bd-11e4-b9d6-1681e6b88ec1",
    "coordenadas": {
      "latitud": 42.880596,
      "longitud": -8.544641
    }
  },
  {...}
]
```
También se pueden crear avisos sobre la llegada de un autobús y calcular rutas, pendiente de investigar.

```http
GET https://app.tussa.org//tussa/api/dispositivos/ca75147d572024f0 

{
  "idioma": "GL",
  "notificacionesActivadas": true
}
```
```http
GET https://app.tussa.org//tussa/api/avisos/ca75147d572024f0 

{}
```
```http
POST https://app.tussa.org//tussa/api/avisos/
{"uuid":"ca75147d572024f0","antelacion":"5","idLinea":40,"idTrayecto":44,"idParada":576,"hora":"22:21","repeticion":["D"]} 

{}
```
```http
POST https://app.tussa.org/tussa/api/rutas/acciones/calcular
{"origen":{"latitud":42.8706512,"longitud":-8.5461194},"destino":{"latitud":42.8919182,"longitud":-8.4216896}}

{"inicio":"Ubicación origen","fin":"Ubicación destino","trayectos":[],"numeroTrayectos":0}
```