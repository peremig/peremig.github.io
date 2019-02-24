--- 
published: true
title: Música en lloc de timbre
layout: post
author: Pere MiG 
category: howto #articles
tags: 
- mpv
- recutils
- cron

---
<div style="text-align:center" markdown="1">

![Esbarjo](http://niuniformesnietiquetes.esy.es/wp-content/uploads/2018/06/1r.jpg)

</div>
<div style="text-align:justify" markdown="1">

L'institut on presto serveis no fa servir el clàssic timbre que marca els finals de les sessions de classe. Aquest, en principi, funcionament sorprenent, ha resultat molt satisfactori excepte en un sol cas: **el final de l'esbarjo**. L'alumnat, sempre atent al final de classe, calia ser avisat quan acabava l'esbarjo. Davant d'això es va decidir utilitzar música en lloc de timbre, música que seria proposada pel mateix alumnat.

L'alumnat ha proposat sempre música de [Youtube](https://www.youtube.com/){:target="_blank"} i s'ha executat sempre des d'un ordinador connectat a un equip de so. L'execució de tot plegat ha estat sempre manual (un professor, el coordinador informàtic, anava a l'ordinador, obria Youtube al navegador i hi inseria la pàgina proposada per l'alumnat). Darrerament el coordinador informàtic m'ha demanat si coneixia algun programa o aplicació per automatitzar-ho.

No en conec cap per Windows, de fet fa vora quinze anys que vaig deixar d'utilitzar-lo. Però és una tasca força senzilla amb un **cron** que executi un *script*. Comparteixo el que he elaborat per al meu institut.

<!-- more -->

La base de l'*script* rau en els passos següents:

   1. La pàgina de Youtube se selecciona aleatòriament d'una base de dades de pàgines proposades per l'alumnat.
   2. S'executa la música

A continuació dono el codi de l'*script*, anomenat `timbres.sh`:

{% highlight Bash shell scripts%}

#!/bin/bash

timbre=$(recsel -m 1 -t Timbre -P url timbres.rec)
mpv --start=0 --length=2:00 ${timbre} 2>/dev/null

{% endhighlight %}

Per activar-lo cal incloure'l com una tasca **cron** de l'usuari amb `crontab -e`; en el cas del meu institut on fem dos esbarjos per grup (el segon esbarjo és diferent per a primer i segon cicle d'ESO) i només se n'indica la finalització:

{% highlight Bash shell scripts%}

00 11 * * 1-5           /home/USER/timbres.sh   # De dl a dv a les 11:00
00 13 * * 1-5           /home/USER/timbres.sh   # De dl a dv a les 13:00
03 13 * * 1-5           /home/USER/timbres.sh   # De dl a dv a les 13:30

{% endhighlight %}


He desestimat fer una base de dades SQL ja que no calen dades relacionals ni massa potència de màquina (de fet, podria controlar-se des d'una Raspberry Pi 3 dedicada), per aquesta raó, he decidit utilitzar [recutils](https://packages.debian.org/stretch/recutils){:target="_blank"}, un sistema de base de dades en mode text de molt fàcil accés i que, a més, presenta una comanda amb paràmetres per obtenir un o diversos registres aleatoris d'una base.

La capçalera del fitxer, anomenat `timbres.rec` on es contenen les propostes de l'alumnat seria com següeix:

{% highlight Bash shell scripts%}

%rec: Timbre
%key: Id
%type: Id int
%mandatory: url interpret
%auto: Id

{% endhighlight %}

Un exemple de registre, seria el següent:

{% highlight Bash shell scripts%}

Id: 0
url: https://youtu.be/BeH2eH9iPw4
interpret: Txarango

{% endhighlight %}

El manteniment d'aquesta base de dades és molt senzill, així, per exemple, per inserir registres a la base de dades cal executar  `recins -t Timbre -f url -v "URL" -f interpret -v "INTÈRPRET" timbres.rec`, on substituïm *URL* per l'adreça de Youtube i *INTÈRPRET* pel seu intèrpret. No podem deixar cap dels dos en blanc, ja que en la capçalera es configuren com a camps requerits.

Exemple:

{% highlight Bash shell scripts%}

recins -t Timbre -f url -v "https://youtu.be/BeH2eH9iPw4" -f interpret -v "Txarango" timbres.rec

{% endhighlight %}

El fet d'utilitzar un camp *interpret* és per facilitar l'esborrat dels registres, així, per esborrar un registre cal executar `recdel -t Timbre -q EXPRESSIÓ timbre.rec` on hem de subtituir *EXPRESSIÓ* per una sola paraula que ens identifiqui clarament l'intèrpret.

Per esborrar el registre que eb¡ns està servint d'exemple, podríem escriure:

{% highlight Bash shell scripts%}

recdel -t Timbre -q Txarango timbres.rec

{% endhighlight %}

Finalment, pel que fa al reproductor de vídeo, he optat per **mpv**, en comptes de **vlc** ja que aquest segon no es tancava un cop acabada la reproducció de la música (s'ha provat amb la versió 3.0.6) i, en alguna ocasió, fallava en obrir l'*streaming*.

Requeriments sota Debian: per poder dur a terme aquesta tasca, cal tenir instal·lats els següents paquets (així com les seves dependències):

   - [recutils](https://packages.debian.org/stable/recutils){:target="_blank"} (ens ofereix les aplicacions *recsel*, *recins* i *recdel*)
   - [mpv](https://packages.debian.org/stable/mpv){:target="_blank"} (ens ofereix l’aplicació *mpv*)
   
</div>
