---
published: true
title: Automuntar unitats USB amb accés a escriptura
layout: post
author: Pere MiG 
category: howto
tags:
- Debian
- Jessie
- usb
---

<div style="text-align:center" markdown="1">

![usb](https://images.duckduckgo.com/iu/?u=http%3A%2F%2Fdebianhelp.files.wordpress.com%2F2011%2F11%2Fusb-300.gif&f=1)

</div>
<div style="text-align:justify" markdown="1">

Després d’instal·lar *Debian 8 (Jessie)* a l’*Acer Aspire V5-121*, m’he trobat que l’accés a llapis de memòria USB amb format FAT era només d’escriptura per a l’usuari habitual. Si hi volia escriure, calia fer-ho com a *root*. D’altra banda, el llapis es muntava a `/media/usb*` en comptes de a `/media/usuari`.

<!-- more -->

He comprovat que no tenia en el meu sistema els paquets *usbmount* ni *pmount*, la presència dels quals provocava [el mateix error en un altre usuari de Debian](http://forums.debian.net/viewtopic.php?f=7&t=109604&sid=fbef38fc21231d0ff2b4f8fc0a956f7d){:target="_blank"}, error que solucionà eliminant-los del sistema segons que explica en un post del 10 de desembre de 2013.

No es tractava tampoc de llapis de memòria defectuosos, donat que funcionaven perfectament al PC de sobretaula (amb Debian Wheezy). Ni tampoc tenia pinta de ser un bug de Jessie, versió prou madura actualment ([la RC1 va ser anunciada el 26 de gener de 2015 i s’espera la versió estable durant aquest mes de febrer](https://lists.debian.org/debian-devel-announce/2015/01/msg00005.html){:target="_blank"}).

Fent memòria vaig recordar que vaig instal·lar Jessie des de llapis de memòria USB, cosa que m’havia deixat la següent línia a *fstab*:

{% highlight bash %}
/dev/sdb1       /media/usb1        auto       rw,user,noauto      0 0
{% endhighlight %}

En principi, i donades les regles udev, no cal aquesta entrada en aquest fitxer. La solució, doncs, ha estat tan simple com comentar-la (també pot eliminar-se, però així em serveix de recordatori per si torna a passar en una altra instal·lació):

{% highlight bash %}
# /dev/sdb1       /media/usb1        auto       rw,user,noauto      0 0
{% endhighlight %}

A partir d’aquest moment, el llapis ja s’ha muntat a `/media/usuari` en comptes de a `/media/usb*` i ja hi ha hagut accés de lectura i escriptura als llapis de memòria per a l’usuari habitual.

</div>