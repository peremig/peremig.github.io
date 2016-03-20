--- 
published: true
title: Torna Firefox a Debian
layout: post
author: Pere MiG 
category: articles #howto
tags: 
- Iceweasel
- Firefox
- Debian

---
<div style="text-align:center" markdown="1">

![Firefox](images/firefox.png)

</div>
<div style="text-align:justify" markdown="1">

El novembre de 2006, *Debian* presentava [**Iceweasel**](https://ca.wikipedia.org/wiki/IceWeasel){:target="_blank"}, un fork de [**Firefox**](https://www.mozilla.org/ca/firefox/new/){:target="_blank"} motivat per discrepàncies amb *Mozilla Foundation* sobre el caràcter de la llicència relativa a la marca del producte i el seu logotip.

Deu anys després, el [17 de febrer de 2016](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=815006#5){:target="_blank"} Debian ha anunciat que reconeix que **Firefox** compleix amb la [llicència DFSG](https://www.debian.org/social_contract.ca.html#guidelines){:target="_blank"} i Mozilla que les modificacions aplicades a **Iceweasel** no han impactat sobre la qualitat del producte. De manera que el passat 9 de març, *Debian* [ha anunciat la desaparició d'**Iceweasel**](https://www.debian.org/security/2016/dsa-3510){:target="_blank"} i la seva substitució per **Firefox**. És més, el proper *Debian Strech* portarà paquets de **Firefox** enlloc de paquets d'**Iceweasel**.

<!-- more -->

De fet, des de dijous 10 de març, ja no es possible actualitzar **Iceweasel**, que ha mort en la versió 44.0.2. Una crida `# aptitude -u` ens mostra un missatge d'error indicant-nos que no ha pogut resoldre la següent entrada de `/etc/apt/sources.list`:

{% highlight Bash shell scripts%}

# iceweasel
deb http://mozilla.debian.net/ jessie-backports iceweasel-release

{% endhighlight %}

Per continuar tenint suport d'actualitzacions de seguretat tenim dues solucions: fer un *downgrade* a **Iceweasel** versió 38.7.0esr-1 o substituir-lo pel backport de **Firefox** (versió 45.0.1 en el moment d'escriure aquestes línies).

En el primer cas haurem de comentar o esborrar primer la línia que ens ha produït l'error en el nostre `/etc/apt/sources.list` i assegurar-nos que hi tinguem la línia:

{% highlight Bash shell scripts%}

deb http://security.debian.org/ jessie/updates main

{% endhighlight %}

després caldrà fer *downgrade* de la manera habitual.

En el segon cas, l'haurem de substituir per

{% highlight Bash shell scripts%}

# firefox
deb http://mozilla.debian.net/ jessie-backports firefox-release

{% endhighlight %}

després desinstal·lar **Iceweasel** i finalment instal·lar **Firefox**.

</div>