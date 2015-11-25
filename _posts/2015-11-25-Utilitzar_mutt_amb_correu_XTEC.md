--- 
published: true
title: Utilitzar mutt amb correu XTEC
layout: post
author: Pere MiG 
category: articles #howto
tags: 
- Mutt
- XTEC
- email
- gmail

---
<div style="text-align:center" markdown="1">

![Mutt](data:image/png;base64,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)

</div>
<div style="text-align:justify" markdown="1">

**Mutt** és un client de correu en mode text potent i lleuger alhora, cosa que és molt d'agrair per accedir a comptes de correu a través d'IMAP (com ara *gmail*). Per la xarxa es poden trobar diverses guies de configuració dels comptes de *gmail* amb *Mutt*. Fa tres anys em vaig veure incapaç de fer funcionar el correu XTEC amb Mutt. Donat que els comptes XTEC funcionen a través de *gmail* sembla que no hi hauria d'haver cap problema. El cas és que, amb les darreres modificacions del [portal XTEC](http://xtec.gencat.cat/ca/),
es fa treballós arribar a llegir els correus i s'agraeix l'accés a una via ràpida i lleugera com la que ofereix **Mutt**.

<!-- more -->

Per poder usar el correu XTEC des de **Mutt** és convenient, per ser ordenat, de crear la configuració d'usuari en un fitxer apart que desarem en el directori ocult amb el nom `~/.mutt/usuari_XTEC`; així, en cas que alguna cosa ens falli, ens serà més fàcil trobar l'error i arreglar-ho. El contigut d'aquest fitxer ha de ser com segueix:

{% highlight Bash shell scripts%}

set from = "usuari@xtec.cat"
set realname = "Nom real de l'usuari"
set imap_user = "usuari@xtec.cat"
set imap_password = "contrasenya usuari XTEC" #No és necessari; si no es posa, la demanarà en entrar a Mutt
set folder = "imaps://imap.gmail.com:993"
set spoolfile = "+INBOX"
set postponed = "+[Gmail]/Esborranys"
set record = "+[Gmail]/Enviats"
set trash = "imaps://imap.gmail.com/[Gmail]/Paperera"
set header_cache =~/.mutt/cache/headers
set message_cachedir =~/.mutt/cache/bodies
set certificate_file =~/.mutt/certificates
set smtp_url = "smtp://usuari@xtec.cat@smtp.gmail.com:587/"
bind editor <space> noop
macro index gi "<change-folder>=INBOX<enter>" "Go to inbox"
#macro index ga "<change-folder>=[Gmail]/All Mail<enter>" "Go to all mail"
macro index gs "<change-folder>=[Gmail]/Enviats<enter>" "Vés a Enviats"
macro index ge "<change-folder>=[Gmail]/Esborranys<enter>" "Vés a Esborranys"
macro index gp "<change-folder>=[Gmail]/Paperera<enter>" "Vés a Paperera"
set move = no  #Deixar de demanar "moure missatges llegits a mbox"!
set imap_keepalive = 900

{% endhighlight %}

Cal encara editar el fitxer `~/.muttrc` com segueix:

{% highlight Bash shell scripts%}

source ~/.mutt/usuari_XTEC

{% endhighlight %}

A partir d'aquí podem fer altres canvis, per exemple, canviar l'editor per defecte (**vi**) per **nano**, de més fàcil ús. Ho fem editant el fitxer  `~/.muttrc`:

{% highlight Bash shell scripts%}

source ~/.mutt/usuari_XTEC
set editor=nano

{% endhighlight %}

Amb això accedirem bé als correus que rebem en mode text, però els correus *html* ens seran il·legibles si no connectem **Mutt** amb un navegador html. Com que es tracta de tenir un sistema lleuger, el connectarem a un navegador en mode text, que ens permetrà fer una primera lectura dels correus i, si cal, ja hi tornarem amb un lector més *pesat* o bé a través de *[La meva XTEC](https://accounts.google.com/ServiceLogin?continue=https%3A%2F%2Fsites.google.com%2Fa%2Fxtec.cat%2Faplicacionsxtec%2F&service=jotspot&sacu=1&hd=xtec.cat)*. He triat per a aquesta tasca **elinks**, per fer-ho, cal crear (o afegir-hi si ja el tenim) el fitxer `~/.mutt/mailcap` amb el contingut següent

{% highlight Bash shell scripts%}

text/html; elinks %s; nametemplate=%s.html
text/html; elinks -no-numbering -no-references -no-home -dump-charset %{charset} -dump %s; nametemplate=%s.html; copiousoutput 

{% endhighlight %}

I tornar a `~/.muttrc` per completar-lo com veiem a continuació:

{% highlight Bash shell scripts%}

source ~/.mutt/usuari_XTEC
set editor=nano
auto_view text/html

{% endhighlight %}

**Mutt** és molt més versàtil i ens permet el seu ús amb múltiples comptes de correu, però això serà tema d'un altre article.

</div>