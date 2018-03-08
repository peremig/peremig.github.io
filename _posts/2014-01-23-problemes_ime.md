--- 
published: true
title: Els meus problemes amb els IME
layout: post
author: Pere MiG 
category: articles
tags: 
- ime
- SCIM
- UIM
- IBUS
- FCITX

---
<div style="text-align:center" markdown="1">

![Fcitx](https://fcitx-im.org/images/1/19/Fcitx-pinyin.png)

</div>
<div style="text-align:justify" markdown="1">

En la migració de Debian Squeeze a Wheezy he trobat un darrer entrebanc: el mètode d’entrada per a caràcters xinesos. Fins ara havia emprat **SCIM** i n’estava força content, però el projecte semblava ja interromput  quan vaig actualitzar a Squeeze i ara sembla ja [totalment abandonat](http://www.scim-im.org/){:target="_blank"}, de fet estava en projecte fer-ne una nova generació d’SCIM anomenada [SCIM2](http://code.google.com/p/scim2/){:target="_blank"}, que va ser abandonada al seu torn quan alhora va començar el projecte *IBus*. A més a més, ja no existeix el [paquet corresponent al mètode d’entrada per pinyin en els repositoris de Wheezy](http://packages.debian.org/search?keywords=scim&searchon=names&suite=stable&section=all){:target="_blank"}.

<!-- more -->

S’imposa, doncs, la migració a un altre mètode d’entrada (cosa que ja [havia intentat el 2011 amb l’ibus](/article/2011/02/10/perque_no_ibus.html){:target="_blank"}, però que vaig descartar perquè no admetia la introducció de caràcters accentuats).  En aquesta migració he provat tres IME, dels quals n’he hagut de descartar dos:

### UIM

Ha estat el primer que he instal·lat i he intentat fer funcionar. No he estat capaç d’arrencar cap mètode d’entrada pinyin per al xinès simplificat. Sembla ser que funciona força bé amb el japonès, però com que no en sé, no he instal·lat cap mètode d’entrada per al japonès. Després de molt googlejar i de força intents frustrants, he desinstal·lat i purgat tot els paquets que havia introduït al meu sistema.

### IBUS

A continuació, he donat una segona oportunitat a aquest IME que havia descartat dos anys abans. Continua tenint errors importants i inexplicables: ara ja permet caràcters accentuats, però no pas en totes les aplicacions. És especialment greu la seva [incompatibilitat amb Libreoffice](http://forums.debian.net/viewtopic.php?t=76716){:target="_blank"},  amb aquesta aplicació és possible emprar el mètode d’entrada per al xinès, però no pas els caràcters accentuats (però si que permet introduir la `ç`, la `ŀ` i la `ñ`). és més, desactiva la tecla *Compose* (que tinc assignada a *Win esquerra*). Sembla funcionar bé, en canvi, amb altres aplicacions *KDE* (com ara *KWrite*).

[Aquestes disfuncions es documenten almenys des de 2010 fins a l’actualitat](https://duckduckgo.com/?q=ibus+libreoffice&t=debian){:target="_blank"} i amb diferents distribucions Linux (Debian, Ubuntu, Arch, OpenSuse, Fedora, etc) sense que estiguin encara resoltes del tot [ni sembli clara la voluntat de resoldre-les](https://bugs.launchpad.net/ubuntu/+source/ibus/+bug/1007423){:target="_blank"}.

L’única manera d’escriure caràcters accentuats amb Libreoffice és desactivar l’**ibus** (tancar-lo) i iniciar-lo abans d’escriure en xinès (ara bé, en alguna pàgina web s’adverteix que l’ibus provoca tancaments sobtats i  de les aplicacions de Libreoffice al cap d’una estona de treballar-hi; no he comprovat, però).

### FCITX

Ha estat el tercer IME que he provat i amb el que m’he quedat. La instal·lació és senzilla i ràpida a partir dels paquets dels repositoris Debian i ha funcionat des del primer moment amb totes les aplicacions on l’he provat (incloent-hi Libreoffice).

El seu punt més fort és que les diferents opcions que ofereix es presenten en un tipus de lletra clar i gros, clarament llegibles (a diferència d’*ibus* i *scim*), cosa que és d’agrair a partir de certes edats.

El seu punt més feble és que les diferents *hotkeys* es basen en la distribució del teclat americà (*us keyboard*), de manera que les tecles que s’assignen per defecte per visionar diferents conjunts d’opcions (cinc per defecte, però la xifra és configurable), no corresponen a les que trobem impreses sobre el teclat català. Així, doncs, per defecte s’utilitza «=» per a mostrar les opcions següents i «-» per mostrar-ne les anteriors, però en el nostre teclat, aquestes opcions se situen a les tecles «¿¡»  i «?’» respectivament (també podem configurar aquestes opcions).

### Addenda

Un cop acabada la tria del nou IME, he ensopegat amb dues pàgines que poden ajudar qui es trobi en una situació anàloga a la que he descrit. La primera [analitza diferents IME per a Linux](http://www.verious.com/article/linux-input-method-framework-brief-summary/){:target="_blank"} a data 15 de gener de 2011. La segona és, de fet, la resposta a la pregunta *[What’s your favourite user input method?](http://chakra-project.org/bbs/viewtopic.php?id=10365){:target="_blank"}*  que es va fer dins del fòrum de Chakra per triar quin seria l’IME “oficial” d’aquesta distribució, aquesta pregunta es va fer el 5 de maig de 2013 i les respostes (poques) arriben fins al 7 de gener de 2014; aquesta pàgina ens pot ajudar a triar l’IME més adient per a la llengua en què vulguem escriure, en resum seria:

   + [FCITX](https://fcitx-im.org/wiki/Fcitx){:target="_blank"} seria el millor IME per a **xinès simplificat**, però no gaire adequat per a japonès.
   + [GCIN](https://code.google.com/p/gcin/){:target="_blank"} seria el millor IME per a **xinès tradicional** (si més no, el més emprat per a aquesta finalitat)
   + [IBUS](https://code.google.com/p/ibus/) seria l’IME més emprat per a **japonès** i el que més suport presenta per a les **llengües de l’Índia**
   + [UIM](https://code.google.com/p/uim/){:target="_blank"} és un IME adequat per a **japonès**
   + Per al **Coreà**, hom aconsella *FCTIX* en comptes d'*IBUS*


</div>