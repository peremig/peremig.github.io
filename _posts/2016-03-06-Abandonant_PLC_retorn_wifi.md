--- 
published: true
title: Abandonant els PLC, retorn al wifi
layout: post
author: Pere MiG 
category: articles #howto
tags: 
- xarxa
- PLC


---
<div style="text-align:center" markdown="1">

![PLC](/images/plc.jpg)

</div>
<div style="text-align:justify" markdown="1">

Fa uns anys, quan van instal·lar-me la connexió de fibra òptica a casa (en aquells moments [Movistar](http://www.movistar.es/ca/particulars/internet/adsl-fibra-optica/fibra-optica/){:target="_blank"} oferia 50 Mb de pujada i 5 Mb de baixada), vaig tenir la desagradable sorpresa que els operaris podien fer-me-la arribar al punt més allunyat del lloc on tinc l'ordinador de sobretaula. Un lloc on el senyal wifi arribava força dèbil (a més, el wifi -N- tenia un sostre proper a la velocitat contractada). Vaig decidir, llavors, emprar PLC i vaig adquirir (amb vistes al futur) uns PLC que oferien connexió a 500 Mb. I aquí va començar una història de desencontres entre el router (connectat a un PLC) i l'ordinador (connectat a un altre PLC), que es passaven dies sencers sense veure's ni parlar-se.

<!-- more -->

Ja des d'un primer moment, vaig poder observar que el rendiment dels PLC no arribava al que havia contractat (sí que hi arribava, però, una connexió d'un portàtil directa al router). També vaig patir de tant en tant pèrdues de senyal: els PLC s'ignoraven entre ells i no hi havia manera de comunicar l'ordinador amb el router (ni tan sols amb un miserable ping).

Com que hi havia webs on es deia que hi influïen les interferències de la xarxa elèctrica, l'electricista del barri va venir i va modificar la línia del pis de manera que els fils que anaven als dos endolls on eren connectats els PLC morissin en el mateix interruptor del quadre de llums. Però, tot i donant-se les mans, hi havia una progressiva caiguda de rendiment en la comunicació entre ells fins al dia que s'ignoraven totalment. Aquell dia tocava resetejar-ho tot (és a dir, apagar-ho tot), esperar uns 10 minuts que tots els seus indicadors leds deixessin d'estar actius i, després, reiniciar-ho tot: router i pc.

Des d'aleshores, la companyia ha ampliat dues vegades els amples de banda i actualment ofereix 300 Mb pujada i 30 Mb de baixada (si bé sembla ser que en el darrer Mobile Word Congress han anunciat que estan estudiant oferir els 300 Mb simètrics). Amb aquestes ampliacions, els problemes de desconnexió es van veure agreujats i les caigudes més freqüents. El més curiós, però, va ser que els tests de velocitat no mostraven massa millora; és van clavar al voltant d'uns 30 Mb de baixada i 30 Mb de pujada, tot i que la velocitat de pujada fos de 300 Mb. Una connexió directa a router, però, donava els resultats esperats.

La veritat és que em va pujar la mosca al nas. Vaig sospitar que es devia produir una col·lisió de dades en algun punt (un coll d'ampolla). Els cables eren tots categoria 5e, per aquest costat correcte. La sortida del router és Gigalan, així com la tarja de l'ordinador; també correcte. Primera sorpresa: les rosetes RJ45 del PLC eren tipus Fastlan, és a dir, limitades a 100 Mb/s. Llavors, quin sentit té oferir PLC de més de 100 Mb/s (500 Mb/s, en aquest cas) si després no podrà suportar velocitats més altes? Vaig descobrir que només els PLC de 1200 Mb/s munten rosetes RJ45 de tipus Gigalan (però avui dia ja hi ha alguna companyia, com [Adamo](https://www.adamo.es/ca/){:target="_blank"}, que ofereix 1Gb de connexió a internet).

Vaig pensar a comprar nous PLC, però de marca diferent. Segona sorpresa: a can Google, els usuaris recomanaven la marca Devolo, la que ja estava emprant i que m'ha generat tots els inconvenients descrits abans ja des del primer dia de tenir-los.

Googlejant una mica, vaig poder llegir [històries semblants a aquesta](http://www.adslzone.net/postt98307.html){:target="_blank"}. Va ser en aquell moment que vaig decidir abandonar els PLC i tornar a una solució wifi semblant a la que tenia en temps de l'ADSL (llavors vaig poder connectar el router més a la vora de l'ordinador (cablejar hauria estat millor, però la Gigalan està a punt de ser superada per l'oferta de velocitat de la fibra òptica i no em veig fent obres per amagar tubs corrugats plens de cables de xarxa). 

La solució ha consistit en connectar el pc a un punt d'accés en mode bridge. I aquí ha estat la darrera sorpresa: quan, fa més de 10 anys, vaig connectar el router ADSL a un punt d'accés (que vaig modificar a mode bridge), no hi havia documentació a la xarxa que facilités una feina que em va ocupar un parell d'hores; avui dia, els fabricants ja ho tenen en compte (almenys [Asus](http://www.asus.com/us/Networking/Wireless-AP-Repeater-Bridges-Products/){:target="_blank"}) i ha estat feina de pocs minuts tenir-ho tot en marxa i funcionant.

</div>