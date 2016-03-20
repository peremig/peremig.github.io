--- 
published: true
title: Resetejar webserver d'Airzone
layout: post
author: Pere MiG 
category: howto #articles 
tags: 
- airzone
- domòtica
- webserver

---
<div style="text-align:center" markdown="1">

![Airzone Flexa 3.0](images/airzone.jpg)

</div>
<div style="text-align:justify" markdown="1">

[Airzone](http://www.airzone.es/){:target="_blank"} és un sistema de climatització per zones que permet oferir diferents temperatures de confort a diferents espais d'un mateix habitacle o empresa. A banda de les opcions programables que tenen tots aquests sistemes, el que el fa interessant és l'opció de control a través d'Internet mitjançant la configuració d'un mòdul webserver.

En la configuració d'un sistema [Flexa 3.0](http://www.airzone.es/en/pro/range-of-systems/flexa-3-0/){:target="_blank"} m'han aparegut diversos contratemps que cal anotar, ja que la solució si bé simple, no és accessible fàcilment. D'altra banda, potser per la novetat del sistema, [**Google**](https://encrypted.google.com/){:target="_blank"} no m'ha ajudat gens a trobat-ne les solucions.

<!-- more -->

Existeixen dos tipus de webserver: cablejat amb RJ45 (cosa que demana fer arribar un cable d'aquest tipus des del nostre router domèstic fins al mòdul de control d'Airzone, normalment situat sobre el sostre fals del lavabo) o bé amb wifi (més còmode, però hem de tenir en compte que la placa utilitza wifi 802.11b -es veu que encara hi ha qui en fabrica tot i la seva obsolescència- i que si el sostre fals que amaga el mòdul de control és d'alumini ens pot causar interferències que redueixen la intensitat del senyal).

La configuració del webserver consta de dues parts, en la primera es vincula el webserver al router domèstic (és a dir, li indiquem l'ESSID i la contrasenya associada i, si cal, una IP fixa). En la segona part, després de crear-nos un compte a [Airzone Cloud](https://www.airzonecloud.com/#/init/login){:target="_blank"}, ens hi vinculem el webserver, de manera que podrem actuar sobre la climatització via aplicació de mòbil (tant per a mòbils [Apple](https://itunes.apple.com/es/app/airzone-cloud/id968067256){:target="_blank"} com [Android](https://play.google.com/store/apps/details?id=es.altra.airzone){:target="_blank"}) o via [pàgina web](https://www.airzonecloud.com/#/home/servers){:target="_blank"}. Ambdues configuracions estan ben explicades en el fulletó que acompanya el mòdul webserver.

La configuració que vaig fer era wifi i amb el mòdul de control amagat darrere d'un sostre fals d'alumini. Per millorar la qualitat del senyal, es va optar per un allargador USB i portar l'antena fora del lavabo, amagant-la sobre el sostre fals de pladur que oculta els conductes de climatització. Tot i amb això, va sorgir un problema: no hi havia manera de vincular el webserver amb l'aplicació d'*Airzone Cloud*; després de diversos intents infructuosos, vam trucar a la [seu central d'Airzone a Màlaga](http://www.airzone.es/contacto/){:target="_blank"} i ens en va donar el motiu: no els constava com a venut el mòdul i, per tant, no estava donat d'alta al *Cloud*, cosa que van fer i es va poder solucionar aquest primer aspecte. Va ser en aquesta trucada que ens van dir que, tot i així el senyal era dèbil i que convindria allunyar l'antena (un dongle USB) del sostre d'alumini.

Posteriorment, vam provar de canviar les opcions configurables del webserver (ESSID, contrasenya i IP). No es pot fer altra cosa que un reset del webserver, és impossible canviar-ne algun dels paràmetres per separat. Per fer-ho, hem de prémer tres cops (amb pulsació llarga) sobre el logotip *Airzone* del *Flexa* màster. Accedirem així al menú de `Configuració avançada`, allí trobem dues opcions, `Informació` i `Zones`, hem de triar-ne *Informació*. Aquesta opció consta de dues pantalles, en la segona d'elles, la darrera opció és `Webserver`, si la triem podrem llegir la seva configuració actual i arribarem, finalment, a l'opció `Reset`, amb què podrem deixar el mòdul tal i com venia de fàbrica per tornar-lo a configurar amb les noves opcions.

Ignoro per què *Airzone* no facilita l'accés a aquesta informació: l'ús del wifi 802.11b en la placa apareix en un dels catàlegs professionals consultats (però no està a l'abast del públic general), de manera que si l'instal·lador no se n'ha adonat o no ho diu, l'usuari no coneix aquesta dada (i potser hauria estat millor muntar com a mínim un 802.11g). La modificació dels paràmetres de configuració no és possible, cal fer un reset total i tornar a configurar (d'altra banda les opcions obertes són ben poques i, com va confirmar la trucada a Màlaga, el webserver informa de moltes variables que no són accessibles a l'usuari, com pot ser la potència del senyal wifi que arriba del router a la placa). Finalment, la manera de fer aquest reset s'ha ocultat excessivament, no s'hi arriba de forma intuïtiva i és la darrera del menú destinat al servei tècnic; fa la impressió que es consideri fer un *Reset* com una avaria per a la qual calgui personal especialitzat, amb el seu cost de desplaçament i mà d'obra.

</div>