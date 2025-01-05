# FEVE

FEVE era la empresa pública que operaba los servicios públicos de ancho métrico en España, desde 2015 es gestionado por Renfe.

## Datos estáticos

Los datos de los servicios ferroviarios de FEVE se pueden obtener en formato GTFS desde el portal de datos abiertos de Renfe. La URL del dataset es <https://data.renfe.com/dataset?res_format=GTFS>, sin necesidad de autenticación. También están disponibles en el [NAP](../other/nap.md) del Ministerio de Transportes y Movilidad Sostenible. La URL del dataset es <https://nap.transportes.gob.es/Files/Detail/930>, en el caso de FEVE; y  <https://nap.transportes.gob.es/Files/Detail/929>, en el caso de las Cercanías (Salen los de Ancho Métrico también).

!!! note "Nota"

	Los datos de los trenes Regionales en Ancho Métrico no salen en ningún GTFS actual, solo en los antiguos del open data de Renfe.

## Datos en tiempo real

No existe un feed público en un formato estándar (como lo son GTFS-RealTime o SIRI) para acceder a las estimaciones de llegada de los trenes en tiempo real. Por tanto, no hay forma de obtener las estimaciones de llegadas a las estaciones, ni alertas de servicio ni posiciones de los vehículos.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas API de Renfe, extraídas de la app oficial de la empresa.

### WDSL de FEVE

Existe un WDSL en el que se describen los servicios de la API de FEVE: <https://ram.renfe.es/ServiciosWebHorarios/Service.asmx>.

### API de Renfe

Desde la unificación se ha ido integrando en los servicios de Renfe progresivamente descritos a continuación.

### Alertas de servicio

Las alertas sobre modificaciones o incidencias del servicio ferroviario se pueden obtener en formato JSON diferenciado por comunidades en el dataset de su open data <https://data.renfe.com/dataset/avisos>.

### Retrasos y puntualidad de los trenes

Se puede obtener en la siguiente web de la operadora buscando por estación, número de tren o de billete: <https://venta.renfe.com/vol/infoPuntualidadTrenes.do>.

### Estaciones

Se pueden obtener todas las estaciones en la siguiente web de la operadora: <https://horarios.renfe.com/HIRRenfeWeb/estaciones.do> y en <https://www.renfe.com/content/dam/renfe/es/General/buscadores/javascript/estacionesEstaticas.js>.


### Horarios

Se pueden obtener todas las estaciones en la siguiente web de la operadora: <https://horarios.renfe.com/HIRRenfeWeb/buscar.do> para Regionales y <https://horarios.renfe.com/cer/hjcer300.jsp?NUCLEO=46&CP=NO&I=s#> para las Cercanías de Ferrol.

