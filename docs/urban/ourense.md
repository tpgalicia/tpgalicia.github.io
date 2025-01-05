# Urbano de Ourense

El transporte urbano de Ourense consiste en un servicio de autobuses urbanos prestado por [Avanza](https://ourense.avanzagrupo.com/), en régimen de concesión por parte del Concello de Ourense, en precario desde 2015.

## Datos estáticos

Los datos de las líneas de autobuses urbanos de Vigo se pueden obtener en formato GTFS desde su propia web o desde el [NAP](../other/nap.md) del Ministerio de Transportes y Movilidad Sostenible. La URL del dataset es <https://ourense.avanzagrupo.com/gt/gtfs-urbano-ourense.zip>, sin necesidad de autenticación, en el caso del de su web o  <https://nap.transportes.gob.es/Files/Detail/1387>, en el caso del ofrecido en el NAP.

!!! note "Nota"

	Los datos de GTFS de Avanza Ourense no parecen actualizarse con regularidad, presentando información errónea con líneas antiguas y horarios que no aplican en los días correspondientes (nocturnos y servicios especiales).

## Datos en tiempo real

No existe un feed público en un formato estándar (como lo son GTFS-RealTime o SIRI) para acceder a las estimaciones de llegada de los autobuses urbanos en tiempo real. Por tanto, no hay forma de obtener las estimaciones de llegadas a las paradas, ni alertas de servicio ni posiciones de los vehículos.

La única forma de acceder a estos datos (de manera individualizada) es aprovechando distintas API del Concello de Vigo, extraídas de los QRs de las paradas


## _Scraping_

De manera alternativa, se pueden obtener los datos de avisos y tiempo real mediante Web Scraping, muy similar a la API de Vitrasa.

### Avisos

La URL es `https://ourense.avanzagrupo.com/avisos` y el HTML de los avisos se puede obtener, por ejemplo, con el siguiente JavaScript:

```js
document
	.querySelectorAll("#v-pills-tabContent .tab-pane")
	.values()
	.map(p => p.innerHTML)
```

### Estimaciones de una parada

La URL es `https://consultasqrou.avanzagrupo.com/default.aspx/?parada=45` , cambiando "parada" por el ID de la parada a consultar. Para sacar las estimaciones, se puede usar, por ejemplo, este JavaScript:

```js
document.querySelectorAll("#GridView1 > tbody > tr")
	.values()
	.map(tr => tr.querySelectorAll("td"))
	.filter(l => l.length === 3)
```

Es importante filtrar los `td` donde solo hay tres elementos, porque la "UI" utiliza tablas para todo el diseño, incluyendo la paginación en la parte inferior. Esos tres elementos corresponden, en este orden a "linea", "ruta", "minutos". 

!!! note "Nota"

	Usar la paginación es posible, pero complicado, ya que hay que procesar la primera página, y sacar variables como ViewState, y hacer un POST para obtenerla. Por ello, es mucho más sencillo y eficiente usar la API descrita anteriormente.
    La web lleva meses caída.
