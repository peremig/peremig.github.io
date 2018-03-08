--- 
published: true
title: De debian squeeze a wheezy (2)
layout: post
author: Pere MiG 
category: howto
tags: 
- Debian
- Squeeze
- Wheezy
- audio
- AC'97

---
<div style="text-align:center" markdown="1">

![Mute](/images/mute_icon.png)

</div>
<div style="text-align:justify" markdown="1">

Comentava en l’entrada anterior com en la migració d’squeeze a wheezy m’havien fallat el sistema gràfic i el so. En el post anterior mostrava com s’havia solucionat la fallada del servidor gràfic. En aquest es mostrarà com s’ha arreglat el sistema d’àudio.

<!-- more -->

El xip d’àudio que utilitza el maquinari és un SiS SI7012 integrat en la placa base, no havia mostrat mai símptomes de mal funcionament en cap de les versions anteriors de Debian emprades (la primera amb aquest maquinari va ser *Sarge*, Debian 3.0), però havia mostrat un comportament una mica erràtic sota *Ubuntu 6.06 LTS* (que es va solucionar migrant a Debian Sarge).

En acabar la instal·lació de Wheezy (es va optar per fer una instal·lació neta del sistema en comptes d’una actualització des d’Squeeze), sobtava que el sistema estava mut. La icona del mesclador de so *kmix* apareixia amb el símbol d’altaveu mut i era impossible activar el so a través dels controladors dels mesclador.

Una revisió de la instal·lació amb les comandes `aplay -l`, `aplay -L`, `lspci` i `cat /proc/asound/modules` semblava indicar que tot era correcte, però no hi havia so. En arrencar l’*alsamixer*, es mostrava com a sistema de so per defecte *pulseaudio*.

Una recerca a [Google](https://encrypted.google.com/search?hl=en&q=debian%20wheezy%20%22SiS%20SI7012%22){:target="_blank"}, em va fer veure que aquest problema ja havia aparegut amb Squeeze i afectava també el xip *SiS AC’97*. Les [diferents solucions que hom hi aportava](https://www.debian-fr.org/pas-de-son-avec-squeeze-t37367.html){:target="_blank"} no em van funcionar. Vaig recordar que l’*Asus Eeepc 710* duu com a xip de so un AC’97 i que en fer-li la migració a Wheezy el passat estiu no n’havia experimentat cap problema. Així que vaig decidir revisar-li la instal·lació i configuració per mirar de treure’n l’entrellat.

La sorpresa me la va donar l’*alsamixer*, en l’Eeepc el sistema de so per defecte no era *pulseaudio* (de fet ni tan sols hi apareixia). La raó era molt senzilla: *pulseaudio* no estava instal·lat en l’Eeepc; així, doncs, la solució ha estat tan senzilla com desintal·lar *pulseaudio* en l’ordinador de sobretaula (deixant-hi, però, els paquets `libpulse-mainloop-glib0` i `libpulse0`). Un cop reiniciat el sistema de so (o tota la màquina, si es prefereix) i ajustats els controladors del mesclador de so, s’ha acabat amb la mudesa de Wheezy.

Queda per explicar per què la instal·lació de l’Eeepc no duia el sistema de so *pulseaudio*. En aquesta màquina, i donada la seva poca capacitat de disc (4 GB), es va fer una instal·lació del sistema base que es va anar completant a mà (sense utilitzar les Tasques de Debian); en instal·lar el so, es va instal·lar el sistema de so *alsa* de la manera més mínima possible, per la qual cosa es va obviar *pulseaudio*.

</div>