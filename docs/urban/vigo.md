# Urbano de Vigo

El transporte urbano de Vigo consiste en un servicio de autobuses urbanos prestado por [Vitrasa](https://www.vitrasa.es), en régimen de concesión por parte del Concello de Vigo.

## Datos estáticos

Los datos de las líneas de autobuses urbanos de Vigo se pueden obtener en formato GTFS desde el portal de datos abiertos del Concello de Vigo. La URL del dataset es <https://nap.transportes.gob.es/Files/Detail/1518>.

!!! note "Nota"

	Los datos de GTFS de Vitrasa en el portal de datos abiertos del Concello de Vigo parecen actualizarse con regularidad, pero el sistema CKAN indica la última actualización erróneamente.

## Datos en tiempo real

No existe un feed público en un formato estándar (como lo son GTFS-RealTime o SIRI) para acceder a las estimaciones de llegada de los autobuses urbanos en tiempo real. Por tanto, no hay forma de obtener las estimaciones de llegadas a las paradas, ni alertas de servicio ni posiciones de los vehículos.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas API del Concello de Vigo, extraídas de la app oficial de la ciudad.

### Alertas de servicio

Llamando por HTTP GET a siguiente URL se obtienen todos los avisos activos pero sin las líneas afectadas. Poniendo el parámetro `tipo` en `TRANSPORTE_AVISOS_ES` se devuelven en castellano, y usando `TRANSPORTE_AVISOS_GL`, en gallego.

```http
GET https://retrasa.es/vigo/avisos

[
	{
		"fin":"2025-01-05",
		"nombre":"SERVICIO ESPECIAL CABALGATA DE REYES 2025",
		"fecha":"03-01-2025",
		"id":2407
	},
	{ ... }
]
```

Y mediante este otro endpoint, la correlación entre IDs y líneas afectadas. El parámetro lang es necesario, aunque no se devuelva texto en ninguno de los dos idiomas. El valor 1 indica "castellano" y el valor 0, "gallego".

```http
GET https://retrasa.es/vigo/avisos-lineas/lang=0

[
    {
        "lines": "A",
        "fecha": "2025-01-03",
        "id": 2407,
        "fin": "2025-01-05"
    },
	{ ... }
]
```

### Estimaciones para una parada

Llamando al siguiente endpoint, se pueden obtener las estimaciones de llegada para una parada, ordenadas por tiempo de manera ascendente, junto a datos de la parada como su nombre y la ubicación.

```http
GET https://bigo.es/bus/estimaciones/14264

{
    "parada": [
        {
            "latitud": 42.235873545,
            "longitud": -8.720083317,
            "parada": 14264,
            "nombre": "Rúa de Urzáiz - Príncipe"
        }
    ],
    "buses": [
        {
            "tiempo": 4,
            "linea": "C1"},
        { ... },
    ]
}
```