---
published: true
title: Debian 8 (Jessie) en notebook Acer Aspire V5-121
layout: post
author: Pere MiG 
category: articles
tags:
- Debian
- Jessie
---

<div style="text-align:center" markdown="1">

![Debian Jessie](https://i.imgur.com/aaw0gEC.png%3Fw%3D480?w=400&h=247)

</div>
<div style="text-align:justify" markdown="1">

L’agost de 2013 finalment va morir el meu estimat *Asus Eeepc 701*, de manera que vaig adquirir un notebook nou per reemplaçar-lo. Vaig triar un *Acer Aspire V5-121* després d’haver comprovat que a França en venien una versió amb sistema operatiu GNU/Linux (concretament la distribució *Linpus Linux*).

<!-- more -->

Per fer funcionar correctament el xip **wifi**, cal que el **kernel sigui igual o superior al 3.8.0**, motiu que em va fer decantar per instal·lar, en un primer moment la Kubuntu 13.04 (que més tard vaig actualitzar a 13.10 i a 14.04). En la primera actualització vaig perdre el so (sembla que és un clàssic de la meva relació amb les distribucions derivades d'Ubuntu) i, des d’un primer moment, la visualització de les aplicacions Gnome sota KDE era francament desagradable (fins i tot la de les antigues pantalles de fòsfor verd era millor!).

A més, cap al més de juliol, la placa base va començar a fallar, motiu pel qual vaig enviar a reparar l’aparell al servei tècnic no sense abans haver reformatat l’aparell i haver-ne fet una instal·lació neta mínima. La visualització dels caràcters de les aplicacions Gnome sota KDE continuava tan horrorosa com abans i vaig tornar a tenir feina per configurar el so.

Un cop reparat, vaig decidir que ja n’hi havia hagut prou de Kubuntu i que instal·laria Debian i que, com que Wheezy empra un kernel de la branca 3.2, havia de triar Wheezy + kernel del repositori backports o directament Jessie, que empra kernel de la branca 3.16. Vaig decantar-me per Jessie donat que ja està prou madura (en aquests moments està congelada i s’espera que s’alliberi cap al febrer de 2015, el proper mes).

Ara bé, tot i això, perquè funcioni correctament aquest notebook amb *Debian 8 (Jessie)*, cal tenir la precaució d’instal·lar els següents paquets:

   - **firmware-realtek**, si volem utilitzar la xarxa ethernet, sense aquest paquet el funcionament de la xarxa “de fil” serà erràtic donat que el sistema no trobarà el controlador `rtl_nic/rtl8105e-1.fw`
   - **firmware-linux-nonfree**, essencial per poder activar el xip d’àudio (*Radeon HD 6250/6310*)
   - **fglrx-driver + fglrx-modules-dkms + linux-headers-amd64 + *dependències necessàries***, opcionalment també **fglrx-control**. Això ens instal·larà els controladors de vídeo *Catalyst*. Com que aquest notebook porta un xip *Radeon HD 7290*, els controladors lliures (*xserver-xorg-video-radeon*) no funcionen correctament.

La solució trobada ha acabat amb els problemes de pèrdua de so i de visualització horrible de caràcters de les aplicacions Gnome sota KDE que em trobava amb Kubuntu.

</div>