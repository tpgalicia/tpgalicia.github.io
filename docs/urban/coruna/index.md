# Urbano de A Coruña

El transporte urbano de A Coruña consiste en un servicio de autobuses urbanos prestado por [Tranvias Coruña](https://tranviascoruna.com), en régimen de concesión por parte del Concello de A Coruña.

## Datos estáticos

Los datos de las líneas de autobuses urbanos de A Coruña se pueden obtener en formato GTFS desde el [NAP](../other/nap.md) del Ministerio de Transportes y Movilidad Sostenible. La URL del dataset es <https://nap.transportes.gob.es/Files/Detail/1376>.

Además, el Concello dispone de un servidor FTP con el historial de feeds GTFS para el ayuntamiento, al que se puede acceder a través de `ftp://tranviasro:TR4nV14S.ro@ftp.coruna.es/`.

El feed GTFS solo incluye los archivos obligatorios `agency.txt`, `routes.txt`, `trips.txt`, `stops.txt`, `stop_times.txt`, `calendar.txt` y `calendar_dates.txt` y, también, `shapes.txt`.

## Datos en tiempo real

Esta página documenta la API que utiliza la página [iTranvías](https://itranvias.com) de la [Compañía de Tranvías de **La** Coruña](https://tranviascoruna.com), que a la que he hecho *ingeniería inversa* durante el desarrollo de mi página alternativa [bus.delthia.com](https://bus.delthia.com).

!!! warning "Aviso"
    Es posible que no haya descubierto toda la funcionalidad, o que haya maneras diferentes de utilizar los parámetros para obtener otros resultados o información adicional. Esta es mi mejor apuesta sobre el funcionamiento de la API según lo observado a través de la página de *iTranvias* y una pequeña investigación

### Contenidos

- [Información general](general/): Datos generales sobre el sistema de transporte
    - [Líneas](general#lineas): Líneas y sus recorridos
    - [Paradas](general#paradas): Paradas y las rutas que pasan por las mismas
    - [Enlaces](general#enlaces): Enlaces permitidos y su coste
    - [Precios](general#precios): Tarifas disponibles
- [Paradas](paradas/): Próximos buses para una parada
- [Líneas](lineas/): Información sobre una línea
    - Posición de los buses sobre el recorrido
    - Posición geográfica de los buses
    - Horas de salida
    - Trazado de una línea
