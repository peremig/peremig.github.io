--- 
published: true
title: Dictats autocorrectius amb GNU/Linux 
layout: post
author: Yu
category: howto
tags: 
- dictat
- iconv
- rename
- sed
- wdiff

---
<div style="text-align:center" markdown="1">
![Dictat](https://deixebledetux.files.wordpress.com/2013/03/dictat.jpg?w=221&h=160)
</div>

<div style="text-align:justify" markdown="1">

Avui dia, el dictat és un procediment que té poc prestigi (potser és perquè durant el segle XX per aquí hi va haver abundor de dictadors, o potser és perquè el més pesat de tot és haver-los de corregir); malgrat tot, encara és una pràctica útil que relaciona com cap altra el so amb la grafia que el representa.

Com acabo d’apuntar, el més pesat del dictat és la seva correcció. La combinació d’unes poques eines sota GNU/Linux ens automatitzen aquesta tasca tan pesada (i més encara si volem). I, el que és més interessant, és que utilitzarem el format text pla (TXT).

<!-- more -->

El procés a seguir és el següent:

   1. Es fa el dictat (pot ser a càrrec del professor o, fins i tot, a través de síntesi de veu).
   2. Es fa una comparació automatitzada amb el text que s’ha dictat.
   3. Es retorna als alumnes .

Necessitem tres aplicacions:

   - **iconv** (només si el nostres alumnes utilitzen Windows o qualsevol altre sistema que encara no codifiqui amb UTF-8)
   - **wdiff**
   - **sed**
   - **rename**

Els meus alumnes, que treballen amb ordinadors de l’Educat 1×1 (després va ser Educat  2.0), empren gairebé sempre l’entorn Windows, per la qual cosa, codifiquen el text en Latin-1. El primer pas a fer consiteix en canviar la codificació a UTF-8, cosa que, des de la terminal es fa amb l’ordre:

`iconv -f LATIN1 -t UTF-8 -o FITXERi.utf FIXTER.latin1`

Com que tenim més d’un alumne, farem la conversió dins d’un bucle (assumim que tots els fitxers dels alumnes tenen l’extensió TXT):

`for i in $( ls *.txt); do iconv -f LATIN1 -t UTF-8 -o $i.utf $i; done`

El següent pas,  seria ja corregir-los el dictat. Per fer-ho, comparem els fitxers dels alumnes amb el fitxer que contindrà el text correcte que els hem dictat. Aquesta comparació es fa mot a mot (d’aquí que s’utilitzi wdiff i no pas diff). Aquesta utilitat ens dóna diferents opcions de sortida:

   - tot el text amb els inputs incorrectes al costat del correctes sense estadístiques encert / error
   - tot el text amb els inputs incorrectes al costat del correctes amb estadístiques encert / error
   - tot el text amb les formes correctes de les errades (però sense mostrar-ne la forma errònia que ha introduït l’alumne)
   - només les errades amb les formes correctes al costat (separades per línies i sense mostrar la resta del text)

Les ordres corresponents són:
{% highlight bash %}

$ wdiff -1 dictat_original dictat_alumne.txt #tot el text amb els inputs incorrectes al costat del correctes sense estadístiques encert / error 

$ wdiff -s dictat_original dictat_alumne.txt #tot el text amb els inputs incorrectes al costat del correctes amb estadístiques encert / error 

$ wdiff -2 dictat_original dictat_alumne.txt #tot el text amb les formes correctes de les errades (però sense mostrar-ne la forma errònia que ha introduït l’alumne)

$ wdiff -3 dictat_original dictat_alumne.txt #només les errades amb les formes correctes al costat (separades per línies i sense mostrar la resta del text)
  
{% endhighlight %}

Les ordres anteriors en mostraran la comparació en pantalla, però com el que ens interessarà serà produir un nou document per analitzar-lo (ja sigui per nosaltres o pels alumnes), emprarem la redirecció a fitxer de la sortida, per exemple:

{% highlight bash %}
  $ wdiff -3 dictat_original dictat_alumne.txt > dictat_corregit.txt
{% endhighlight %}
Però, perquè ens sigui realment útil, tot això s’hauria de poder resumir en una sola ordre de la terminal. Hem de crear, per tant, un script de Bash i, per obtenir una sortida ordenada, ens anirà bé emprar les comandes sed i rename. Si hem anat seguint fins aquí, haurem observat que es creen fitxers de text, que cal que tinguin extensions diferents i que, al final, haurem de poder localitzar ràpidament els resultats.

Un script pot ser el següent:

{% highlight Bash shell scripts linenos%}

 #!/bin/bash
 echo "Convertint a UTF-8..."
 for i in $( ls *.txt); do iconv -f LATIN1 -t UTF-8 -o $i.utf $i; done
 mkdir utf
 for i in $( ls *.txt); do mv $i.utf ./utf/$i; done
 cp dictat ./utf/dictat.txt
 cd utf
 echo "Corregint..."
 for i in $( ls *.txt); do sed "s/$/\n/" $i >$i.nou; done
 for i in $( ls *.nou); do wdiff -s $i dictat.txt.nou> $i.res; done
 rm *.txt
 rm *.nou
 rm dictat.*
 rename 's/\.nou.res$//' *.res
 echo "Fet!"
 
{% endhighlight %}

Al final de la seva execució, trobarem una carpeta /utf  dins de la qual hi seran els dictats dels alumnes en codificació UTF-8 i ja corregits (en aquest cas, el fitxer corregit de cada alumne contindrà tot el text amb les formes incorrectes -entre claudàtors- que ha introduït al costat de les correctes -entre claus- i, al final, l’estadística d’encerts / errors). Vegem-ne un exemple de fitxer de sortida:

>Els caçadors [-fortius cercan-] {+furtius cerquen+} els grans goril·les mascles per convertir el seu crani en [-petxa papers,-] {+petjapapers,+} i les mans i els [-peus,-] {+peus+} en cendrers, que venen a uns preus que s'acosten [-els-] {+als+} 50 [-dolars-] {+dòlars+} la peça. Els caçadors més [-ábils-] {+hàbils+} capturen vius [-als-] {+els+} goril·les més joves i els [-subasten-] {+subhasten+} per exportar-los [-il·legantment-] {+il·legalment+} a [-zoologics-] {+zoològics+} i col·leccions privades [-de reu-] {+d'arreu+} del món.
>
>alumne.txt: 61 paraules  47 77% comunes  0 0% esborrades  14 22% canviades
>
>dictat.txt: 59 paraules  47 79% comunes  0 0% inserides  12 20% canviades

Requeriments sota Debian: per poder dur a terme aquesta tasca, cal tenir instal·lats els següents paquets (així com les seves dependències):

   - [libc-bin](https://packages.debian.org/stable/libc-bin){:target="_blank"} (ens ofereix l’aplicació *iconv*)
   - [wdiff](https://packages.debian.org/stable/wdiff){:target="_blank"}
   - [sed](https://packages.debian.org/stable/sed){:target="_blank"}
   - [util-linux](https://packages.debian.org/stable/util-linux){:target="_blank"} (ens ofereix l’aplicació *rename*)


</div>