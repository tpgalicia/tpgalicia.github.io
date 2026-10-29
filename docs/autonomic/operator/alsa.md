# ALSA

La empresa ALSA opera en la actualidad 3 concesiones de autobús de la Xunta de Galicia: XG642 (Metropolitano de Ferrol), XG719 (Barreiros-Ribadeo, con anexos) y XG881 (Leste da comarca da Coruña). También opera varias rutas nacionales e internacionales con parada en las estaciones gallegas.

## Datos estáticos

Los datos de las líneas de autobuses de ALSA se pueden obtener en formato GTFS desde el [NAP](../other/nap.md) del Ministerio de Transportes y Movilidad Sostenible. La URL del dataset es <https://nap.transportes.gob.es/Files/Detail/932>, en el caso del ofrecido por ALSA; y  <https://nap.transportes.gob.es/Files/Detail/1386>, en el caso del ofrecido por la Xunta de Galicia.

!!! warning "Aviso"
    Estos archivos contienen la totalidad de líneas operadas por ALSA en España y en el caso de los de la Xunta, todos los autobuses gestionados por esta administración.

## Datos en tiempo real

No existe un feed público en un formato estándar (como lo son GTFS-RealTime o SIRI) para acceder a las estimaciones de llegada de los autobuses urbanos en tiempo real. Por tanto, no hay forma de obtener las estimaciones de llegadas a las paradas, ni alertas de servicio ni posiciones de los vehículos.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas API de ALSA o [Xunta](../autonomic/index.md), extraídas de las apps Alsa Regional y Transporte Público de Galicia, respectivamente.

## Paradas

Llamando por HTTP POST con los parámetros adecuados a la siguiente URL se obtienen todas las paradas con su id, nombre largo, nombre corto y coordenadas.

```http
POST https://alsa.es/api/stops/

{
    "info": [
        {
            "id": "15002",
            "name": "PLAZA DE OURENSE PLAZA DE OURENSE",
            "latGPS": "0.75684979",
            "lonGPS": "-0.14669449",
        },
        {...}
    ]
}
```

## Líneas

Llamando por HTTP POST con los parámetros adecuados a la siguiente URL se obtienen todas las líneas con su id, nombre largo, nombre corto y color representativo.

```http
POST https://alsa.es/api/lines/

{
    "info": [
        {
            "id": 11149,
            "name": "A1 ENTREXARDÍNS-LABORAL-A BARCALA-CAMBRE-A PATIÑA-OS CAMPONS",
            "numero": "A1",
            "color": "008DD2",
        },
        {...}
    ]

}
```

### Rutas

Llamando por HTTP POST con los parámetros adecuados  a la siguiente URL se obtienen todas las rutas de una línea con su respectivo id, nombre, sentido (tipo) y color.

```http
POST https://alsa.es/api/rutas

{
    "info": [
        {
            "id": 101,
            "name": "Entrexardins-Cambre-Os Campons",
            "sentido": "I",
            "color": "008DD2"
        },
        {
            "id": 101,
            "name": "Os Campons-Cambre-Entrexardins",
            "sentido": "I",
            "color": "008DD2"
        }
    ]

}
```


### Detalles ruta    

Llamando por HTTP POST con los parámetros adecuados  a la siguiente URL se obtienen los vehículos recorriendo la ruta y las paradas con su respectivo id, nombre, sentido, orden, coordenadas y líneas con enlace.

```http
POST https://alsa.es/api/lineas/paradas

{
    "info": [
        {
            "paradas": [
                {
                    "name": "ENTREXARDINS",
                    "id": 15001,
                    "latitude": "0.75690374",
                    "longitude": "-0.14665775"
                },
        {...}
    ]

}
```




### Estimaciones para una parada

Llamando por HTTP POST con los parámetros adecuados a la siguiente URL se pueden obtener las estimaciones de llegada para una parada, ordenadas por tiempo de manera ascendente, junto a datos de la parada como su nombre y la ubicación.

```http
POST https://alsa.es/stops/estimaciones

{
    "info": [
        {
            "id": "15132",
            "estText": "SIN ESTIMACIÓN EN ESTE MOMENTO"

        },
        {...}
    ]

}
```