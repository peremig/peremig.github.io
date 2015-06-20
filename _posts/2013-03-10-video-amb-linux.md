--- 
published: true
title: Vídeo amb GNU/Linux
layout: post
author: Pere MiG
category: articles
tags: 
-  vídeo

---

<div style="text-align:center" markdown="1">
![Vídeo amb Linux](https://i1.wp.com/www.pcactual.com/medio/2010/01/26/edita_videoen_linux_con_kdenlive_618x380.jpg)
</div>

<div style="text-align:justify" markdown="1">
En el marc de l’edició del concurs [Viquilletra 2013](http://lletra.uoc.edu/viquilletra/Viquilletra){:target="_blank"} (on han participat alumnes d’un grup de 4t d’ESO), vaig assistir a un seminari de vídeo impartit per un formador de la [XTEC](http://www.xtec.cat/web/guest/home){:target="_blank"}. La sessió, de quatre hores de durada, va ser molt profitosa i interessant. Després d’una introducció teòrica que havia de durar una hora (i que es va allargar una mica més), es va passar a la part pràctica, on entre tots els assistents havíem de crear un vídeo a partir d’una obra literària catalana.

Com que calia que cadascú portés el seu portàtil, ens hi vam trobar amb tres sistemes diferents: Windows, Mac i GNU/Linux (aquest darrer minoritari, només jo). Es va plantejar, doncs, el problema de les compatibilitats; el formador va recomanar el *Movie maker* per a Windows i l'*iMovie* per als que duien Mac. Pel que fa a GNU/Linux, va dir que *no hi ha un editor de vídeo satisfactori* (sic). Quan li vaig exposar diferents alternatives, va reconèixer que li sonava *un tal Cinelerra molt complicat i Kdenlive*, i que mai no havia utilitzat cap dels dos; per la qual cosa vaig deduir que la seva valoració sobre els editors de vídeo amb GNU/Linux partia d’apriorismes sense cap altres fonaments que el desconeixement i el prejudici.

<!-- more -->

Personalment, conec força bé [Kdenlive](http://www.kdenlive.org/){:target="_blank"} i no hi he trobat a faltar res que tinguin altres editors de vídeo d’altres plataformes. Però, a més, i a banda de [Cinelerra](http://cinelerra.org/){:target="_blank"}, els usuaris de GNU/Linux disposem d’altres opcions com ara

   - [Open movie editor](http://www.openmovieeditor.org/){:target="_blank"},
   - [Openshot video editor](http://www.openshotvideo.com/){:target="_blank"},
   - [LiVES](http://lives.sourceforge.net/){:target="_blank"},
   - [PiTiVi](http://www.pitivi.org/){:target="_blank"},
   - [Stopmotion](http://linuxstopmotion.org/){:target="_blank"}
   - [Blender](http://www.blender.org/){:target="_blank"}
   - …

Encara més, només amb el terminal podem treballar sobre vídeos amb [FFmpeg](http://www.ffmpeg.org/){:target="_blank"} i [Mencoder](http://www.mplayerhq.hu/design7/news.html){:target="_blank"} amb els quals, a banda de convertir entre diferents formats de vídeo, separar imatge de so, etc., també podem crear diversos efectes.

Treballant amb edició de vídeo amb *Kdenlive*, només un cop no vaig saber com crear un efecte: el de rebobinat de cinta de vídeo (encara ara no sé com fer-lo).  Ho vaig solucionar ràpidament amb *Openshot*, on aquesta opció es troba ràpidament en el seu menú d’efectes.

Per acabar, dues anècdotes. Una d’antiga, el 2006, quan començava amb això de GNU/Linux, vaig trobar-me editant un vídeo amb un programa propietari sota Windows (penso que era *Pinacle Studio 8*); va ser impossible fer un clip de més de 15 minuts sense que el programa petés i, encara més impossible, crear un DVD de vídeo. Amb GNU/Linux no se m’ha presentat mai aquest problema i, amb [‘Q’ dvdauthor](http://qdvdauthor.sourceforge.net/){:target="_blank"}, crear un DVD vídeo és una tasca força fàcil i visual (de fet, hi he creat algun DVD de 80 minuts de durada).

La segona anècdota és més moderna i es va esdevenir en el seminari a què vaig assistir. Hi havia assistents que duien Windows i altres que duien Mac; cadascun va crear els seus clips de vídeo. Quan els vam voler ajuntar va aparèixer la incompatibilitat dels formats de vídeo propietari (*mov* i *wmv*). A més a més, cap dels programes amb què els havien creat permetia la conversió a un format comú. Cap? No, per sort hi havia algú (jo) que duia GNU/Linux i, amb una senzilla comanda de *Ffmpeg* (aplicació que era desconeguda per al formador), es van convertir tots els vídeos a un format comú i es van poder deixar els clips llestos per al muntatge final. La comanda va ser: `ffmpeg -i FitxerEntrada FitxerSortida`, on l’extensió del fitxer n’indica el format.

</div>