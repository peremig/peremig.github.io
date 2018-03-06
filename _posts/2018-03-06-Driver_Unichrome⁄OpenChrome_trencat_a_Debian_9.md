--- 
published: true
title: Driver per a xips de vídeo VIA UniChrome trencat a Debian 9 Stretch
layout: post
author: Pere MiG 
category: articles #howto
tags: 
- Debian
- vídeo
- Stretch

---
<div style="text-align:center" markdown="1">

![OpenChrome](https://www.freedesktop.org/wiki/Openchrome/openchrome.gif)

</div>
<div style="text-align:justify" markdown="1">

De tant en tant em dedico a restaurar velles màquines i fer que puguin ser operatives amb sistemes més lleugers. Avui li ha tocat el torn a un vell portàtil amb xip de vídeo **VIA UniChrome**. El sistema a instal·lar triat ha estat Debian 9 (Stretch) amb entorn gràfic  LXDE.

En acabar la instal·lació la presentació horrible dels caràcters en pantalla ha indicat clarament que faltava instal·lar els drivers gràfics.

<!-- more -->

Una consulta a `/var/log/Xorg.0.log` ha estat suficient per corroborar que faltava el driver openchrome:

{% highlight bash %}

user@domain:/var/log$ cat Xorg.0.log | grep '(EE)'
        (WW) warning, (EE) error, (NI) not implemented, (??) unknown.
[    18.964] (EE) Failed to load module "openchrome" (module does not exist, 0)

{% endhighlight %}

En no haver-se instal·lat **xserver-xorg-video-openchrome**, s'estava emprant el driver genèric **Vesa**.

La instal·lació del driver (paquet `xserver-xorg-video-openchrome`) i el posterior reinici del sistema gràfic ha bloquejat tot el sistema operatiu amb una pantalla completament negra, fins al punt que ha estat impossible de canviar a cap cònsola virtual en mode text (`Ctrl + Alt + F1..F6`). Ha calgut reiniciar la màquina, entrar en mode de rescat, desinstal·lar el driver *openchrome* i tornar a iniciar amb el driver *Vesa*.

Després de googlejar, he pogut trobar una solució que m'ha funcionat. La versió instal·lada per Stretch és la `xserver-xorg-video-openchrome (1:0.5.0-3)`, alguns usuaris en notificaven el malfuncionament i interferència amb altres elements del maquinari on actuava (wifi, ratolí, etc.). Tots ells ho havien solucionat **reemplaçant aquesta versió per la que es troba a testing** `xserver-xorg-video-openchrome (1:0.6.0-3)`. Eureka!

</div>