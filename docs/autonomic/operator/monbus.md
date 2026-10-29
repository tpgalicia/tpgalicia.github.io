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
GET https://monbus.es/api/stops/es?search=coruna

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
          }
        }
      }
    ]  
```


