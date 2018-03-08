--- 
published: true
title: Emacs i el xinès (fcitx)
layout: post
author: Pere MiG 
category: howto
tags: 
- ime
- emacs
- FCITX

---
<div style="text-align:center" markdown="1">

![Emacs](https://llaisdy.files.wordpress.com/2009/02/echimp21.png%3Fw%3D480?w=490&h=247)

</div>
<div style="text-align:justify" markdown="1">

Lligant amb l’article sobre els diferents IME a què m’he acostat, he preferit deixar per a un article posterior (aquest), la relació de l’IME triat amb [Emacs](https://www.gnu.org/software/emacs/){:target="_blank"}. De fet *Emacs* ja porta incorporat el seu IME i, en un determinat moment, quan ja gairebé desesperava de trobar un bon substitut per a *scim*, vaig valorar seriosament la possibilitat de no instal·lar-ne cap i fer servir aquest editor de textos quan em calgués escriure res en xinès. Ara bé, com es pot veure en la imatge que acompanya aquestes línies (una mica obsoleta, però serveix), la visualització dels caràcters xinesos és un pèl deficient (sobretot si emprem un netbook).

<!-- more -->

El problema ve donat pel fet que sembla ser que els diferents IME externs no es comuniquen bé amb Emacs; de manera que el més comú és que, d’entrada, no només no funcionin sinó que, a més a més, desactivin la possibilitat d’escriure paraules accentuades (maten les *dead keys*, que substitueixen per una pitada esquerdada) així com la tecla *compose*, que deixa d’actuar i se substiteix per la mateixa pitada esquerdada quan s'intenta activar.

### Com comunicar un IME extern amb *Emacs*

Els diferents IME presenten diferents solucions per a comunicar-se amb Emacs, la més estesa (compartida per *scim*, *ibus* i *uim*) és la instal·lació d’una aplicació *elisp* a què es crida mitjançant el fitxer de configuració `.emacs` que se situa en el *home* de l’usuari.

*Fcitx*, per contra, [crida Emacs passant-li una variable d’entorn LC_CTYPE assignada a xinès simplificat](https://fcitx-im.org/wiki/FAQ#Emacs){:target="_blank"} amb la comanda:

{% highlight bash %}
$ LC_CTYPE=zh_CN.UTF-8 emacs
{% endhighlight %}

Aquesta comanda no canvia el *locale* del sistema i activa *fcitx* per a *Emacs*. Cal, però, [haver definit abans el locale](https://wiki.debian.org/Locale){:target="_blank"} que es passa amb la variable d’entorn LC_CTYPE (en aquest cas `zh_CN.UTF-8`). La manera més senzilla en un sistema debian és emprant la comanda `# dpkg-reconfigure locales` (com a *root*)

Ara bé, això no arregla el problema dels accents ni el de la tecla *compose*. La [solució, referida a uim](https://xmleye.wordpress.com/2009/12/13/entrada-de-acentos-y-japones-en-emacsgtkkde-en-ubuntu-9-10-karmic-koala/){:target="_blank"}, ens la dóna Antonio García-Domínguez, de la Universitat de Cadis: consisteix en cridar *Emacs* buidant-li la variable d’entorn XMODIFIERS a través de la comanda

{% highlight bash %}
$ XMODIFIERS=@im=none emacs
{% endhighlight %}

Cridar així *Emacs* ens restablirà els accents i la tecla *compose*, però no ens comunicarà *Fcitx* amb *Emacs*, raó per la qual no hi podrem emprar l’IME.

### *Emacs* + *fcitx* + accents + *compose*

La solució és cridar *Emacs* passant-li el valor de les dues variables alhora. Això ho podem fer amb la instrucció següent:

{% highlight bash %}
$ LC_CTYPE=zh_CN.UTF-8 emacs | XMODIFIERS=@im=none
{% endhighlight %}

I ara sí, ja tindrem l’*Emacs* amb *fcitx* de forma totalment funcional i hi podrem usar aquest IME a més a més dels que aquest editor ja porta incorporats. Només quedarien per fer uns petits detalls:

   - **Canviar l’assignació de la combinació *Ctrl+Espai*** a *Emacs* (on indica inici-final de marca) o a *fcitx* (on commuta el mètode d’entrada)
   - **Modificar les entrades del menú del *KDE* que es refereixen a *Emacs*** (normalment hi trobarem alguna cosa semblant a `/usr/bin/emacs23 %F` i les canviarem per `LC_CTYPE=zh_CN.UTF-8 /usr/bin/emacs23 %F | XMODIFIERS=@im=none`)
   - **Opcionalment, col·locar una icona a l’escriptori de treball** (a *KDE* consisteix en clicar amb el botó dret del ratolí sobre l’entrada del menú i triar l’opció *Afegeix a l’escriptori*)
   - **Només si hi ha diferents usuaris que utilitzen *Emacs* i *fcitx***, caldrà instal·lar-hi una nova alternativa que reculli les modificacions de les dues variables LC_CTYPE i XMODIFIERS, més o menys [com fa García-Dominguez per a uim](https://xmleye.wordpress.com/2009/12/13/entrada-de-acentos-y-japones-en-emacsgtkkde-en-ubuntu-9-10-karmic-koala/){:target="_blank"}.

</div>