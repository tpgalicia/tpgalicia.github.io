# Urbano de Vigo

El transporte urbano de Vigo consiste en un servicio de autobuses urbanos prestado por [Vitrasa](https://www.vitrasa.es), en régimen de concesión por parte del Concello de Vigo.

## Datos estáticos

Los datos de las líneas de autobuses urbanos de Vigo se pueden obtener en formato GTFS desde el portal de datos abiertos del Concello de Vigo. La URL del dataset es <https://datos-ckan.vigo.org/dataset/gtfs-vitrasa>, sin necesidad de autenticación.

!!! note "Nota"

	Los datos de GTFS de Vitrasa en el portal de datos abiertos del Concello de Vigo parecen actualizarse con regularidad, pero el sistema CKAN indica la última actualización erróneamente.

## Datos en tiempo real

No existe un feed público en un formato estándar (como lo son GTFS-RealTime o SIRI) para acceder a las estimaciones de llegada de los autobuses urbanos en tiempo real. Por tanto, no hay forma de obtener las estimaciones de llegadas a las paradas, ni alertas de servicio ni posiciones de los vehículos.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas API del Concello de Vigo, extraídas de la app oficial de la ciudad.

### Alertas de servicio

Llamando por HTTP GET a siguiente URL se obtienen todos los avisos activos pero sin las líneas afectadas. Poniendo el parámetro `tipo` en `TRANSPORTE_AVISOS_ES` se devuelven en castellano, y usando `TRANSPORTE_AVISOS_GL`, en gallego.

```http
GET https://datos.vigo.org/vci_api_app/api2.jsp?tipo=TRANSPORTE_AVISOS_ES

[
	{
		"id_subcategoria":26,
		"fecha_fin_publicacion":"2025-01-05",
		"id_categoria":20,
		"categoria":"Transporte",
		"nombre":"SERVICIO ESPECIAL CABALGATA DE REYES 2025",
		"fecha_publicacion":"03-01-2025",
		"id_publicacion":2407
	},
	{ ... }
]
```

Y mediante este otro endpoint, la correlación entre IDs y líneas afectadas. El parámetro lang es necesario, aunque no se devuelva texto en ninguno de los dos idiomas. El valor 1 indica "castellano" y el valor 0, "gallego".

```http
GET https://datos.vigo.org/vci_api_app/api2.jsp?tipo=WEBPUB_AVISOS_TRANSPORTE&lang=1

[
    {
        "lineas_afectadas": "A",
        "fecha_inicio": "2025-01-03",
        "id": 2407,
        "fecha_fin": "2025-01-05"
    },
	{ ... }
]
```

### Estimaciones para una parada

Llamando al siguiente endpoint, se pueden obtener las estimaciones de llegada para una parada, ordenadas por tiempo de manera ascendente, junto a datos de la parada como su nombre y la ubicación. Para escoger la parada, hay que fijar el parámetro `id` de la query al código de parada, teniendo en cuenta que en el GTFS, por ejemplo, se suelen prefijar con `P00` o similares, y ese número no lo va a reconocer.

```http
GET https://datos.vigo.org/vci_api_app/api2.jsp?tipo=TRANSPORTE-ESTIMACION-PARADA&id=14264

{
    "parada": [
        {
            "latitud": 42.235873545,
            "longitud": -8.720083317,
            "stop_vitrasa": 14264,
            "nombre": "Rúa de Urzáiz - Príncipe"
        }
    ],
    "estimaciones": [
        {
            "minutos": 4,
            "ruta": "P.AMÉRICA",
            "linea": "C1",
            "metros": 788
        },
        { ... },
    ]
}
```

A partir de estos datos de estimaciones, especialmente el de distancia (metros), se podría calcular la posición aproximada de los vehículos, usando los datos del `shapes.txt` del GTSF y heurísticas para encontrar el viaje correcto.

## _Scraping_

De manera alternativa, se pueden obtener los datos de avisos y tiempo real mediante Web Scraping, muy similar a esta API pero teniendo que procesar los HTML.

### Avisos

La URL es `https://vitrasa.es/avisos` y el HTML de los avisos se puede obtener, por ejemplo, con el siguiente JavaScript:

```js
document
	.querySelectorAll("#v-pills-tabContent .tab-pane")
	.values()
	.map(p => p.innerHTML)
```

### Estimaciones de una parada

La URL es `http://infobus.vitrasa.es:8002/Default.aspx?parada=14264` (mediante HTTP plano, no soporta HTTPS), cambiando "parada" por el ID de la parada a consultar. Para sacar las estimaciones, se puede usar, por ejemplo, este JavaScript:

```js
document.querySelectorAll("#GridView1 > tbody > tr")
	.values()
	.map(tr => tr.querySelectorAll("td"))
	.filter(l => l.length === 3)
```

Es importante filtrar los `td` donde solo hay tres elementos, porque la "UI" utiliza tablas para todo el diseño, incluyendo la paginación en la parte inferior. Esos tres elementos corresponden, en este orden a "linea", "ruta", "minutos". 

!!! note "Nota"

	Usar la paginación es posible, pero complicado, ya que hay que procesar la primera página, y sacar variables como ViewState, y hacer un POST para obtenerla. Por ello, es mucho más sencillo y eficiente usar la API descrita anteriormente.
