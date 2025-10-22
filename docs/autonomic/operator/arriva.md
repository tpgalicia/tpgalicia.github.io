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
GET https://arriva.gal/plataforma/api/superparadas/index/buscador.json

{
  "paradas": [
    {
      "parada": 5274,
      "nombre": "Estación de Coruña (A CORUÑA)",
      "nom_web": "Estación de Coruña",
      "peso": 516,
      "lat": 43.3531,
      "lon": -8.4053,
      "latitud": 43.3531,
      "longitud": -8.4053
    },
    {...}
  ]
}
```
### Paradas por origen

Llamando por HTTP GET a la siguiente URL se se obtienen todas las paradas con su id, nombre largo y corto, peso y ubicación con respecto a un origen.

```http
GET https://arriva.gal/plataforma/api/superparadas/por-origen/5274/buscador.json

[
  {
    "parada": 4802,
    "nombre": "Arteixo (ARTEIXO)",
    "nom_web": "Arteixo",
    "peso": 229,
    "lat": 43.3064,
    "lon": -8.5072
  },
  {...}
]

```

### Ver parada

Llamando por HTTP GET a la siguiente URL con su respectivo id se se obtienen detalles sobre una parada como nombres corto y largo, ayuntamiento, coordenadas, distintos id de la xunta 

```http
GET https://arriva.gal/plataforma/api/superparadas/view/5505.json

{
  "parada": {
    "id": 5505,
    "nombre": "Fofelle",
    "lat": 43.249,
    "lon": -8.5687,
    "gps_n": 4324900,
    "gps_w": 856870,
    "ayuntamiento_id": 131,
    "deshabilitada": false,
    "manual": false,
    "paradaexpediciones_count": 114,
    "peso_mod": 0,
    "created": "2020-01-26T03:09:44+01:00",
    "modified": "2020-01-27T21:36:32+01:00",
    "paradas": [
      {
        "parada": 2534,
        "nom_parada": "Fofelle",
        "gps_n": 237868959,
        "gps_w": 85691680,
        "ayunta_fisico": 131,
        "destacar_parada_intermedia": false,
        "nom_web": "Fofelle",
        "paradaexpediciones_count": 109,
        "peso_mod": 0,
        "deshabilitada": false,
        "nuevo": false,
        "asimilado_a": null,
        "lat1": 43.249,
        "lon1": -8.5687,
        "lat2": 43.2483,
        "lon2": -8.5696,
        "geoloc_desde": null,
        "geoloc_fecha": null,
        "lat": 43.2486,
        "lon": -8.56915,
        "gescar_id": "2534",
        "id_simob": "15041-205",
        "ayunta_fisico_simob": 15041,
        "_joinData": {
          "id": 6086,
          "parada_id": 2534,
          "superparada_id": 5505,
          "created": null
        },
        "parada_expediciones": [
          {
            "parex": 112861,
            "expedicion": 1362,
            "linea": 187,
            "ordinal": 27,
            "parada": 2534,
            "gps_n_ida": 43249010,
            "gps_w_ida": 8568700,
            "gps_n_vuelta": 43248270,
            "gps_w_vuelta": 8569600,
            "kms_or": 238,
            "min_or": 49,
            "horario": "2025-01-07T12:39:00+01:00",
            "revisado": false,
            "deshabilitada": false,
            "parlin": 37138,
            "creado": false,
            "parada_asimilada_id": null,
            "horario_xunta": "2025-01-07T12:39:00+01:00",
            "horario_manual": null,
            "horario_calculado": null,
            "expedicion_id": 1362,
            "linea_id": 187,
            "expedicion_asoc": {
              "id": 1362,
              "expediciones": 35782,
              "linea_exped": 187,
              "nom_exped": "Entrexardíns-Carballo E.A.",
              "nom_exped_abrev": "Marineda City",
              "origen": 95546,
              "id_par_origen": 15384,
              "ord_origen": 1,
              "destino": 37149,
              "id_par_destino": 843,
              "ord_destino": 38,
              "sentido": 1,
              "frec_sem_exped": 3,
              "temp_anu_exped": 1,
              "hora_salida": "2025-01-07T11:50:00+01:00",
              "hora_llegada": "2025-01-07T12:55:00+01:00",
              "virtual": 0,
              "v_info": "undefined",
              "fecha_desde": "2018-02-26T00:00:00+01:00",
              "fecha_hasta": "2020-12-22T23:59:59+01:00",
              "Descripcion_Web": "Entrexardíns-Carballo E.A.",
              "revisado": true,
              "clonado": false,
              "nuevo": false,
              "asimilado_a": null,
              "gescar_id": "35782",
              "partir_circular": 0,
              "linea_id": 187,
              "estimacion_plazas_reservadas": null,
              "integrada": null
            }
          },
          {...}
          }
        ],
        "peso": 109,
        "is_geoloc": true,
        "is_xunta_geoloc": true,
        "wgs84_lat": "43248600",
        "wgs84_lon": "-8569150"
      }
    ],
    "peso": 114,
    "latitud": 43.249,
    "longitud": -8.5687
  }
}

```

## Expediciones

Llamando por HTTP GET a la siguiente URL se pueden buscar paradas colocando origen/destino/DD-MM-AAAA

```http
GET https://arriva.gal/plataforma/api/buscador/search/5274/4802/07-01-2025.json

{
  "expediciones": {
    "ida": [
      {
        "id": 6317,
        "expediciones": 112957,
        "linea_exped": 10399,
        "nom_exped": "Coruña E.A.-Arteixo",
        "nom_exped_abrev": "",
        "origen": 154833,
        "id_par_origen": 257,
        "ord_origen": 1,
        "destino": 155272,
        "id_par_destino": 810,
        "ord_destino": 15,
        "sentido": 1,
        "frec_sem_exped": 2,
        "temp_anu_exped": 1,
        "hora_salida": "2025-01-07T06:30:00+01:00",
        "hora_llegada": "2025-01-07T07:08:00+01:00",
        "virtual": 0,
        "v_info": "undefined",
        "fecha_desde": "2024-06-22T00:00:00+02:00",
        "fecha_hasta": "3000-12-12T23:59:59+01:00",
        "Descripcion_Web": "Coruña E.A. - Arteixo",
        "revisado": true,
        "clonado": false,
        "nuevo": false,
        "asimilado_a": null,
        "gescar_id": "112957",
        "partir_circular": 0,
        "linea_id": 846,
        "estimacion_plazas_reservadas": 0,
        "integrada": false,
        "tarifas_vendibles": [],
        "parada_destino": {
          "parada": 810,
          "nom_parada": "Arteixo",
          "gps_n": 433063887,
          "gps_w": 46789539,
          "ayunta_fisico": 14,
          "destacar_parada_intermedia": false,
          "nom_web": "Arteixo",
          "paradaexpediciones_count": 279,
          "peso_mod": 0,
          "deshabilitada": false,
          "nuevo": false,
          "asimilado_a": null,
          "lat1": 43.3065,
          "lon1": -8.50726,
          "lat2": 43.3064,
          "lon2": -8.50722,
          "geoloc_desde": null,
          "geoloc_fecha": null,
          "lat": 43.3064,
          "lon": -8.50724,
          "gescar_id": "810",
          "id_simob": "15005-39",
          "ayunta_fisico_simob": 15005,
          "peso": 279,
          "is_geoloc": true,
          "is_xunta_geoloc": true,
          "wgs84_lat": "43306400",
          "wgs84_lon": "-8507240"
        },
        "parada_origen": {
          "parada": 257,
          "nom_parada": "Coruña E.A.",
          "gps_n": 433536198,
          "gps_w": 840384,
          "ayunta_fisico": 1,
          "destacar_parada_intermedia": false,
          "nom_web": "Estación de Coruña",
          "paradaexpediciones_count": 433,
          "peso_mod": 0,
          "deshabilitada": false,
          "nuevo": false,
          "asimilado_a": null,
          "lat1": 43.3531,
          "lon1": -8.4053,
          "lat2": 43.3531,
          "lon2": -8.4053,
          "geoloc_desde": null,
          "geoloc_fecha": null,
          "lat": 43.3531,
          "lon": -8.4053,
          "gescar_id": "257",
          "id_simob": "15030-1",
          "ayunta_fisico_simob": 15030,
          "peso": 433,
          "is_geoloc": true,
          "is_xunta_geoloc": true,
          "wgs84_lat": "43353100",
          "wgs84_lon": "-8405300"
        },
        "parada_expediciones": [
          {
            "horaSalida": "06:30",
            "parex": 284126,
            "expedicion": 112957,
            "linea": 10399,
            "ordinal": 1,
            "parada": 257,
            "gps_n_ida": 433535368,
            "gps_w_ida": 8404557,
            "gps_n_vuelta": 433537558,
            "gps_w_vuelta": 84035126,
            "kms_or": 0,
            "min_or": 0,
            "horario": "2025-01-07T06:30:00+01:00",
            "revisado": true,
            "deshabilitada": false,
            "parlin": 154833,
            "creado": false,
            "parada_asimilada_id": null,
            "horario_xunta": "2025-01-07T06:30:00+01:00",
            "horario_manual": null,
            "horario_calculado": null,
            "expedicion_id": 6317,
            "linea_id": null,
            "parada_asoc": {
              "parada": 257,
              "nom_parada": "Coruña E.A.",
              "gps_n": 433536198,
              "gps_w": 840384,
              "ayunta_fisico": 1,
              "destacar_parada_intermedia": false,
              "nom_web": "Estación de Coruña",
              "paradaexpediciones_count": 433,
              "peso_mod": 0,
              "deshabilitada": false,
              "nuevo": false,
              "asimilado_a": null,
              "lat1": 43.3531,
              "lon1": -8.4053,
              "lat2": 43.3531,
              "lon2": -8.4053,
              "geoloc_desde": null,
              "geoloc_fecha": null,
              "lat": 43.3531,
              "lon": -8.4053,
              "gescar_id": "257",
              "id_simob": "15030-1",
              "ayunta_fisico_simob": 15030,
              "peso": 433,
              "is_geoloc": true,
              "is_xunta_geoloc": true,
              "wgs84_lat": "43353100",
              "wgs84_lon": "-8405300"
            }
          },
          {
            "horaSalida": "07:08",
            "parex": 284140,
            "expedicion": 112957,
            "linea": 10399,
            "ordinal": 15,
            "parada": 810,
            "gps_n_ida": 433064023,
            "gps_w_ida": 85071836,
            "gps_n_vuelta": 433063751,
            "gps_w_vuelta": 8507242,
            "kms_or": 133,
            "min_or": 38,
            "horario": "2025-01-07T07:08:00+01:00",
            "revisado": true,
            "deshabilitada": false,
            "parlin": 155272,
            "creado": false,
            "parada_asimilada_id": null,
            "horario_xunta": "2025-01-07T07:08:00+01:00",
            "horario_manual": null,
            "horario_calculado": null,
            "expedicion_id": 6317,
            "linea_id": null,
            "parada_asoc": {
              "parada": 810,
              "nom_parada": "Arteixo",
              "gps_n": 433063887,
              "gps_w": 46789539,
              "ayunta_fisico": 14,
              "destacar_parada_intermedia": false,
              "nom_web": "Arteixo",
              "paradaexpediciones_count": 279,
              "peso_mod": 0,
              "deshabilitada": false,
              "nuevo": false,
              "asimilado_a": null,
              "lat1": 43.3065,
              "lon1": -8.50726,
              "lat2": 43.3064,
              "lon2": -8.50722,
              "geoloc_desde": null,
              "geoloc_fecha": null,
              "lat": 43.3064,
              "lon": -8.50724,
              "gescar_id": "810",
              "id_simob": "15005-39",
              "ayunta_fisico_simob": 15005,
              "peso": 279,
              "is_geoloc": true,
              "is_xunta_geoloc": true,
              "wgs84_lat": "43306400",
              "wgs84_lon": "-8507240"
            }
          }
        ],
        "linea": {
          "id": 846,
          "conc_admin_l": 848,
          "lineas": 10399,
          "nom_linea": "Coruña E.A.-Arteixo",
          "par_ori": 257,
          "par_des": 810,
          "Descripcion_Web_Ida": "CORUÑA E.A.-ARTEIXO (POR MEICENDE)",
          "Descripcion_Web_Vuelta": "ARTEIXO-CORUÑA E.A. (POR MEICENDE)",
          "fecha_desde": "2024-06-22T00:00:00+02:00",
          "fecha_hasta": "3000-12-12T23:59:59+01:00"
        },
        "_matchingData": {
          "ParadaExpediciones": {
            "parex": 284126,
            "expedicion": 112957,
            "linea": 10399,
            "ordinal": 1,
            "parada": 257,
            "gps_n_ida": 433535368,
            "gps_w_ida": 8404557,
            "gps_n_vuelta": 433537558,
            "gps_w_vuelta": 84035126,
            "kms_or": 0,
            "min_or": 0,
            "horario": "2025-01-07T06:30:00+01:00",
            "revisado": true,
            "deshabilitada": false,
            "parlin": 154833,
            "creado": false,
            "parada_asimilada_id": null,
            "horario_xunta": "2025-01-07T06:30:00+01:00",
            "horario_manual": null,
            "horario_calculado": null,
            "expedicion_id": 6317,
            "linea_id": null
          },
          "TemporadasAnuales": {
            "temp_anu": 1,
            "nom_temp": "Todo o ano",
            "Descripción_Web": "Todo el año",
            "created": null,
            "modified": "2022-01-01T04:43:18+01:00",
            "creada": false
          },
          "CalerangDet": {
            "rnd_idemp": 267,
            "rnd_idcalerang": 1,
            "rnd_id": 1,
            "rnd_desde": "2000-01-01T00:00:00+00:00",
            "rnd_hasta": "2222-12-31T00:00:00+00:00",
            "created": null,
            "modified": null
          },
          "FrecuenciasSemanales": {
            "frec_sem": 2,
            "nom_frec": "De luns a venres - Non festivos",
            "Dias": "LMXJV",
            "Obserbaciones": null,
            "Tiene_Observaciones": "No",
            "created": null,
            "modified": "2022-01-01T04:43:18+01:00",
            "creada": false
          },
          "Frecdesa": {
            "frd_idemp": 267,
            "frd_idfre": 2,
            "frd_dia": 2,
            "frd_idtdia": 1,
            "frd_acti": 1,
            "created": null,
            "modified": null
          },
          "TiposDia": {
            "Cod": 1,
            "TipoDia": "NN",
            "Definicion": "Normal",
            "Lunes_L": -1,
            "Lunes_F": 0,
            "Martes_L": -1,
            "Martes_F": 0,
            "Miercoles_L": -1,
            "Miercoles_F": 0,
            "Jueves_L": -1,
            "Jueves_F": 0,
            "Viernes_L": -1,
            "Viernes_F": 0,
            "Sabado_L": -1,
            "Sabado_F": 0,
            "Domingo": -1
          },
          "Diasanyo": {
            "Fecha": "2025-01-07T00:00:00+00:00",
            "Dia": "MARTES",
            "TipoDia": "NN",
            "DiaSem": "2",
            "NUMDIA": 7,
            "NUMSEMANA": 2,
            "NUMMES": 1,
            "fecha_texto": "2025-01-07"
          }
        },
        "tarifa_basica": 155,
        "gmvPrices": [],
        "bus": {
          "id": 776,
          "name": 776,
          "marca": null,
          "modelo": "633",
          "caracteristicas": [],
          "conductor": 4017,
          "posicion": {
            "lat": null,
            "lon": null,
            "long": null,
            "course": null,
            "direction": null,
            "direction_text": null
          },
          "last_stop": {
            "timestamp": null,
            "parada_id": null,
            "fecha": null
          },
          "estado": null
        }
      },
```

### Ver expedición

Llamando por HTTP GET a la siguiente URL se se obtienen todas las paradas con su id, nombre largo y corto, peso y ubicación con respecto a un origen.

```http
GET https://arriva.gal/plataforma/api/expediciones/get/6317.json

{
  "expedicion": {
    "id": 6317,
    "expediciones": 112957,
    "linea_exped": 10399,
    "nom_exped": "Coruña E.A.-Arteixo",
    "nom_exped_abrev": "",
    "origen": 154833,
    "id_par_origen": 257,
    "ord_origen": 1,
    "destino": 155272,
    "id_par_destino": 810,
    "ord_destino": 15,
    "sentido": 1,
    "frec_sem_exped": 2,
    "temp_anu_exped": 1,
    "hora_salida": "2025-01-07T06:30:00+01:00",
    "hora_llegada": "2025-01-07T07:08:00+01:00",
    "virtual": 0,
    "v_info": "undefined",
    "fecha_desde": "2024-06-22T00:00:00+02:00",
    "fecha_hasta": "3000-12-12T23:59:59+01:00",
    "Descripcion_Web": "Coruña E.A. - Arteixo",
    "revisado": true,
    "clonado": false,
    "nuevo": false,
    "asimilado_a": null,
    "gescar_id": "112957",
    "partir_circular": 0,
    "linea_id": 846,
    "estimacion_plazas_reservadas": 0,
    "integrada": false,
    "planning_hoy": {
      "PLA_TYPE": "G",
      "PLA_RECNUM": 14242192,
      "expedicion_id": 6317,
      "PLA_DETAIL": "112957",
      "PLA_DATE": "2025-01-07T00:00:00+00:00",
      "PLA_HDEP": "2025-01-07T06:30:00+01:00",
      "PLA_HRET": "2025-01-07T07:08:00+01:00",
      "VEH_REF": 776,
      "CON_REF": 4017,
      "ACT_NOM": "848",
      "CLI_NOM": "XUNTA GALICIA 357",
      "PLA_TOTKM": 13,
      "PLA_SERNOM": "6013",
      "PLA_SERVAR": "XLO",
      "PLA_LDEP": "257-CORUÑA E.A. (A CORUÑA)",
      "PLA_LRET": "810-ARTEIXO (ARTEIXO)",
      "ETA_NOM": null,
      "gescar_desc": "CORUÑA E.A.-ARTEIXO",
      "expediciones": 112957,
      "cod_plan": null,
      "end_detected": false,
      "PLA_LDEP_id": 257,
      "PLA_LRET_id": 810,
      "bajo_demanda": false,
      "horas_paso_webfleet_matched": null,
      "webfleet_pasos_paradas_count": null,
      "gmv_pasos_paradas_count": null,
      "created": "2025-01-06T01:40:16+01:00",
      "modified": "2025-01-06T23:51:07+01:00",
      "is_abierta": null,
      "is_detectada_sae": false,
      "is_sae": true,
      "is_xg": true
    },
    "tarifas_vendibles": [],
    "prohibiciones": [],
    "frecuencia_semanal": {
      "frec_sem": 2,
      "nom_frec": "De luns a venres - Non festivos",
      "Dias": "LMXJV",
      "Obserbaciones": null,
      "Tiene_Observaciones": "No",
      "created": null,
      "modified": "2022-01-01T04:43:18+01:00",
      "creada": false
    },
    "temporada_anual": {
      "temp_anu": 1,
      "nom_temp": "Todo o ano",
      "Descripción_Web": "Todo el año",
      "created": null,
      "modified": "2022-01-01T04:43:18+01:00",
      "creada": false
    },
    "parada_expediciones": [
      {
        "parex": 284126,
        "expedicion": 112957,
        "linea": 10399,
        "ordinal": 1,
        "parada": 257,
        "gps_n_ida": 433535368,
        "gps_w_ida": 8404557,
        "gps_n_vuelta": 433537558,
        "gps_w_vuelta": 84035126,
        "kms_or": 0,
        "min_or": 0,
        "horario": "2025-01-07T06:30:00+01:00",
        "revisado": true,
        "deshabilitada": false,
        "parlin": 154833,
        "creado": false,
        "parada_asimilada_id": null,
        "horario_xunta": "2025-01-07T06:30:00+01:00",
        "horario_manual": null,
        "horario_calculado": null,
        "expedicion_id": 6317,
        "linea_id": null,
        "parada_asoc": {
          "parada": 257,
          "nom_parada": "Coruña E.A.",
          "gps_n": 433536198,
          "gps_w": 840384,
          "ayunta_fisico": 1,
          "destacar_parada_intermedia": false,
          "nom_web": "Estación de Coruña",
          "paradaexpediciones_count": 433,
          "peso_mod": 0,
          "deshabilitada": false,
          "nuevo": false,
          "asimilado_a": null,
          "lat1": 43.3531,
          "lon1": -8.4053,
          "lat2": 43.3531,
          "lon2": -8.4053,
          "geoloc_desde": null,
          "geoloc_fecha": null,
          "lat": 43.3531,
          "lon": -8.4053,
          "gescar_id": "257",
          "id_simob": "15030-1",
          "ayunta_fisico_simob": 15030,
          "superparadas": [
            {
              "id": 5274,
              "nombre": "Estación de Coruña",
              "lat": 43.3531,
              "lon": -8.4053,
              "gps_n": 0,
              "gps_w": 0,
              "ayuntamiento_id": 1,
              "deshabilitada": false,
              "manual": false,
              "paradaexpediciones_count": 516,
              "peso_mod": 0,
              "created": "2020-01-26T03:09:40+01:00",
              "modified": "2022-04-30T14:16:52+02:00",
              "_joinData": {
                "id": 5840,
                "parada_id": 257,
                "superparada_id": 5274,
                "created": null
              },
              "peso": 516,
              "latitud": 43.3531,
              "longitud": -8.4053
            }
          ],
          "peso": 433,
          "is_geoloc": true,
          "is_xunta_geoloc": true,
          "wgs84_lat": "43353100",
          "wgs84_lon": "-8405300"
        }
      },
      ,
    "linea": {
      "id": 846,
      "conc_admin_l": 848,
      "lineas": 10399,
      "nom_linea": "Coruña E.A.-Arteixo",
      "par_ori": 257,
      "par_des": 810,
      "Descripcion_Web_Ida": "CORUÑA E.A.-ARTEIXO (POR MEICENDE)",
      "Descripcion_Web_Vuelta": "ARTEIXO-CORUÑA E.A. (POR MEICENDE)",
      "fecha_desde": "2024-06-22T00:00:00+02:00",
      "fecha_hasta": "3000-12-12T23:59:59+01:00"
    }
  }
}

```

### Ver expediciones por parada

Llamando por HTTP GET a la siguiente URL con su respectivo id se se obtienen detalles sobre una parada como nombres corto y largo, ayuntamiento, coordenadas, distintos id de la xunta 

```http
GET https://arriva.gal/plataforma/api/superparadas/expediciones-fecha/5505.json

{
  "parada": {
    "id": 5505,
    "nombre": "Fofelle",
    "lat": 43.249,
    "lon": -8.5687,
    "gps_n": 4324900,
    "gps_w": 856870,
    "ayuntamiento_id": 131,
    "deshabilitada": false,
    "manual": false,
    "paradaexpediciones_count": 114,
    "peso_mod": 0,
    "created": "2020-01-26T03:09:44+01:00",
    "modified": "2020-01-27T21:36:32+01:00",
    "paradas": [
      {
        "parada": 2534,
        "nom_parada": "Fofelle",
        "gps_n": 237868959,
        "gps_w": 85691680,
        "ayunta_fisico": 131,
        "destacar_parada_intermedia": false,
        "nom_web": "Fofelle",
        "paradaexpediciones_count": 109,
        "peso_mod": 0,
        "deshabilitada": false,
        "nuevo": false,
        "asimilado_a": null,
        "lat1": 43.249,
        "lon1": -8.5687,
        "lat2": 43.2483,
        "lon2": -8.5696,
        "geoloc_desde": null,
        "geoloc_fecha": null,
        "lat": 43.2486,
        "lon": -8.56915,
        "gescar_id": "2534",
        "id_simob": "15041-205",
        "ayunta_fisico_simob": 15041,
        "_joinData": {
          "id": 6086,
          "parada_id": 2534,
          "superparada_id": 5505,
          "created": null
        },
        "parada_expediciones": [
          {
            "parex": 112861,
            "expedicion": 1362,
            "linea": 187,
            "ordinal": 27,
            "parada": 2534,
            "gps_n_ida": 43249010,
            "gps_w_ida": 8568700,
            "gps_n_vuelta": 43248270,
            "gps_w_vuelta": 8569600,
            "kms_or": 238,
            "min_or": 49,
            "horario": "2025-01-07T12:39:00+01:00",
            "revisado": false,
            "deshabilitada": false,
            "parlin": 37138,
            "creado": false,
            "parada_asimilada_id": null,
            "horario_xunta": "2025-01-07T12:39:00+01:00",
            "horario_manual": null,
            "horario_calculado": null,
            "expedicion_id": 1362,
            "linea_id": 187,
            "expedicion_asoc": {
              "id": 1362,
              "expediciones": 35782,
              "linea_exped": 187,
              "nom_exped": "Entrexardíns-Carballo E.A.",
              "nom_exped_abrev": "Marineda City",
              "origen": 95546,
              "id_par_origen": 15384,
              "ord_origen": 1,
              "destino": 37149,
              "id_par_destino": 843,
              "ord_destino": 38,
              "sentido": 1,
              "frec_sem_exped": 3,
              "temp_anu_exped": 1,
              "hora_salida": "2025-01-07T11:50:00+01:00",
              "hora_llegada": "2025-01-07T12:55:00+01:00",
              "virtual": 0,
              "v_info": "undefined",
              "fecha_desde": "2018-02-26T00:00:00+01:00",
              "fecha_hasta": "2020-12-22T23:59:59+01:00",
              "Descripcion_Web": "Entrexardíns-Carballo E.A.",
              "revisado": true,
              "clonado": false,
              "nuevo": false,
              "asimilado_a": null,
              "gescar_id": "35782",
              "partir_circular": 0,
              "linea_id": 187,
              "estimacion_plazas_reservadas": null,
              "integrada": null
            }
          },
          {...}
          }
        ],
        "peso": 109,
        "is_geoloc": true,
        "is_xunta_geoloc": true,
        "wgs84_lat": "43248600",
        "wgs84_lon": "-8569150"
      }
    ],
    "peso": 114,
    "latitud": 43.249,
    "longitud": -8.5687
  }
}

```

## Precios

Llamando por HTTP GET a la siguiente URL se se obtienen los precios entre dos paradas, pendiente de investigar.

```http
GET https://arriva.gal/plataforma/api/buscador/precio/5274/4802.json

{

}
```

## Líneas

Llamando por HTTP GET a la siguiente URL se se obtienen todas las líneas.

```http
GET https://arriva.gal/plataforma/api/lineas/index.json

{
  "lineas": [
    {
      "id": 96,
      "conc_admin_l": 200,
      "lineas": 163,
      "nom_linea": "A Gallada - Maniños - Neda - Valdoviño (Servizo Praias)",
      "par_ori": 393,
      "par_des": 75,
      "Descripcion_Web_Ida": "A Gallada - Maniños - Neda - Valdoviño (Servizo Praias)",
      "Descripcion_Web_Vuelta": "A Gallada - Maniños - Neda - Valdoviño (Servizo Praias)",
      "fecha_desde": "1970-01-01T00:00:00+01:00",
      "fecha_hasta": "3000-12-12T23:59:59+01:00",
      "expediciones": [],
      "paradas_lineas": [
        {
          "parlin": 2382,
          "linea_par_lin": 96,
          "ordinal": 3,
          "parada_de_par_lin": 28,
          "mod_par": 1,
          "par_enl": 0,
          "gps_n_ida": 0,
          "gps_w_ida": 0,
          "gps_n_vuelta": 0,
          "gps_w_vuelta": 0,
          "kms_or": 82,
          "min_or": 10,
          "deshabilitada": false,
          "created": null,
          "modified": null,
          "revisado": false,
          "creado": false,
          "parada_asimilada_id": null,
          "linea_id": 96,
          "parada": {
            "parada": 28,
            "nom_parada": "Fene",
            "gps_n": 434750565,
            "gps_w": 81641656,
            "ayunta_fisico": 107,
            "destacar_parada_intermedia": true,
            "nom_web": "Avda Naturales",
            "paradaexpediciones_count": 31,
            "peso_mod": 0,
            "deshabilitada": false,
            "nuevo": false,
            "asimilado_a": null,
            "lat1": 43.2857,
            "lon1": -8.09738,
            "lat2": 43.2857,
            "lon2": -8.09738,
            "geoloc_desde": null,
            "geoloc_fecha": null,
            "lat": 43.2857,
            "lon": -8.09738,
            "gescar_id": "28",
            "id_simob": "15035-18",
            "ayunta_fisico_simob": 15035,
            "superparadas": [
              {
                "id": 5456,
                "nombre": "Avda Naturales",
                "lat": 43.2857,
                "lon": -8.09738,
                "gps_n": 0,
                "gps_w": 0,
                "ayuntamiento_id": 107,
                "deshabilitada": false,
                "manual": false,
                "paradaexpediciones_count": 74,
                "peso_mod": 0,
                "created": "2020-01-26T03:09:43+01:00",
                "modified": "2022-04-30T14:16:52+02:00",
                "_joinData": {
                  "id": 6037,
                  "parada_id": 28,
                  "superparada_id": 5456,
                  "created": null
                },
                "peso": 74,
                "latitud": 43.2857,
                "longitud": -8.09738
              }
            ],
            "peso": 31,
            "is_geoloc": true,
            "is_xunta_geoloc": true,
            "wgs84_lat": "43285700",
            "wgs84_lon": "-8097380"
          },
          "is_xunta_geoloc": false
        },
        {
          "parlin": 2384,
          "linea_par_lin": 96,
          "ordinal": 5,
          "parada_de_par_lin": 75,
          "mod_par": 1,
          "par_enl": 0,
          "gps_n_ida": 0,
          "gps_w_ida": 0,
          "gps_n_vuelta": 0,
          "gps_w_vuelta": 0,
          "kms_or": 239,
          "min_or": 35,
          "deshabilitada": false,
          "created": null,
          "modified": null,
          "revisado": false,
          "creado": false,
          "parada_asimilada_id": null,
          "linea_id": 96,
          "parada": {
            "parada": 75,
            "nom_parada": "Valdoviño",
            "gps_n": 4336472,
            "gps_w": 808555,
            "ayunta_fisico": 290,
            "destacar_parada_intermedia": false,
            "nom_web": "Valdoviño",
            "paradaexpediciones_count": 0,
            "peso_mod": 0,
            "deshabilitada": false,
            "nuevo": false,
            "asimilado_a": null,
            "lat1": null,
            "lon1": null,
            "lat2": null,
            "lon2": null,
            "geoloc_desde": null,
            "geoloc_fecha": null,
            "lat": 43.3647,
            "lon": -8.08555,
            "gescar_id": null,
            "id_simob": null,
            "ayunta_fisico_simob": null,
            "superparadas": [
              {
                "id": 6697,
                "nombre": "Valdoviño",
                "lat": 43.3647,
                "lon": -8.08555,
                "gps_n": 4336470,
                "gps_w": 808555,
                "ayuntamiento_id": 290,
                "deshabilitada": false,
                "manual": false,
                "paradaexpediciones_count": 0,
                "peso_mod": 0,
                "created": "2020-01-26T03:10:02+01:00",
                "modified": "2020-01-27T21:36:52+01:00",
                "_joinData": {
                  "id": 7408,
                  "parada_id": 75,
                  "superparada_id": 6697,
                  "created": null
                },
                "peso": 0,
                "latitud": 43.3647,
                "longitud": -8.08555
              }
            ],
            "peso": 0,
            "is_geoloc": true,
            "is_xunta_geoloc": true,
            "wgs84_lat": "43364700",
            "wgs84_lon": "-8085550"
          },
          "is_xunta_geoloc": false
        },
        {
          "parlin": 2381,
          "linea_par_lin": 96,
          "ordinal": 2,
          "parada_de_par_lin": 291,
          "mod_par": 1,
          "par_enl": 0,
          "gps_n_ida": 0,
          "gps_w_ida": 0,
          "gps_n_vuelta": 0,
          "gps_w_vuelta": 0,
          "kms_or": 25,
          "min_or": 5,
          "deshabilitada": false,
          "created": null,
          "modified": null,
          "revisado": false,
          "creado": false,
          "parada_asimilada_id": null,
          "linea_id": 96,
          "parada": {
            "parada": 291,
            "nom_parada": "Barallobre - Maniños",
            "gps_n": 4327728,
            "gps_w": 811425,
            "ayunta_fisico": 107,
            "destacar_parada_intermedia": false,
            "nom_web": "Barallobre - Maniños",
            "paradaexpediciones_count": 2,
            "peso_mod": 0,
            "deshabilitada": false,
            "nuevo": false,
            "asimilado_a": null,
            "lat1": null,
            "lon1": null,
            "lat2": null,
            "lon2": null,
            "geoloc_desde": null,
            "geoloc_fecha": null,
            "lat": 43.2773,
            "lon": -8.11425,
            "gescar_id": null,
            "id_simob": null,
            "ayunta_fisico_simob": null,
            "superparadas": [
              {
                "id": 4862,
                "nombre": "Barallobre - Maniños",
                "lat": 43.2773,
                "lon": -8.11425,
                "gps_n": 4327730,
                "gps_w": 811425,
                "ayuntamiento_id": 107,
                "deshabilitada": false,
                "manual": false,
                "paradaexpediciones_count": 2,
                "peso_mod": 0,
                "created": "2020-01-26T03:09:34+01:00",
                "modified": "2020-01-27T21:36:22+01:00",
                "_joinData": {
                  "id": 5381,
                  "parada_id": 291,
                  "superparada_id": 4862,
                  "created": null
                },
                "peso": 2,
                "latitud": 43.2773,
                "longitud": -8.11425
              }
            ],
            "peso": 2,
            "is_geoloc": true,
            "is_xunta_geoloc": true,
            "wgs84_lat": "43277300",
            "wgs84_lon": "-8114250"
          },
          "is_xunta_geoloc": false
        },
        {
          "parlin": 2380,
          "linea_par_lin": 96,
          "ordinal": 1,
          "parada_de_par_lin": 393,
          "mod_par": 1,
          "par_enl": 0,
          "gps_n_ida": 0,
          "gps_w_ida": 0,
          "gps_n_vuelta": 0,
          "gps_w_vuelta": 0,
          "kms_or": 0,
          "min_or": 0,
          "deshabilitada": false,
          "created": null,
          "modified": null,
          "revisado": false,
          "creado": false,
          "parada_asimilada_id": null,
          "linea_id": 96,
          "parada": {
            "parada": 393,
            "nom_parada": "A Gallada",
            "gps_n": 4344278,
            "gps_w": 820930,
            "ayunta_fisico": 169,
            "destacar_parada_intermedia": true,
            "nom_web": "A Gallada",
            "paradaexpediciones_count": 122,
            "peso_mod": 0,
            "deshabilitada": false,
            "nuevo": false,
            "asimilado_a": null,
            "lat1": null,
            "lon1": null,
            "lat2": null,
            "lon2": null,
            "geoloc_desde": null,
            "geoloc_fecha": null,
            "lat": 43.4428,
            "lon": -8.2093,
            "gescar_id": null,
            "id_simob": null,
            "ayunta_fisico_simob": null,
            "superparadas": [
              {
                "id": 4615,
                "nombre": "A Gallada",
                "lat": 43.4428,
                "lon": -8.2093,
                "gps_n": 4344280,
                "gps_w": 820930,
                "ayuntamiento_id": 169,
                "deshabilitada": false,
                "manual": false,
                "paradaexpediciones_count": 122,
                "peso_mod": 0,
                "created": "2020-01-26T03:09:31+01:00",
                "modified": "2020-01-27T21:36:18+01:00",
                "_joinData": {
                  "id": 5111,
                  "parada_id": 393,
                  "superparada_id": 4615,
                  "created": null
                },
                "peso": 122,
                "latitud": 43.4428,
                "longitud": -8.2093
              }
            ],
            "peso": 122,
            "is_geoloc": true,
            "is_xunta_geoloc": true,
            "wgs84_lat": "43442800",
            "wgs84_lon": "-8209300"
          },
          "is_xunta_geoloc": false
        },
        {
          "parlin": 2383,
          "linea_par_lin": 96,
          "ordinal": 4,
          "parada_de_par_lin": 414,
          "mod_par": 1,
          "par_enl": 0,
          "gps_n_ida": 0,
          "gps_w_ida": 0,
          "gps_n_vuelta": 0,
          "gps_w_vuelta": 0,
          "kms_or": 146,
          "min_or": 15,
          "deshabilitada": false,
          "created": null,
          "modified": null,
          "revisado": false,
          "creado": false,
          "parada_asimilada_id": null,
          "linea_id": 96,
          "parada": {
            "parada": 414,
            "nom_parada": "Neda (O Puntal)",
            "gps_n": 4329153,
            "gps_w": 809814,
            "ayunta_fisico": 176,
            "destacar_parada_intermedia": false,
            "nom_web": "O Puntal",
            "paradaexpediciones_count": 0,
            "peso_mod": 0,
            "deshabilitada": false,
            "nuevo": false,
            "asimilado_a": null,
            "lat1": null,
            "lon1": null,
            "lat2": null,
            "lon2": null,
            "geoloc_desde": null,
            "geoloc_fecha": null,
            "lat": 43.2915,
            "lon": -8.09814,
            "gescar_id": null,
            "id_simob": null,
            "ayunta_fisico_simob": null,
            "superparadas": [
              {
                "id": 5947,
                "nombre": "O Puntal",
                "lat": 43.2915,
                "lon": -8.09814,
                "gps_n": 4329150,
                "gps_w": 809814,
                "ayuntamiento_id": 176,
                "deshabilitada": false,
                "manual": false,
                "paradaexpediciones_count": 0,
                "peso_mod": 0,
                "created": "2020-01-26T03:09:51+01:00",
                "modified": "2020-01-27T21:36:40+01:00",
                "_joinData": {
                  "id": 6582,
                  "parada_id": 414,
                  "superparada_id": 5947,
                  "created": null
                },
                "peso": 0,
                "latitud": 43.2915,
                "longitud": -8.09814
              }
            ],
            "peso": 0,
            "is_geoloc": true,
            "is_xunta_geoloc": true,
            "wgs84_lat": "43291500",
            "wgs84_lon": "-8098140"
          },
          "is_xunta_geoloc": false
        }
      ]
    },
```

### Ver línea

Llamando por HTTP GET a la siguiente URL se se obtienen los detalles de una línea.

```http
GET https://arriva.gal/plataforma/api/lineas/view/493.json

{
  "linea": {
    "id": 493,
    "conc_admin_l": 848,
    "lineas": 10368,
    "nom_linea": "Coruña E.A.-Fisterra",
    "par_ori": 257,
    "par_des": 875,
    "Descripcion_Web_Ida": "CORUÑA E.A.-FISTERRA (DIRECTO HASTA CARBALLO)",
    "Descripcion_Web_Vuelta": "FISTERRA-CORUÑA E.A. (DIRECTO DESDE CARBALLO)",
    "fecha_desde": "2020-12-23T00:00:00+01:00",
    "fecha_hasta": "3000-12-12T23:59:59+01:00",
    "expediciones": [
      {
        "id": 3399,
        "expediciones": 113166,
        "linea_exped": 10368,
        "nom_exped": "Coruña E.A.-Fisterra",
        "nom_exped_abrev": "",
        "origen": 155363,
        "id_par_origen": 875,
        "ord_origen": 41,
        "destino": 155058,
        "id_par_destino": 257,
        "ord_destino": 1,
        "sentido": 2,
        "frec_sem_exped": 2,
        "temp_anu_exped": 1,
        "hora_salida": "2025-01-07T11:00:00+01:00",
        "hora_llegada": "2025-01-07T13:00:00+01:00",
        "virtual": 0,
        "v_info": "undefined",
        "fecha_desde": "2020-12-23T00:00:00+01:00",
        "fecha_hasta": "3000-12-12T23:59:59+01:00",
        "Descripcion_Web": "FISTERRA-CORUÑA E.A. (DIRECTO DESDE CARBALLO)",
        "revisado": true,
        "clonado": false,
        "nuevo": false,
        "asimilado_a": null,
        "gescar_id": "113166",
        "partir_circular": 0,
        "linea_id": 493,
        "estimacion_plazas_reservadas": 0,
        "integrada": false
      },
      {
        "id": 3400,
        "expediciones": 113219,
        "linea_exped": 10368,
        "nom_exped": "Coruña E.A.-Fisterra",
        "nom_exped_abrev": "",
        "origen": 155058,
        "id_par_origen": 257,
        "ord_origen": 1,
        "destino": 155363,
        "id_par_destino": 875,
        "ord_destino": 41,
        "sentido": 1,
        "frec_sem_exped": 2,
        "temp_anu_exped": 1,
        "hora_salida": "2025-01-07T08:15:00+01:00",
        "hora_llegada": "2025-01-07T10:15:00+01:00",
        "virtual": 0,
        "v_info": "undefined",
        "fecha_desde": "2020-12-23T00:00:00+01:00",
        "fecha_hasta": "3000-12-12T23:59:59+01:00",
        "Descripcion_Web": "CORUÑA E.A.-FISTERRA (DIRECTO HASTA CARBALLO)",
        "revisado": true,
        "clonado": false,
        "nuevo": false,
        "asimilado_a": null,
        "gescar_id": "113219",
        "partir_circular": 0,
        "linea_id": 493,
        "estimacion_plazas_reservadas": 0,
        "integrada": false
      },
      ],
    "paradas_lineas": [
      {
        "parlin": 155058,
        "linea_par_lin": 10368,
        "ordinal": 1,
        "parada_de_par_lin": 257,
        "mod_par": 1,
        "par_enl": 0,
        "gps_n_ida": 433535368,
        "gps_w_ida": 8404557,
        "gps_n_vuelta": 433537558,
        "gps_w_vuelta": 84035126,
        "kms_or": 0,
        "min_or": 0,
        "deshabilitada": false,
        "created": null,
        "modified": null,
        "revisado": true,
        "creado": false,
        "parada_asimilada_id": null,
        "linea_id": 493,
        "parada": {
          "parada": 257,
          "nom_parada": "Coruña E.A.",
          "gps_n": 433536198,
          "gps_w": 840384,
          "ayunta_fisico": 1,
          "destacar_parada_intermedia": false,
          "nom_web": "Estación de Coruña",
          "paradaexpediciones_count": 433,
          "peso_mod": 0,
          "deshabilitada": false,
          "nuevo": false,
          "asimilado_a": null,
          "lat1": 43.3531,
          "lon1": -8.4053,
          "lat2": 43.3531,
          "lon2": -8.4053,
          "geoloc_desde": null,
          "geoloc_fecha": null,
          "lat": 43.3531,
          "lon": -8.4053,
          "gescar_id": "257",
          "id_simob": "15030-1",
          "ayunta_fisico_simob": 15030,
          "superparadas": [
            {
              "id": 5274,
              "nombre": "Estación de Coruña",
              "lat": 43.3531,
              "lon": -8.4053,
              "gps_n": 0,
              "gps_w": 0,
              "ayuntamiento_id": 1,
              "deshabilitada": false,
              "manual": false,
              "paradaexpediciones_count": 516,
              "peso_mod": 0,
              "created": "2020-01-26T03:09:40+01:00",
              "modified": "2022-04-30T14:16:52+02:00",
              "_joinData": {
                "id": 5840,
                "parada_id": 257,
                "superparada_id": 5274,
                "created": null
              },
              "peso": 516,
              "latitud": 43.3531,
              "longitud": -8.4053
            }
          ],
          "peso": 433,
          "is_geoloc": true,
          "is_xunta_geoloc": true,
          "wgs84_lat": "43353100",
          "wgs84_lon": "-8405300"
        },
        "is_xunta_geoloc": true
      },
```
## Buses

Llamando por HTTP GET a la siguiente URL se se obtienen todos los buses.

```http
GET https://arriva.gal/plataforma/api/buses/getGeolocs.json

{
  "buses": [
    {
      "id": 141,
      "matricula": "919",
      "marca": null,
      "modelo": null,
      "descripcion": null,
      "created": "2021-12-20T15:12:15+01:00",
      "modified": "2024-08-22T18:15:33+02:00",
      "name": 141,
      "odometer": 2710914,
      "date": "2021-12-20T15:11:00+01:00",
      "plataforma": "webfleet",
      "ovelan_id": null,
      "webfleet_uid": "1-83646-6663E74501",
      "activo": false,
      "normativa_emisiones": null,
      "categoria_emisiones": null,
      "fecha_primera_matriculacion": null,
      "asientos": null,
      "plazas_totales": null,
      "posicion_ovelan": null,
      "posicion_webfleet": {
        "objectno": "141",
        "created": "2021-12-20T15:06:02+01:00",
        "modified": "2021-12-20T16:28:02+01:00",
        "objectname": "919",
        "objectclassname": "Vehículo",
        "objecttype": "van",
        "lastmsgid": "208570726210",
        "deleted": false,
        "msgtime": "2021-12-20T16:25:00+01:00",
        "longitude": "8°26'26,3\" W",
        "latitude": "43°19'38,3\" N",
        "postext": "Taller Pocomaco, Quinta Avenida del Polígono de Pocomaco, 21C, 15190 La Coruña, ES",
        "postext_short": "Taller Pocomaco, Quinta Avenida del Polígono de Pocomaco, 21C, 15190 La Coruña, ES",
        "speed": null,
        "course": null,
        "direction": null,
        "status": "A",
        "driver_currentworkstate": 0,
        "codriver_currentworkstate": 0,
        "odometer": 2710914,
        "ignition": false,
        "standstill": true,
        "pndconn": false,
        "ignition_time": "2021-12-20T16:20:00+01:00",
        "pos_time": "2021-12-20T16:25:00+01:00",
        "longitude_mdeg": -8440658,
        "latitude_mdeg": 43327321,
        "objectuid": "1-83646-6663E74501",
        "fuellevel": 220,
        "engine_operating_time": 21538440,
        "lat": 43.327321,
        "lon": -8.440658
      },
      "planning_actual": null,
      "posicion": {
        "lat": 43.327321,
        "lon": -8.440658,
        "long": -8.440658,
        "course": null,
        "direction": null,
        "direction_text": null,
        "speed": null
      },
      "last_stop": {
        "timestamp": null,
        "parada_id": null,
        "fecha": null
      },
      "estado": null
    },
```

### Ver posición de un bus

Llamando por HTTP GET a la siguiente URL se se obtiene la ubicación de un bus.

```http
GET https://arriva.gal/plataforma/api/buses/getGeoloc/849.json

{
  "id": 849,
  "matricula": "3203LBK",
  "marca": null,
  "modelo": "632 01",
  "descripcion": null,
  "created": "2021-12-20T15:12:15+01:00",
  "modified": "2024-08-22T18:15:33+02:00",
  "name": 849,
  "odometer": 7329743,
  "date": "2024-08-22T17:42:00+02:00",
  "plataforma": "webfleet",
  "ovelan_id": null,
  "webfleet_uid": "1-83646-880D81675A",
  "activo": true,
  "normativa_emisiones": "Euro V",
  "categoria_emisiones": "B",
  "fecha_primera_matriculacion": "2012-11-22T00:00:00+00:00",
  "asientos": 53,
  "plazas_totales": 55,
  "posicion_ovelan": null,
  "posicion_webfleet": {
    "objectno": "849",
    "created": "2021-12-03T06:26:03+01:00",
    "modified": "2025-01-07T00:39:01+01:00",
    "objectname": "3203LBK",
    "objectclassname": "Vehículo",
    "objecttype": "bus",
    "lastmsgid": "378014602681",
    "deleted": false,
    "msgtime": "2025-01-06T17:19:00+01:00",
    "longitude": "9°00'08,2\" W",
    "latitude": "42°52'33,3\" N",
    "postext": "AC-400, 15258 Mazaricos, ES",
    "postext_short": "AC-400, 15258 Mazaricos, ES",
    "speed": 79,
    "course": 226,
    "direction": 6,
    "status": "A",
    "driver_currentworkstate": 0,
    "codriver_currentworkstate": 0,
    "odometer": 7536010,
    "ignition": false,
    "standstill": true,
    "pndconn": false,
    "ignition_time": "2025-01-03T15:12:00+01:00",
    "pos_time": "2025-01-06T17:19:00+01:00",
    "longitude_mdeg": -9002281,
    "latitude_mdeg": 42875921,
    "objectuid": "1-83646-880D81675A",
    "fuellevel": null,
    "engine_operating_time": null,
    "lat": 42.875921,
    "lon": -9.002281
  },
  "planning_actual": null,
  "posicion": {
    "lat": 42.875921,
    "lon": -9.002281,
    "long": -9.002281,
    "course": 226,
    "direction": 6,
    "direction_text": "SW",
    "speed": 79
  },
  "last_stop": {
    "timestamp": null,
    "parada_id": null,
    "fecha": null
  },
  "estado": null
}
```

### Ver último área de un bus

Llamando por HTTP GET a la siguiente URL se se obtiene el último área de un bus.

```http
GET https://arriva.gal/plataforma/api/buses/getLastArea/849.json

{
  "bus": {
    "id": 849,
    "matricula": "3203LBK",
    "marca": null,
    "modelo": "632 01",
    "descripcion": null,
    "created": "2021-12-20T15:12:15+01:00",
    "modified": "2024-08-22T18:15:33+02:00",
    "name": 849,
    "odometer": 7329743,
    "date": "2024-08-22T17:42:00+02:00",
    "plataforma": "webfleet",
    "ovelan_id": null,
    "webfleet_uid": "1-83646-880D81675A",
    "activo": true,
    "normativa_emisiones": "Euro V",
    "categoria_emisiones": "B",
    "fecha_primera_matriculacion": "2012-11-22T00:00:00+00:00",
    "asientos": 53,
    "plazas_totales": 55,
    "planning_actual": null,
    "last_area": {
      "timestamp": null,
      "parada_id": null,
      "fecha": null
    },
    "posicion": {
      "lat": null,
      "lon": null,
      "long": null,
      "course": null,
      "direction": null,
      "direction_text": null
    },
    "last_stop": {
      "timestamp": null,
      "parada_id": null,
      "fecha": null
    },
    "estado": null
  }
}
```

### Ver última parada de un bus

Llamando por HTTP GET a la siguiente URL se se obtiene el última parada de un bus.

```http
GET https://arriva.gal/plataforma/api/buses/getLastStop/849.json

{
  "bus": {
    "id": 849,
    "matricula": "3203LBK",
    "marca": null,
    "modelo": "632 01",
    "descripcion": null,
    "created": "2021-12-20T15:12:15+01:00",
    "modified": "2024-08-22T18:15:33+02:00",
    "name": 849,
    "odometer": 7329743,
    "date": "2024-08-22T17:42:00+02:00",
    "plataforma": "webfleet",
    "ovelan_id": null,
    "webfleet_uid": "1-83646-880D81675A",
    "activo": true,
    "normativa_emisiones": "Euro V",
    "categoria_emisiones": "B",
    "fecha_primera_matriculacion": "2012-11-22T00:00:00+00:00",
    "asientos": 53,
    "plazas_totales": 55,
    "last_stop_ovelan": null,
    "last_stop_webfleet": {
      "objectno": "849",
      "created": "2021-12-03T17:33:03+01:00",
      "modified": "2024-05-14T12:00:23+02:00",
      "parada_id": 257,
      "objectuid": "1-83646-880D81675A",
      "objectname": "3203LBK",
      "start_time": "2024-05-14T11:39:00+02:00",
      "start_odometer": 7147676,
      "start_postext": "Coruña (Estación) *257*, ES",
      "end_time": "14/5/24, 11:40",
      "end_odometer": 7147676,
      "end_postext": "Coruña (Estación) *257*, ES",
      "reference": "puerta delantera",
      "distance": 0,
      "duration": 53
    },
    "planning_actual": null,
    "posicion": {
      "lat": null,
      "lon": null,
      "long": null,
      "course": null,
      "direction": null,
      "direction_text": null
    },
    "last_stop": {
      "timestamp": "14/5/24, 11:40",
      "parada_id": 257,
      "fecha": "14/5/24, 11:40"
    },
    "estado": null
  }
}
```

## Investigación

Aquí están todas las peticiones, pendiente de investigar.

```http
GET https://arriva.gal/plataforma/api/buses/getLastArea/849.json

{getParadas(e) {        return e || (e = {}), this.http.get(`${s.uw}/superparadas/index.json`, {params: e}).pipe((0, i.U)(e => e.paradas));
      }      getParadasDestinoPorOrigen(e, t) {
        return t || (t = {}), this.http.get(`${s.uw}/superparadas/por-origen/${e = undefined !== e ? e : 0}.json`, {params: t}).pipe((0, i.U)(e => e));      }
      getExpedicionesPorOrigenYDestino(e, t, a, n) {        let r = {};
        return "limited" == n && (r = {collection: s.du}), this.http.get(`${s.uw}/buscador/search/${e}/${t}/${a}.json`, {params: r}).pipe((0, i.U)(e => e));      }
      getPrice(e, t, a) {        return this.http.get(`${s.uw}/buscador/precio/${e}/${t}.json`, {params: a});
      }      getLines() {
        return this.http.get(`${s.uw}/lineas/index.json`, {params: {collection: s.du, associated: "Expediciones.ParadaExpediciones.Paradas;Expediciones.ParadaOrigen;Expediciones.ParadaDestino;Expediciones.FrecuenciasSemanales;Expediciones.TemporadasAnuales;Expediciones.GescarPlanningHoy"}});      }
      getLine(e, t) {        return t || (t = {associated: "ParadasLineas.Paradas;Expediciones.ParadaExpediciones.Paradas;Expediciones.FrecuenciasSemanales;Expediciones.GescarPlanningHoy"}), this.http.get(`${s.uw}/lineas/view/${e}.json`, {params: t});
      }      getExpedition(e, t) {
        return t || (t = {}), this.http.get(`${s.uw}/expediciones/view/${e}.json`, {params: t}).pipe((0, i.U)(e => e));      }
      getStops(e) {        return e || (e = {}), this.http.get(`${s.uw}/superparadas/index.json`, {params: e}).pipe((0, i.U)(e => e));
      }      getStop(e) {
        return this.http.get(`${s.uw}/superparadas/view/${e}.json`).pipe((0, i.U)(e => e));      }
      getExpeditionsByStopToday(e) {        return this.http.get(`${s.uw}/superparadas/expediciones-fecha/${e}.json`).pipe((0, i.U)(e => e));
      }      getBusLastStop(e) {
        return this.http.get(`${s.uw}/buses/getLastStop/${e}.json`);      }
      getBusLastArea(e, t) {        return t || (t = {}), this.http.get(`${s.uw}/buses/getLastArea/${e}.json`, {params: t});
      }      getBusesGeolocs() {
        return this.http.get(`${s.uw}/buses/getGeolocs.json`, {params: {collection: s.du}});      }
      getBusGeoloc(e) {        return this.http.get(`${s.uw}/buses/getGeoloc/${e}.json`);
      }      getComunicaciones() {
        return this.http.get(`${s.bW}/comunicaciones/index.json`);      }
      getComunicacion(e) {        return this.http.get(`${s.bW}/comunicaciones/view/${e}.json`);
      }    }
    return e.ɵfac = function (t) {      return new (t || e)(n.LFG(r.eN));
    }, e.ɵprov = n.Yz7({token: e, factory: e.ɵfac, providedIn: "root"}), e;  })();

}
```
