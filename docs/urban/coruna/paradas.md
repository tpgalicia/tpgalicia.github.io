# Paradas

Esta sección describe cómo obtener los próximos buses para una parada y, por tanto, son datos en tiempo real.

Para obtener los datos se puede utilizar la ruta

```
https://itranvias.com/queryitr_v3.php?&func=0&dato=10
```

Donde el parámetro `dato` es el identificador de la parada para la que se quieren consultar los buses. La respuesta tendrá esta forma:

```json
{
    "resultado": "OK",
    "fecha_peticion": "20230922152056",
    "peticion": "jbuses?parada=100&version=2",
    "tama\u00f1o": 700,
    "buses": {
        "parada": 100,
        "lineas": [
            {
                "linea": 500,
                "buses": [
                    {
                        "bus": 385,
                        "tiempo": "<1",
                        "distancia": "186",
                        "estado": 1,
                        "ult_parada": 203
                    },
                    ...
                ],
                ...
            },
            ...
        ]
    }
}
```

El contenido principal se encuentra bajo la clave `buses['paradas']` y, donde existe una entrada para cada línea **activa** (esto es importante, no incluirá aquellas líneas que pasan por la parada pero para las que ya no hay buses activos con ese destino) y, dentro de la clave `buses`, una entrada de diccionario para cada bus con la información:

- Identificador del bus: `id`
- Tiempo que tardará en llegar a la parada: `tiempo`. En minutos pero el valor será _<1_ cuando el bus esté a punto de llegar
- Distancia del bus a la parada en metros: `distancia`
- Estado del bus: `estado`, con los siguientes valores:
    - 0: El bus está en la parada
    - 1: El bus está en movimiento
- Última parada del recorrido por la que pasó el bus: `ult_parada`
