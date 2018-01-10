---
layout: post
title:  "Presentación sobre RIPE Atlas, en La Paz el 10/01/2018"
date:   2018-01-10 18:00:00 -0400
categories: ripe, charla, tutorial
---

Charla el 10/01/2018 19:00 en el auditorium del FNDR en La Paz.

## Proyecto RIPE Atlas

Instituciones:

- ICANN asigna las direcciones IP, los números autónomos a nivel mundial
- en Latinoamerica es LACNIC, en Europa es RIPE NCC
- RIPE Atlas es un proyecto de RIPE NCC
- Otro proyecto relacionado: [https://stat.ripe.net/](https://stat.ripe.net/)

Proyecto RIPE Atlas:

- Entrega de sondas en el mundo entero, sin costo
- Red de sondas para lanzar mediciones distribuidas: DNS, ping, traceroute, HTTP, NTP, certificados TLS
- Se busca la mejor repartición entre países y sistemas autónomos
- Más información: [https://atlas.ripe.net/about/](https://atlas.ripe.net/about/)

Situación en Bolivia:

- 43 sondas: [https://atlas.ripe.net/probes/?search=&status=&af=&country=BO#!tab-public](https://atlas.ripe.net/probes/?search=&status=&af=&country=BO#!tab-public)
- 24 sondas conectadas: [https://atlas.ripe.net/probes/?search=&status=1&af=&country=BO#!tab-public](https://atlas.ripe.net/probes/?search=&status=1&af=&country=BO#!tab-public)
- aproximadamente 35 sondas nuevas listas para distribuir

De las 24 sondas conectadas:

- 10 con Entel - [AS 6568](https://stat.ripe.net/6568)
- 6 con AXS - [AS 26210](https://stat.ripe.net/26210)
- 6 con Tigo - [AS 27882](https://stat.ripe.net/27882), 2 de Viva - [AS 28024](https://stat.ripe.net/28024)

Las 24 sondas conectadas se encuentran en las [siguientes ciudades](https://atlas.ripe.net/results/maps/network-coverage/?filter=Bolivia+(bo)):

- 16 en La Paz
- 3 en Cochabamba
- 1 en Oruro
- 1 en Sucre
- 1 en Tarija

En la región, la [cobertura](https://atlas.ripe.net/results/maps/density/) es la siguiente:

- 64 en Brazil
- 40 en Argentina
- 28 en Bolivia
- 27 en Chile
- 17 en Uruguay
- 12 en Ecuador
- ...
- 1.401 en Alemania

## Participar

Si tengo una sonda, que tengo que hacer:

- Crear mi cuenta en [https://atlas.ripe.net/](https://atlas.ripe.net/)
- Encender y conectar al modem por ethernet
- No tocar - es crucial que la sonda esté conectada de manera permanente
- Registrar mi sonda en [https://atlas.ripe.net/](https://atlas.ripe.net/)
- Cobrar automáticamente mis créditos

Si tengo créditos, qué puedo hacer:

- Lanzar mediciones: a través de la interfaz web [https://atlas.ripe.net/measurements/](https://atlas.ripe.net/measurements/), de la API [https://atlas.ripe.net/docs/api/v2/reference/](https://atlas.ripe.net/docs/api/v2/reference/), o mediante comandos [https://github.com/RIPE-Atlas-Community/ripe-atlas-community-contrib/](https://github.com/RIPE-Atlas-Community/ripe-atlas-community-contrib/)
- Transferir créditos a tus amigos - [https://atlas.ripe.net/docs/credits/](https://atlas.ripe.net/docs/credits/)

Si no tengo sonda, qué puedo hacer:

- Solicitar directamente a RIPE NCC: [https://atlas.ripe.net/apply/](https://atlas.ripe.net/apply/)
- Solicitar a la comunidad boliviana: [https://atlas.tecnologia.bo/involucrarse/](https://atlas.tecnologia.bo/involucrarse/)

Si no tengo créditos, qué puedo hacer:

- Albergar una sonda
- Solicitar a la comunidad boliviana: [https://atlas.tecnologia.bo/involucrarse/](https://atlas.tecnologia.bo/involucrarse/)

## Qué podemos hacer en Bolivia

Proyectos existentes:

- ["Mapa" de la Internet boliviana](http://sg-pub.ripe.net/emile/ixp-country-jedi/latest/BO/), por [@meileaben](https://twitter.com/meileaben)
- [Supervisión y "uptime" de las sondas en Bolivia](https://notibol.com/monitor/), por [@Gourami](http://twitter.com/Gourami/)
- [Mapa de las sondas](https://geo.gob.bo/mapfishapp/map/504bf4e2068b8d2442381d6c8e4fba5d), por [@geoboliviaide](http://twitter.com/geoboliviaide/) y [@rafemoro](http://twitter.com/rafemoro/)

Podríamos hacer:

- Mapa de la internet boliviana: realizar un mapa de la internet boliviana, con los nombres de los operadores, todos los sistemas autónomos, sus relaciones, su ubicación geográfica, los puntos de intercambio. Se puede usar datos de las sondas, pero también de LACNIC, de peeringDB.
- Calidad de los proveedores de acceso a internet en Bolivia: establecer indicadores de calidad de los servicios ofrecidos por los diferentes proveedores de acceso a internet en Bolivia, como ser: cortes, latencia hacia diferentes sitios muy usados, configuración de DNS, provisión de IPv6.
- Uso del Punto de Intercambio de Tráfico: producir indicadores que permitan comprobar la información publicada en el sitio del Punto de Intercambio de Tráfico.
- Análisis puntual de los cortes para buscar causas y documentarlos, eventualmente con lanzamiento automático de pruebas si se detecta un potencial problema

Quién:

- Aficionados/as
- Estudiantes
- Investigadores
- Docentes

## Cómo lanzo mediciones

Se pueden lanzar y ver todas las pruebas desde [https://atlas.ripe.net/measurements/](https://atlas.ripe.net/measurements/).

Para hacer mediante herramientas de consola:

```
cd ~
mkdir dev
cd dev
git clone git@github.com:RIPE-Atlas-Community/ripe-atlas-community-contrib.git
sudo apt install python-pip dnsutils
sudo pip install cymruwhois
```

Crear una clave de la API en [https://atlas.ripe.net/keys/](https://atlas.ripe.net/keys/) y pegarla en:

```
mkdir ~/.atlas
nano ~/.atlas/auth
```

```
3063b764-a827-4ae9-a64c-a47fc109d596
```

Lanzaremos un traceroute desde 5 sondas de Bolivia hacia el servidor que aloja atlas.tecnologia.bo.

- recuperamos la IP

```
dig +short atlas.tecnologia.bo A
```

- lanzamos el comando (ojo: se requiere que la clave de la API esté instalada):

```
python ~/dev/ripe-atlas-community-contrib/traceroute.py -v -r 5 -c BO 212.83.181.142
```

- vemos la medición en [https://atlas.ripe.net/measurements/10845265/](https://atlas.ripe.net/measurements/10845265/)
- descargamos la medición en un archivo JSON:

```
cd
mkdir atlas
cd atlas
curl https://atlas.ripe.net/api/v2/measurements/10845265/results/?format=jsonpython > ~/atlas/10845265.json
```

- mostramos el resultado en un formato un poco más lindo:

```
~/dev/ripe-atlas-community-contrib/json2traceroute.py ~/atlas/10845265.json
```

Haremos el trabajo al revés: desde el sistema autónomo donde se aloja atlas.tecnologia.bo, hacer un traceroute hacia mi conexión:

- mi IP: [https://stat.ripe.net/widget/whats-my-ip](https://stat.ripe.net/widget/whats-my-ip)
- lanzar traceroute desde 3 sondas diferentes en el sistema autónomo 12876 hacia mi IP 181.115.130.8

```
python /home/slesage/dev/ripe-atlas-community-contrib/traceroute.py -v -r 3 -n 12876 181.115.130.8
```

- ver las mediciones: [https://atlas.ripe.net/measurements/](https://atlas.ripe.net/measurements/)
- descargar las mediciones

```
curl https://atlas.ripe.net/api/v2/measurements/10845278/results/?format=json > ~/atlas/10845278.json
```

- mostrar en un formato lindo:

```
~/dev/ripe-atlas-community-contrib/json2traceroute.py ~/atlas/10845278.json
```

Tutoriales:

- [http://www.bortzmeyer.org/ripe-atlas-api.html](http://www.bortzmeyer.org/ripe-atlas-api.html)
- [http://www.bortzmeyer.org/traceroute-atlas.html](http://www.bortzmeyer.org/traceroute-atlas.html)
- [http://www.bortzmeyer.org/jq.html](http://www.bortzmeyer.org/jq.html)
- [https://github.com/RIPE-Atlas-Community/ripe-atlas-community-contrib](https://github.com/RIPE-Atlas-Community/ripe-atlas-community-contrib)
- [https://atlas.ripe.net/measurements-and-tools/tools/](https://atlas.ripe.net/measurements-and-tools/tools/)

## Referencias

- Portal general: [https://atlas.ripe.net/](https://atlas.ripe.net/)
- Documentaciones: [https://atlas.ripe.net/docs/](https://atlas.ripe.net/docs/)
- Preguntas frecuentes: [https://atlas.ripe.net/about/faq/](https://atlas.ripe.net/about/faq/)
- API REST: [https://atlas.ripe.net/docs/api/v2/reference/](https://atlas.ripe.net/docs/api/v2/reference/)
- Cómo usaron las sondas en otros países: [https://labs.ripe.net/atlas](https://labs.ripe.net/atlas)
- La comunidad boliviana: [https://atlas.tecnologia.bo/about/](https://atlas.tecnologia.bo/about/)

Sigan [@RIPE_Atlas_BO](https://atlas.tecnologia.bo/https://twitter.com/RIPE_Atlas_BO) en Twitter, y participen del sitio web [atlas.tecnologia.bo](https://atlas.tecnologia.bo/)

Algunas cuentas Twitter a seguir:

- [@RIPE_Atlas_BO](https://atlas.tecnologia.bo/https://twitter.com/RIPE_Atlas_BO)
- [@meileaben](https://twitter.com/meileaben)
- [@Gourami](http://twitter.com/Gourami/)
- [https://twitter.com/huguei](https://twitter.com/huguei)
- [@PeeringDB](https://twitter.com/PeeringDB)
- [@adslbolivia](https://twitter.com/adslbolivia)
- [@ItsEnmaskarado](https://twitter.com/ItsEnmaskarado)
- [@RIPE_Atlas](https://twitter.com/RIPE_Atlas)
- [@TrainingRIPENCC](https://twitter.com/TrainingRIPENCC)
- [@mir_ripe_labs](https://twitter.com/mir_ripe_labs)
- [@LuixSP](https://twitter.com/LuixSP)
- [@geoboliviaide](http://twitter.com/geoboliviaide/)
- [@rafemoro](http://twitter.com/rafemoro/)
- [@drkpkg](https://twitter.com/drkpkg)
