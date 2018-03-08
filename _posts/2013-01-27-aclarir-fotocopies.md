--- 
published: true
title: Aclarir fotocòpies 
layout: post
author: Pere MiG
category: howto
tags: 
- PDF
- xsane

---
<div style="text-align:center" markdown="1">
<img title="Fotocòpia fosca" src="https://i2.wp.com/lh5.ggpht.com/_FSc4oex43IM/TH0EvqR9HBI/AAAAAAAAbiA/L1E2nFY2g7c/s512/L1160785.JPG" alt="Fotocòpia fosca" width="512" height="369" />
</div>
<div style="text-align:justify" markdown="1">
De vegades m’he trobat que haig de fer una fotocòpia d’alguna publicació per passar-la als alumnes i el resultat és força decebedor: o queda molt fosca o queda massa clara, de manera que esdevé inutilitzable.

Hi ha la possibilitat, però, de treballar-la abans amb eines informàtiques: la podrem aclarir o enfosquir per zones de manera que obtindrem un resultat acceptable.

<!-- more -->

El procediment seria el següent:

  - Escanejar el document amb [Xsane](http://www.xsane.org/){:target="_blank"}. Haurem de desar el document en format PNM, escala de grisos i una resolució mínima de 300 ppp (la que millor em resulta és 600 ppp). Si volem escanejar més d’una pàgina, cadascuna d’elles ha de constituir un sol fitxer
  - Treballar la pàgina amb el [Gimp](http://www.gimp.org/){:target="_blank"}. Podrem fer el següent:
     - Girar la pàgina. Opció del menú `Imatge / Transforma`
     - Invertir àrees en negatiu (que gasta molta tinta i deixa un resultat una mica brut). Primer caldrà que les seleccionem. Opció del menú `Colors / Inverteix`
     - Aclarir les zones més fosques del document (per exemple, textos en zones tramades) per esvair o fer desaparèixer el fons negre; en aquest cas hem de seleccionar la zona. Opció del menú `Colors / Llindar blanc i negre` (ho haurem de fer per a cada zona de la pàgina).
     - Amb això ja haurem netejat. A l’hora de desar-lo, anirà bé desar en format PGM

A partir d’aquí podem seguir treballant per obtenir un PDF o bé enviar la imatge des de Gimp a la impressora. En el cas que vulguem obtenir-ne un PDF, caldria continuar des de Bash amb el procediment següent:

  -  Convertir els fitxers nets a TIFF
  -  Agrupar totes les pàgines TIFF en un sol fitxer
  -  Convertir el fitxer grupal a PDF
  -  No és necessari, però m’agrada fer-ho: expandir el contingut perquè ocupi la mida d’un DIN-A4 (o sigui, ampliar la fotocòpia).
  -  Com que per fer el pas anterior, hem hagut de convertir el PDF a PostScript, tornar a convertir-lo a PDF

Això ho he concretat en un script molt simple que executo des de la carpeta on es troben tots els fitxers PGM:

{% highlight YAML %}
#!/bin/bash
for i in *pgm; do convert $i -verbose ${i%pgm}tif; done
tiffcp *.tif monebook.tif
tiff2pdf -o monebook.pdf monebook.tif
pdftops -level3 -paper "A4" -expand monebook.pdf
ps2pdf -dCompatibility=1.4 miebook.ps
{% endhighlight %}

**Crèdits**: aquesta informació constitueix un extracte adaptat de l’article ***[Libritos](http://www.linux-magazine.es/issue/66/070-073_CreaciondeEbooksLM66.pdf)***, de Daniel Stender, aparegut a ***[Linux Magazine, 66](http://www.linux-magazine.es/issue/66)***

**Requeriments sota Debian**: per poder dur a terme aquesta tasca, cal tenir instal·lats els següents paquets (així com les seves dependències):

   - [Xsane](http://packages.debian.org/stable/xsane){:target="_blank"}
   - [Gimp](http://packages.debian.org/stable/gimp){:target="_blank"}
   - [imagemagick](http://packages.debian.org/stable/imagemagick){:target="_blank"} (ens ofereix l’aplicació ***convert***)
   - [libtiff-tools](http://packages.debian.org/stable/libtiff-tools){:target="_blank"} (ens ofeteix les aplicacions ***tiffcp*** i ***tiff2pdf***)
   - [poppler-utils](http://packages.debian.org/stable/poppler-utils){:target="_blank"} (ens ofereix l’aplicació ***pdftops***)
   - [ghostscript](http://packages.debian.org/stable/ghostscript){:target="_blank"} (ens ofereix l’aplicació ***ps2pdf***)

</div>