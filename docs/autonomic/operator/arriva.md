# Arriva

La empresa Arriva opera en la actualidad varias concesiones de autobús de la Xunta de Galicia.

## Datos estáticos

Los datos de las líneas de autobuses de Arriva se pueden obtener en formato GTFS desde el [NAP](../other/nap.md) del Ministerio de Transportes y Movilidad Sostenible. La URL del dataset es  <https://nap.transportes.gob.es/Files/Detail/1386>, ofrecido por la Xunta de Galicia.

!!! warning "Aviso"
    Estos archivos contienen la totalidad de líneas gestionadas por la Xunta de Galicia.

## Datos en tiempo real

No existe un feed público en un formato estándar (como lo son GTFS-RealTime o SIRI) para acceder a las estimaciones de llegada de los trenes en tiempo real. Por tanto, no hay forma de obtener las estimaciones de llegadas a las estaciones, ni alertas de servicio ni posiciones de los vehículos.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas API de Arriva o [Xunta](../autonomic/index.md), extraídas de las apps Arriva-Arteixo y Transporte Público de Galicia, respectivamente.


## Paradas

Llamando por HTTP GET a la siguiente URL se se obtienen todas las paradas con su id, nombre largo y corto, peso y ubicación.

```http
GET https://arriva.es/paradas.json

{
  "paradas": [
    {
      "id": 5274,
      "nombre": "Estación de Coruña (A CORUÑA)",
      "peso": 516,
      "latitud": 43.3531,
      "longitud": -8.4053
    },
    {...}
  ]
}
```


