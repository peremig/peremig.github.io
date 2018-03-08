--- 
published: true
title: Activar les capacitats dels xips de xarxa en HP 250 G5
layout: post
author: Pere MiG 
category: articles #howto 
tags: 
- Debian
- wifi
- Intel

---
<div style="text-align:center" markdown="1">

![Ethernet + Wifi](http://parentesis.com/imagesPosts/WiFi-Ethernet.jpg)

</div>
<div style="text-align:justify" markdown="1">

La instal·lació de Debian Stretch en un portàtil HP 250 G5 demana tenir preparar en un mitjà extraïble els firmware per al xip de xarxa ethernet Realtek i per al xip de wifi Intel. No tenir-los preparats farà que la navegació per xarxa ethernet no aprofiti les capacitats de navegació a 1 Gb/s i ens limitem a 100 Mb/s; mentre que en el cas del wifi, no el tindrem operatiu fins que no n'instal·lem el firmware

<!-- more -->
### Activació de les capacitats Ethernet del xip Realtek 8168h

Podem tenir preparar en un mitjà extraïble els firmware per als xips wifi Intel proporcionats en el paquet **firmware-realtek**, donat que es consideren *non-free*, o bé incorporar-los un cop acabada la instal·lació (activant-ne primer el repositori a `/etc/apt/sources.list`). Sense aquest paquet el xip no serà capaç de discriminar si el tipus de connexió és GigaLan i ens comunicarem dins la xarxa a 100 Mb/s, en el millor dels casos.

### Activació del xip wifi Intel 7265D

Podem tenir preparar en un mitjà extraïble els firmware per als xips wifi Intel proporcionats en el paquet **firmware-iwlwifi**, donat que es consideren *non-free*, o bé incorporar-los un cop acabada la instal·lació (activant-ne primer el repositori a `/etc/apt/sources.list`, si no ho hem fet abans)..

Un cop fet això, en la primera arrencada (o en una consulta a **dmesg**) trobarem els següents missatges:

{% highlight bash %}

[    2.005420] iwlwifi 0000:02:00.0: firmware: failed to load iwlwifi-7265D-26.ucode (-2)
[    2.005422] iwlwifi 0000:02:00.0: Direct firmware load for iwlwifi-7265D-26.ucode failed with error -2
[    2.005436] iwlwifi 0000:02:00.0: firmware: failed to load iwlwifi-7265D-25.ucode (-2)
[    2.005437] iwlwifi 0000:02:00.0: Direct firmware load for iwlwifi-7265D-25.ucode failed with error -2
[    2.005446] iwlwifi 0000:02:00.0: firmware: failed to load iwlwifi-7265D-24.ucode (-2)
[    2.005448] iwlwifi 0000:02:00.0: Direct firmware load for iwlwifi-7265D-24.ucode failed with error -2
[    2.005456] iwlwifi 0000:02:00.0: firmware: failed to load iwlwifi-7265D-23.ucode (-2)
[    2.005458] iwlwifi 0000:02:00.0: Direct firmware load for iwlwifi-7265D-23.ucode failed with error -2
[    2.015257] iwlwifi 0000:02:00.0: firmware: direct-loading firmware iwlwifi-7265D-22.ucode
[    2.015557] iwlwifi 0000:02:00.0: loaded firmware version 22.361476.0 op_mode iwlmvm
[    2.054163] iwlwifi 0000:02:00.0: Detected Intel(R) Dual Band Wireless AC 3165, REV=0x210

{% endhighlight %}

Es tracta d'un [bug del kernel documentat a Debian](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=857198#15), que es manifesta en la cerca de les versions del driver de les 27 en avall. Els missatges d'error venen donats perquè [les versions salten de la 22 a la 27](https://wireless.wiki.kernel.org/en/users/drivers/iwlwifi/core_release), amb la qual cosa les versions 23 a 26 no existeixen. Això, tot i que pot resultar un pèl lleig, no afecta el funcionament del xip, ja que s'instal·la la millor versió possible (-22.ucode).

</div>
