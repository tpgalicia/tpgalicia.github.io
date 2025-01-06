# ALSA

La empresa ALSA opera en la actualidad 3 concesiones de autobús de la Xunta de Galicia: XG642 (Metropolitano de Ferrol), XG719 (Barreiros-Ribadeo, con anexos) y XG881 (Leste da comarca da Coruña). También opera varias rutas nacionales e internacionales con parada en las estaciones gallegas.

## Datos estáticos

Los datos de las líneas de autobuses de ALSA se pueden obtener en formato GTFS desde el [NAP](../other/nap.md) del Ministerio de Transportes y Movilidad Sostenible. La URL del dataset es <https://nap.transportes.gob.es/Files/Detail/932>, en el caso del ofrecido por ALSA; y  <https://nap.transportes.gob.es/Files/Detail/1386>, en el caso del ofrecido por la Xunta de Galicia.

!!! warning "Aviso"
    Estos archivos contienen la totalidad de líneas operadas por ALSA en España y en el caso de los de la Xunta, todos los autobuses gestionados por esta administración.

## Datos en tiempo real

No existe un feed público en un formato estándar (como lo son GTFS-RealTime o SIRI) para acceder a las estimaciones de llegada de los autobuses urbanos en tiempo real. Por tanto, no hay forma de obtener las estimaciones de llegadas a las paradas, ni alertas de servicio ni posiciones de los vehículos.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas API de ALSA o [Xunta](../autonomic/index.md), extraídas de las apps Alsa Regional y Transporte Público de Galicia, respectivamente.

## Parámetros para usar la API

Para usar la API de Alsa es necesario hacer peticiones HTTPS POST con diferentes parámetros. El `Content-Type` tendrá siempre el valor `application/json` y en el body los siguientes datos:

```http
{
  "authentication": {
    "date": 20221104,
    "operation": 174032,
    "provider": "ABAMOBILE",
    "time": 153335,
    "token": "1966E8D2D03754E63DA035CD1A83355ECA6172830A838BD1"
  },
  "company": 542,
  "conceCod": 1546
}
```
En el parámetro `company` es necesario poner `541` para Ferrol y `542` para A Coruña, y en `conceCod` los valores `1368` para Ferrol y `1546` para A Coruña.

## Paradas

Llamando por HTTP POST con los parámetros adecuados a la siguiente URL se obtienen todas las paradas con su id, nombre largo, nombre corto y coordenadas (EN RADIANES).

```http
POST https://apps.alsa.es/rest/api/apps/v1/getStops/

{
    "status": "ok",
    "info": [
        {
            "oriCod": "15002",
            "paraCod": "2",
            "origen": "PLAZA DE OURENSE PLAZA DE OURENSE",
            "latGPS": "0.75684979",
            "lonGPS": "-0.14669449",
            "find": "PLAZA DE OURENSE"
        },
        {...}
    ]

}
```

Existen otras variantes como OriStops o DestiStops.

```http
POST https://apps.alsa.es/rest/api/apps/v1/getOriStops/

{
    "status": "ok",
    "info": [
        {
            "oriCod": "15001",
            "origen": "ENTREXARDINS",
            "latGPS": "0.75690374",
            "lonGPS": "-0.14665775",
            "find": "ENTREXARDINS"
        },
        {...}
    ]

}
```

```http
POST https://apps.alsa.es/rest/api/apps/v1/getDestiStops/

{
    "status": "ok",
    "info": [
{
            "desCod": "15001",
            "destino": "ENTREXARDINS",
            "latGPS": "0.75690374",
            "lonGPS": "-0.14665775",
            "find": "ENTREXARDINS"
        },
        {...}
    ]

}
```

!!! note "Equivalencias red urbana-interurbana"

	```http
523 Abente y Lago - 15062-1
1 Porta Real - 15086-1
139 Porta Real, dásena - 15086-2
3 Av. Marina, Obelisco - 15087-1
27 Obelisco - 15087-2
5 Pza. Ourense - 15002-1
25 Pza. Ourense, porto - 15002-2
344 A.Molina, Pza. Madrid -15088-1/15691-1
399 A.Molina, EA - 15088-2
41 Palloza, 5 - 15003-2
30 Av. Oza, gaiteira - 15004-1
39 Av. Oza, 115 - 15004-2
55 Av. Pasaxe, Av. Concordia - 15005-1
20 Os Castros - 15005-2
445 Av. Monelos, 6 - 16541-1
70 Av. Monelos, 141 - 16541-2
363 Av. Monelos, f/ 211 - 16543-1
378 Av. Monelos, 211 - 16543-2
364 Eiria, 40 - 15162-1
377 Monelos, 243 - 15162-2
366 Monserrat, Arces - 16544 - 1
374 Pedralonga, f/4 - 16544-2
368 Fabrica de Armas - 16545-1
373 Pedralonga, 57 - 16545-2
60 Pasaxe, tanatorio - 15006-2
275 Pasaxe, gasolineira - 15007-1
293 Pasaxe, materno - 15007-2
276 Pasaxe, oncoloxico - 15008-1
292 Pasaxe, S.Mª Mar - 15008-2
286 A. Molina, Coliseum - 15089-1
281 A.Molina, Matogrande - 15089-2
346 A.Molina, C.Elviña - 15090-1
279 A.Molina, Ofimático - 15090-2
288 A.Molina, zapateira - 15091-1
289 A.Molina, autoestrada - 15092-1
278 A.Molina, palavea - 15092-2
277 A. Molina, pedralonga - 15093-2
369 Alcampo - 15093-1
370 Santa Xema - 15093-3
371 Pasaxe, Santa Xema - 

```

## Líneas

Llamando por HTTP POST con los parámetros adecuados a la siguiente URL se obtienen todas las líneas con su id, nombre largo, nombre corto y color representativo.

```http
POST https://apps.alsa.es/rest/api/urb/v1/getLines/

{
    "status": "ok",
    "info": [
        {
            "id": 11149,
            "name": "A1 ENTREXARDÍNS-LABORAL-A BARCALA-CAMBRE-A PATIÑA-OS CAMPONS",
            "shortName": "A1",
            "color": "008DD2",
            "colorText": "FFFFFF"
        },
        {...}
    ]

}
```

### Rutas

Llamando por HTTP POST con los parámetros adecuados (los de siempre y además junto a `conceCod` hay que añadir el valor `lineId` que corresponda) a la siguiente URL se obtienen todas las rutas de una línea con su respectivo id, nombre, sentido (tipo) y color.

```http
POST https://apps.alsa.es/rest/api/urb/v1/getJourneys/

{
    "status": "ok",
    "info": [
        {
            "id": 101,
            "name": "Entrexardins-Cambre-Os Campons",
            "type": "I",
            "lineId": 11149,
            "color": "008DD2",
            "colorText": "FFFFFF"
        },
        {
            "id": 101,
            "name": "Os Campons-Cambre-Entrexardins",
            "type": "I",
            "lineId": 11176,
            "color": "008DD2",
            "colorText": "FFFFFF"
        }
    ]

}
```
!!! warning "Aviso"
    Muchas líneas usan distintos id para la ida y para la vuelta.

### Detalles ruta    

Llamando por HTTP POST con los parámetros adecuados (los de siempre y además junto a `conceCod` hay que añadir el valor `lineId` y `journeyId` que corresponda) a la siguiente URL se obtienen los vehículos recorriendo la ruta y las paradas con su respectivo id, nombre, sentido (stopLocationId), orden, coordenadas (EN RADIANES) y líneas con enlace.

```http
POST https://apps.alsa.es/rest/api/urb/v1/getJourneys/

{
    "status": "ok",
    "info": [
        {
            "vehicles": null,
            "jouneyStops": [
                {
                    "order": 1,
                    "name": "ENTREXARDINS",
                    "locationId": 15001,
                    "stopLocationId": 1,
                    "latitude": "0.75690374",
                    "longitude": "-0.14665775",
                    "connections": [
                        11101,
                        11102,
                        11103,
                        11104,
                        11107,
                        11110,
                        11113,
                        11126,
                        11127,
                        11134,
                        11135,
                        11149,
                        11152,
                        11153,
                        11154,
                        11155,
                        11158,
                        11160,
                        11163,
                        11164,
                        11167,
                        11168,
                        11176,
                        11113
                    ]
                },
        {...}
    ]

}
```    
### Forma de ruta

Llamando por HTTP POST con los parámetros adecuados (los de autentificación y en lugar de `company` y `conceCod` usaremos `itiCod` y `linCod`) a la siguiente URL se obtiene la forma en geojson sobre una ruta concreta.

```http
POST https://apps.alsa.es/rest/api/apps/v1/getShape/

{
    "status": "ok",
    "info": {
        "valid": "20250107030000",
        "geojson": {
            "type": "LineString",
            "coordinates": [
                [
                    -8.402852,
                    43.367434
                ],
                [...]
            ]
        }
    }
}
```
### Estimaciones para una parada

Llamando por HTTP POST con los parámetros adecuados (los de siempre y además junto a `conceCod` hay que añadir el valor `lineId`, `locale` que pueden usarse los valores `es`,`gl`,`ca`, `en` y `fr`; `locationId`, `stopLocationId` y `records`) a la siguiente URL se pueden obtener las estimaciones de llegada para una parada, ordenadas por tiempo de manera ascendente, junto a datos de la parada como su nombre y la ubicación.

```http
POST https://apps.alsa.es/rest/api/urb/v1/getDeparturesStop/

{
    "status": "ok",
    "info": [
        {
            "date": "06/01/2025",
            "time": "05:50:00",
            "destId": "15132",
            "destName": "OS CAMPONS (H.ALBA)",
            "latGPS": "0.75690374",
            "lonGPS": "-0.14665775",
            "lineId": "11149",
            "lineName": "A1 ENTREXARDÍNS-LABORAL-A BARCALA-CAMBRE-A PATIÑA-OS CAMPONS",
            "lineShortName": "A1",
            "color": "008DD2",
            "colorText": "FFFFFF",
            "itiId": "101",
            "expeId": "15",
            "oriId": "15001",
            "oriName": "ENTREXARDINS",
            "visit": 0,
            "est": 0,
            "estText": "SIN ESTIMACIÓN EN ESTE MOMENTO",
            "estCol": "0,0,0,1.00"
        },
        {...}
    ]

}
```

## Códigos QR

Es posible crear códigos QR que cuando los leas la aplicación Alsa Regional te muestre datos de esa parada, estes están pegados en algunas paradas. <https://www.alsa.es/tracking-bus?p_p_id=TrackingBusPortlet_WAR_Alsaportlet&_TrackingBusPortlet_WAR_Alsaportlet_javax.portlet.action=trackingBusParadaAction&pueblo=15001&parada=1&p_p_lifecycle=1&p_p_state=normal&p_p_mode=view&r=0&e=542&z=0&c=1546&isa=1> El parámetro `pueblo` es el `oriCod` y `parada` el `paraCod`, los parámetros finales `e` y `c` son `company` y `conceCod` respectivamente.
