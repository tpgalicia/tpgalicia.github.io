# Urbano de Lugo

El transporte urbano de Lugo consiste en un servicio de autobuses urbanos prestado por [AULUSA (Grupo Monbus)](http://urbanoslugo.com/), en régimen de concesión por parte del concello de Lugo.

## Datos estáticos

No existe un feed público en un formato estándar (como lo es GTFS) para acceder a las paradas, líneas y horarios.


## Datos en tiempo real

No existe un feed público en un formato estándar (como lo son GTFS-RealTime o SIRI) para acceder a las estimaciones de llegada de los autobuses urbanos en tiempo real. Por tanto, no hay forma de obtener las estimaciones de llegadas a las paradas, ni alertas de servicio ni posiciones de los vehículos.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas APIs de AULUSA, extraídas de la [web oficial de los QRs](https://info.urbanoslugo.com/qr-demo-paradas/uilP)

### Estimaciones para una parada

Llamando al siguiente endpoint, se pueden obtener las estimaciones de llegada para una parada, ordenadas por tiempo de manera ascendente. Poniendo en el parámetro `sms` un código que de momento está pendiente de investigar como obtenerlos se obtienen los datos.

```http
GET http://indra.sae.monbus.es:8080/EstimacionWebLUGO/estimarWebXml?sms=5006

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