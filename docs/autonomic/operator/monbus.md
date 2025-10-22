# Monbus

La empresa Monbus (y derivadas) opera en la actualidad la mayoría de concesiones de autobús de la Xunta de Galicia junto a diversas rutas nacionales e internacionales, algunas en colaboración con Flixbus.

## Datos estáticos

Los datos de las líneas de autobuses de Monbus se pueden obtener en formato GTFS desde el [NAP](../other/nap.md) del Ministerio de Transportes y Movilidad Sostenible. La URL del dataset es  <https://nap.transportes.gob.es/Files/Detail/1386>, ofrecido por la Xunta de Galicia.

!!! warning "Aviso"
    Estos archivos contienen la totalidad de líneas gestionadas por la Xunta de Galicia.

## Datos en tiempo real

No existe un feed público en un formato estándar (como lo son GTFS-RealTime o SIRI) para acceder a las estimaciones de llegada de los trenes en tiempo real. Por tanto, no hay forma de obtener las estimaciones de llegadas a las estaciones, ni alertas de servicio ni posiciones de los vehículos.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas APIs de [Xunta](../autonomic/index.md) o FlixBus.

## Paradas

Llamando por HTTP GET a la siguiente URL se pueden buscar paradas usando el parámetro `search`.

```http
GET https://api.checkout.monbus.es/api/stopsSearch/es?search=coruna

{
  "data": {
    "councils": [
      {
        "councilId": "38",
        "council": "Coruña (A)",
        "provinceId": "1",
        "ineCode": "30",
        "stopId": "10932"
      }
    ],
    "importantStops": [
      {
        "id": "10932",
        "type": "stops",
        "attributes": {
          "name": "A Coruña",
          "comment": "Estación de Autobuses",
          "councilId": "38",
          "council": "Coruña (A)",
          "localityId": "18654",
          "locality": "Coruña (A)",
          "provinceId": "1",
          "province": "A Coruña",
          "ineCode": "150300008",
          "isStation": true,
          "equipment": null,
          "type": {
            "id": "2"
          },
          "way": {
            "point": {
              "latitude": 43.353628416076,
              "longitude": -8.4034827441193,
              "radius": 0.05
            }
          },
          "back": {
            "point": {
              "latitude": null,
              "longitude": null,
              "radius": null
            }
          },
          "links": {
            "self": "/stops/10932"
          }
        },
        "relationships": {
          "destinations": {
            "related": "/stops/10932/destinations"
          }
        }
      }
    ]  
```


## Horarios

Llamando por HTTP GET a la siguiente URL se pueden buscar paradas colocando origen/destino/AAAA-MM-DD/1/1

```http
GET https://api.checkout.monbus.es/api/traveloptions/es/10932/10980/2025-01-06/1/1

{
  "data": {
    "departuresGo": {
      "data": [
        {
          "id": "18152553",
          "type": "expeditions",
          "attributes": {
            "sale": true,
            "stepTime": "08:00",
            "stepDate": "2025-01-06",
            "origin": "10932",
            "originTmgId": "257",
            "destination": "10980",
            "destinationTmgId": "38764",
            "line": "11396",
            "expedition": "1120155",
            "way": "1",
            "link": 0,
            "date": "2025-01-06",
            "description": "A Coruña - Ferrol",
            "arrivalHour": "09:30",
            "arrivalDate": "2025-01-06",
            "duration": "01h 30min",
            "onTransit": false,
            "terminated": false,
            "isDirect": null,
            "booking": [
              {
                "bus": 1,
                "free": 55,
                "seats": 55,
                "isSeatNumbering": false
              }
            ],
            "saleTypes": [
              {
                "id": "2",
                "name": "Taquilla"
              },
              {
                "id": "4",
                "name": "Internet"
              },
              {
                "id": "5",
                "name": "En ruta"
              }
            ],
            "company": {
              "id": "101025",
              "type": "companies",
              "attributes": {
                "name": "UTE XG-871",
                "logo": "monbus.png",
                "logoEndpoint": "/assets/company?logo=monbus.png"
              }
            },
            "grant": {
              "id": "485",
              "name": "XG-871"
            },
            "rates": [
              {
                "id": "352",
                "name": "Familia Numerosa Especial",
                "amount": 2.35,
                "fees": 0,
                "feesDetails": [
                  {
                    "name": "Gastos de Gestión",
                    "value": 0
                  }
                ],
                "points": 18.8,
                "isDocumentationRequired": 1,
                "isYoungSummerRate": false,
                "isDefault": 0,
                "percent": "50",
                "travelersType": [
                  {
                    "travelerTypeId": "1",
                    "type": "Adultos/as",
                    "comment": "26 a 59 años"
                  },
                  {
                    "travelerTypeId": "2",
                    "type": "Bebés",
                    "comment": "Hasta los 3 años"
                  },
                  {
                    "travelerTypeId": "3",
                    "type": "Niños/as",
                    "comment": "4 a 11 años"
                  },
                  {
                    "travelerTypeId": "4",
                    "type": "Jóvenes",
                    "comment": "12 a 25 años"
                  },
                  {
                    "travelerTypeId": "5",
                    "type": "Mayores",
                    "comment": "Más de 60 años"
                  }
                ]
              },
              {
                "id": "351",
                "name": "Familia Numerosa General",
                "amount": 3.8,
                "fees": 0,
                "feesDetails": [
                  {
                    "name": "Gastos de Gestión",
                    "value": 0
                  }
                ],
                "points": 30.4,
                "isDocumentationRequired": 1,
                "isYoungSummerRate": false,
                "isDefault": 0,
                "percent": "20",
                "travelersType": [
                  {
                    "travelerTypeId": "1",
                    "type": "Adultos/as",
                    "comment": "26 a 59 años"
                  },
                  {
                    "travelerTypeId": "2",
                    "type": "Bebés",
                    "comment": "Hasta los 3 años"
                  },
                  {
                    "travelerTypeId": "3",
                    "type": "Niños/as",
                    "comment": "4 a 11 años"
                  },
                  {
                    "travelerTypeId": "4",
                    "type": "Jóvenes",
                    "comment": "12 a 25 años"
                  },
                  {
                    "travelerTypeId": "5",
                    "type": "Mayores",
                    "comment": "Más de 60 años"
                  }
                ]
              },
              {
                "id": "313",
                "name": "Normal (sin descuento)",
                "amount": 4.7,
                "fees": 0,
                "feesDetails": [
                  {
                    "name": "Gastos de Gestión",
                    "value": 0
                  }
                ],
                "points": 37.6,
                "isDocumentationRequired": 0,
                "isYoungSummerRate": false,
                "isDefault": 1,
                "percent": "0",
                "travelersType": [
                  {
                    "travelerTypeId": "1",
                    "type": "Adultos/as",
                    "comment": "26 a 59 años"
                  },
                  {
                    "travelerTypeId": "2",
                    "type": "Bebés",
                    "comment": "Hasta los 3 años"
                  },
                  {
                    "travelerTypeId": "3",
                    "type": "Niños/as",
                    "comment": "4 a 11 años"
                  },
                  {
                    "travelerTypeId": "4",
                    "type": "Jóvenes",
                    "comment": "12 a 25 años"
                  },
                  {
                    "travelerTypeId": "5",
                    "type": "Mayores",
                    "comment": "Más de 60 años"
                  }
                ]
              }
            ],
            "typeLine": "paradas"
          }
        },
        {...}
}
```

## Vista web de panel de salidas

Es posible ver una vista web de una parada en <https://tpgal-ws.xunta.monbus.es/?parada=18403&dir=S> usando el parámetro `parada` y `dir` (S o L) y para obtenerlo en JSON <https://tpgal-ws.xunta.monbus.es/apiCurl2.php?parada=18403>.

En el caso de la estación de Vigo existe una vista en la que se puede ver los buses con andenes y si han salido o no: <https://tpgal-ws.xunta.monbus.es/?modo=comsa&dir=s> y en JSON <https://tpgal-ws.xunta.monbus.es/sqlConnect.php?dir=s>
