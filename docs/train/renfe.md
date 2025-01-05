# Renfe

Renfe es la empresa pública que opera los servicios públicos de media distancia, cercanías y la mayoría de servicios comerciales de larga distancia en España y única en Galicia.

## Datos estáticos

Los datos de los servicios ferroviarios de Renfe se pueden obtener en formato GTFS desde el portal de datos abiertos de Renfe. La URL del dataset es <https://data.renfe.com/dataset?res_format=GTFS>, sin necesidad de autenticación. También están disponibles en el [NAP](../other/nap.md) del Ministerio de Transportes y Movilidad Sostenible. La URL del dataset es <https://nap.transportes.gob.es/Files/Detail/897>, en el caso de Media y Larga Distancia; y  <https://nap.transportes.gob.es/Files/Detail/929>, en el caso de las Cercanías.


## Datos en tiempo real

No existe un feed público en un formato estándar (como lo son GTFS-RealTime o SIRI) para acceder a las estimaciones de llegada de los trenes en tiempo real. Por tanto, no hay forma de obtener las estimaciones de llegadas a las estaciones, ni alertas de servicio ni posiciones de los vehículos.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas API de Renfe, extraídas de la app oficial de la empresa.

### Alertas de servicio

Las alertas sobre modificaciones o incidencias del servicio ferroviario se pueden obtener en formato JSON diferenciado por comunidades en el dataset de su open data <https://data.renfe.com/dataset/avisos>.

### Retrasos y puntualidad de los trenes

Se puede obtener en la siguiente web de la operadora buscando por estación, número de tren o de billete: <https://venta.renfe.com/vol/infoPuntualidadTrenes.do>.

### Estaciones

Se pueden obtener todas las estaciones en la siguiente web de la operadora: <https://horarios.renfe.com/HIRRenfeWeb/estaciones.do> y en <https://www.renfe.com/content/dam/renfe/es/General/buscadores/javascript/estacionesEstaticas.js>.


### Horarios

Se pueden obtener todas las estaciones en la siguiente web de la operadora: <https://horarios.renfe.com/HIRRenfeWeb/buscar.do>

