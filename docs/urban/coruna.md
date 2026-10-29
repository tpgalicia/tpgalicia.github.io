# Urbano de A Coruña

El transporte urbano de A Coruña consiste en un servicio de autobuses urbanos prestado por [Tranvias Coruña](https://tranviascoruna.com), en régimen de concesión por parte del Concello de A Coruña, en precario desde 2025.

## Datos estáticos

Los datos de las líneas de autobuses urbanos de A Coruña se pueden obtener en formato GTFS desde el [NAP](../other/nap.md) del Ministerio de Transportes y Movilidad Sostenible. La URL del dataset es <https://nap.transportes.gob.es/Files/Detail/1376>.

## Datos en tiempo real

Para obtener los datos se puede utilizar la ruta

```
https://tranviasdelacorunha.es/stops/100
```


```json
{

    "buses": {
        "parada": 100,
        "L14" : 5
    }
}
```