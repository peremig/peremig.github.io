--- 
published: true
title: De debian squeeze a wheezy (1)
layout: post
author: Pere MiG 
category: howto
tags: 
- Debian
- Squeeze
- Wheezy
- vídeo
- nvidia

---
<div style="text-align:center" markdown="1">

![nVidia](https://i1.wp.com/kbase.vectorworks.net/images/nvidia-2.jpg)

</div>
<div style="text-align:justify" markdown="1">

Aquestes vacances de Cap d’Any he estat migrant d’Squeeze a Wheezy (versió 7.3). Tot ha anat bé llevat de dues qüestions: la gràfica i el so. En aquest primer post tractaré de com he resolt el sistema gràfic (ja que va ser el primer que vaig resoldre).

<!-- more -->

El sistema actualitzat és un pèl antic, es tracta d’un AMD 386, amb una gràfica amb xip *nvidia Geforce 6200LE*, per la qual cosa, almenys en teoria, no hauria de tenir problemes amb les drivers lliures *nouveau*. D’entrada, cal dir ja que en la versió Squeeze aquests drivers no havien funcionat, per la qual cosa vaig optar per baixar-ne els drivers propietaris de la web d’*nvidia* i compilar-los. Tot i que sempre van funcionar correctament, la veritat és que el procediment era una mica pesat, ja que qualsevol actualització del kernel linux o del servidor gràfic *x.org* m’obligava a recompilar-ne els drivers.

En arrencar Wheezy amb els drivers nouveau, feia la impressió que estigués arrencant un Windows: el sistema arrencava lentament i el servidor gràfic anava força lent (a trompades); és més, al cap d’una estona i quan es començava a fer ús de la multitasca, feia la impressió que tot el sistema s’hagués penjat (el sistema gràfic es congelava i deixava de respondre a ratolí i a teclat).

La solució passa per desintal·lar els drivers *nouveau* i fer servir els drivers propietaris. Si intentem la via fàcil (desintal·lar i purgar el paquet *xserver-xorg-video-nouveau* i instal·lar el paquet *xserver-xorg-video-nvidia*), observarem que no només no funciona, sinó que ni tan sols arrenca el servidor gràfic. Arreglar-ho demana uns quants passos més:

  1. Eliminar el fitxer */usr/lib/xorg/modules/drivers/nouveau.so*
  2. Obligar el servidor gràfic a emprar els drivers propietaris i, per tant, crear el fitxer */etc/X11/xorg.conf* amb almenys les línies següents:

{% highlight Bash shell scripts%}

Section "Screen"
	Identifier	"Default screen"
	Device		"Default Video Card"
	DefaultDepth	24
EndSection

Section "Device"
	Identifier	"Default Video Card"
	Driver		"nvidia"
EndSection

{% endhighlight %}

Reiniciem llavors el servidor gràfic (o tot el sistema, com ho preferim) i ja tindrem el sistema gràfic amb la potència i fiabilitat de GNU/Linux, amb l’avantatge (respecte de la compilació dels drivers), que qualsevol actualització que es faci del nucli Linux o de les *X* ens  recompilarà els drivers de forma totalment automàtica. El desavantatge és que no disposarem dels darrers drivers publicats per *nvidia*.

</div>