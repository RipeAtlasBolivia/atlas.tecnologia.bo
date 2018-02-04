---
layout: page
title: Proyectos
permalink: /proyectos/
---

Los siguientes proyectos hacen uso de las sondas RIPE Atlas ubicadas en Bolivia

## [Monitor Notibol](https://notibol.com/monitor/): Monitor de sondas en Bolivia

![Monitor de sondas]({{ "/assets/monitor-notibol.png" | absolute_url }})

## [IXP Country Jedi](http://sg-pub.ripe.net/emile/ixp-country-jedi/latest/BO/): cartografía de los sistemas autónomos en Bolivia

![Gráfo de sistemas autónomos en Bolivia]({{ "/assets/ixp-country-jedi-bo-as-graph.png" | absolute_url }})

## Número de sondas por número autónomo en Bolivia

<ul>
{% for asn in site.data.sondas_asn %}
<li><a href="https://atlas.ripe.net/probes/?search={{asn.asn}}&status=&af=&country=BO#!tab-public">{{asn.sondas}} sondas</a> - {{asn.nombre}} (<a href="https://stat.ripe.net/{{asn.asn}}">{{asn.asn}}</a>)</li>
{% endfor %}
</ul>

Ver el [código](https://github.com/severo/sondas-por-as).
