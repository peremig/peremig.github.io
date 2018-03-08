--- 
published: true
title: Com enviar els butlletins de notes per correu electrònic
layout: post
author: Pere MiG 
category: howto
tags: 
- PDF
- email
- docència

---
<div style="text-align:center" markdown="1">

![SAGA](https://i1.wp.com/inlab.fib.upc.edu/sites/default/files/styles/galleryformatter_slide/public/saga1.png)

</div>
<div style="text-align:justify" markdown="1">

El proper dissabte comença el descans de setmana santa. Abans, però, en la majoria de centres es lliuraran els butlletins de qualificacions que s’han imprès des de [SAGA](http://educacio.gencat.cat/portal/page/portal/Educacio/PCentrePrivat/PCPInici/PCPGestioAdministrativa/PCPAccesSAGA){:target="_blank"}, un cop acabades les avaluacions del segon trimestre. Aquests butlletins són, en origen, un document PDF generat per aquell aplicatiu; aquest document duu ordenats tots els butlletins de qualificacions dels alumnes d’un grup classe a raó d’un butlletí per pàgina. Amb les retallades econòmiques i l’augment d’hores de dedicació al centre que patim els docents, cal pensar algun sistema que estalviï alhora diners i temps. Pel que fa als butlletins, enviar-los per e-mail (s’estalvien diners de paper, tinta i lloguer de fotocopiadora) i enviar-los de forma automatitzada (estalviem el temps d’ensobrat i de preparació dels butlletins.

<!-- more -->

Els passos a seguir són:

   1. Configuració del servidor de correu electrònic (només cal fer-ho el primer cop que enviem butlletins)
   2. Desmuntar el document generat per SAGA
   3. Enviar els butlletins a les famílies respectives


### Configurar el servidor de correu

Com a servidor de correu, empro Exim4 perquè s’instal·la per defecte a Debian i és fàcil de configurar amb l’ordre dpkg-reconfigure exim4-config. Podem seguir [aquest tutorial en castellà](http://www.elrincondetolgalen.com/2012/07/09/configurar-exim4-com-gmail-como-smarthost-en-debian/){:target="_blank"}. Cal tenir en compte una petita modificació: per enviar correus des de l’adreça <u>usuari@xtec.cat</u>, hem d’editar el fitxer `/etc/exim4/passwd.client` amb les següents dades:

{% highlight Bash shell scripts linenos%}
gmail-smtp.l.google.com:usuari@xtec.cat:password
*.google.com:usuari@xtec.cat:password
smtp.gmail.com:usuari@xtec.cat:password
{% endhighlight %}


### Desmuntar el document generat per SAGA

El document generat per SAGA s’anomena **informe.pdf**, per desmuntar-lo i crear un document PDF per a cada pàgina podem utilitzar *pdftk*:

{% highlight Bash shell scripts %}
$ pdftk informe.pdf burst
{% endhighlight %}

Això és crearà un seguit de fitxers anomenats *pg__000X.pdf*, on X és el número corresponent a la pàgina que ocupa en el document mare (*informe.pdf*). Ara bé, quan passem de les nou pàgines, la numeració elimina un zero (els fitxer passen a ser *pg_00XX.pdf*). Com que encara no tenim grups classe de més de 99 alumnes, la cosa no passa d’aquí; altrament tindríem fitxers *pg_0XXX.pdf*. Es crearà també un fitxer de text que fa les funcions de fitxer de log, és irrellevant per als nostres propòsits, de manera que el podem esborrar.

La manera com ens ha desmuntat el fitxer inicial pot complicar-nos la feina. Personalment, prefereixo un seguit de fitxers anomenat *pN.pdf*, on N sigui el número de pàgina independentment dels dígits que el conformin. He optat, doncs, per reanomenar aquests fitxers amb l’ordre `mv` inserida dins un script de bash (el dono al final d’aquest article).


### Enviar els butlletins a les famílies respectives

Aquest procés ha de ser automàtic. Altrament es converteix en un assumpte més tediós que donar-los en suport físic (paper). Per tant, s’ha de crear un nou script de bash que adjunti cada butlletí a un missatge de correu electrònic apropiat per al seu destinatari. La meva solució opta per servir-se de diferents utilitats:

   - un fitxer de text on es recullin les adreces de correu que rebran els butlletins (**important**: el contingut s’ha d’elaborar a raó d’una adreça per línia i s’han d’ordenar en el mateix ordre que apareix el llistat dels alumnes del grup-classe a SAGA). L’he anomenat *adreces.txt*
   - un fitxer de text on es recull el text que conformarà el cos del missatge. L’he anomenat *mailtext.txt*
   - l’aplicació `read`, que ens servirà per llegir el fitxer d’adreces línia a línia (això és, adreça a adreça)
   - l’aplicació `uuencode`, que ens codificarà el butlletí en format PDF de forma convenient per adjuntar al correu electrònic
   - l’aplicació `mail`, que ens enviarà el correu electrònic a l’adreça desitjada a través d’`exim4`

En aquest procés, l’ordre bàsica és:

{% highlight Bash shell scripts %}
$ (cat mailtext.txt; uuencode ./butlletins/pN.pdf butlleti.pdf) | mail -s "Butlletins de l'avaluació" "$i"
{% endhighlight %}


### Reunim-ho en un script de bash

He reunit tot plegat en un script de bash, el llistat del qual és el següent:

{% highlight Bash shell scripts linenos%}
#! /bin/bash
# Primer pas: desmuntar el pdf amb pdftk fitxer.pdf burst
 mkdir butlletins
 echo "Pas 1: Creant els butlletins..."
 cp informe.pdf ./butlletins
 cd butlletins
 pdftk informe.pdf burst
 rm informe.pdf
 rm *.txt
 echo "... pas 1 fet!"

# Segon pas: reanomenar les pàgines de pg__000X.pdf a pX.pdf 
# i de pg__00XX.pdf a pXX.pdf amb mv
 echo "Pas 2: Preparant-los per trametre..."
 cont=1
 nom="p"
 ext=".pdf"
 for i in $(ls *.pdf)
 do
 nounom=$nom$cont$ext;
 mv $i $nounom;
 cont=$((cont+1));
 done
 cd ..
 echo "... pas 2 fet!"

# Tercer pas: enviar correus amb el butlletí a cada família
echo "Pas 3: enviant butlletins..."
 j=1
 h=1
 while read i
 do echo  "Enviant a $i";
 (cat mailtext.txt; uuencode ./butlletins/p${j}.pdf butlleti.pdf) | mail -s "Butlletins de l'avaluació" "$i"
 j=$((j+h))
 done < adreces.txt
 echo "... tramesa feta. Pas 3 fet!"
{% endhighlight %}

Si es vol utilitzar, n’hi ha prou amb copiar aquest codi i enganxar-ho en un fitxer de text (el meu s’anomena *butlletins.sh*). En fer-ho, tinguem present que li haurem de donar permisos d’execució perquè funcioni.

Requeriments sota Debian: per poder dur a terme aquesta tasca, cal tenir instal·lats els següents paquets (així com les seves dependències):

   - [pdftk](http://packages.debian.org/stable/pdftk){:target="_blank"}
   - [coreutils](http://packages.debian.org/stable/coreutils){:target="_blank"} (ens ofereix l’aplicació ***mv***)
   - [sharutils](http://packages.debian.org/stable/sharutils){:target="_blank"} (ens ofereix l’aplicació ***uuencode***)

</div>