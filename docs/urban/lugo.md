# Urbano de Lugo

El transporte urbano de Lugo consiste en un servicio de autobuses urbanos prestado por [AULUSA (Grupo Monbus)](http://urbanoslugo.com/), en régimen de concesión por parte del concello de Lugo.

## Datos estáticos

No existe un feed público en un formato estándar (como lo es GTFS) para acceder a las paradas, líneas y horarios.


## Datos en tiempo real

No existe un feed público en un formato estándar (como lo son GTFS-RealTime o SIRI) para acceder a las estimaciones de llegada de los autobuses urbanos en tiempo real. Por tanto, no hay forma de obtener las estimaciones de llegadas a las paradas, ni alertas de servicio ni posiciones de los vehículos.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas APIs de AULUSA, extraídas de la [web oficial de los QRs](https://monbusurabnos.com/qr/5006)

### Estimaciones para una parada

Llamando al siguiente endpoint, se pueden obtener las estimaciones de llegada para una parada, ordenadas por tiempo de manera ascendente. Poniendo en el parámetro `parada` un código que de momento está pendiente de investigar como obtenerlos se obtienen los datos.

```http
GET http://urbanoslugo.com/estimaciones?parada=5006

{
  "id": 5006,
  "nombre": "Rda. da Muralla, Sindicatos",
  "coordenadas": {
    "latitud": 42.98696,
    "longitud": -8.09690
  },
  "lineas": [
    {
      "L2": "33 min",
      "L6": "40 min"
    },
    { ... }
  ]
}
```