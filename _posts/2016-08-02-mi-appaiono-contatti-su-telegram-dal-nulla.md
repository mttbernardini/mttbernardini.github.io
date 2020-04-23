---
title: Mi appaiono contatti su Telegram dal nulla?
---

# Mi appaiono contatti su Telegram dal nulla?

«Giovanni si è unito a Telegram»
Ma chi è Giovanni? Non è nei miei contatti, è comparso dal nulla.

È successo una volta, poi due, poi tre... poi ho iniziato a preoccuparmi. Alla fine ho chiesto anche allo staff e ho iniziato a fare vari test ed esperimenti, poi fortunatamente ho capito!

## Il meccanismo

Telegram ha una sua rubrica interna divisa in questo modo:

*   [A] Contatti registrati. Serve per aprire nuove chat.
*   [B] Contatti in attesa di registrazione. Serve per notificare l’utente quando un nuovo contatto si registra. (vengono memorizzati nome, cognome e numero, nient’altro)

Come viene gestita questa doppia lista? A seconda del dispositivo (e dei permessi), [A] viene sincronizzata con la rubrica dello stesso (iOS) oppure affiancata (Android), ad ogni modo agisce una _sincronizzazione completa_: i nuovi contatti aggiunti tramite la rubrica del dispositivo, se sono registrati su telegram, vengono aggiunti ad [A]; viceversa, i contatti che vengono aggiunti tramite telegram stesso (tramite “crea contatto”, ma anche i contatti appena registrati che provengono da [B]) vengono inseriti nella rubrica del dispositivo (a volte capita che mi si creino contatti duplicati). Stessa sincronizzazione avviene quando viene eliminato un contatto (sia che venga eliminato dalla rubrica del device che dalla lista [A] di Telegram).

Se per [A] abbiamo quindi totale accesso, sia se la rubrica viene sincronizzata che tramite l’interfaccia dell’app (ad esempio dove non c’è nessuna rubrica da sincronizzare, tipo telegram desktop), non si può dire la stessa cosa per [B]. Questa subisce una _sincronizzazione unidirezionale passiva_, ossia i contatti del dispositivo che non sono registrati vengono inseriti in [B] e non il viceversa (per fortuna), ma non c’è **nessun modo per eliminarli**. Inoltre nell’interfaccia dell’app la lista [B] non è visibile, pertanto non si ha proprio modo di sapere quali contatti siano finiti lì dentro :\
[[MORE]]

## Dimostrazione

_TL;DR: basta vedere l’ultima immagine con la conferma da parte dello staff. Oppure saltate direttamente a “Dove voglio arrivare”._

Innanzi tutto ho creato un contatto fittizio con un numero a cui ho accesso:

![](https://68.media.tumblr.com/e74040f4116c055cf73760c84def7199/tumblr_inline_obaf43x76l1rc5rnw_540.png)

Il numero non è registrato a telegram, appare quindi tra i contatti che si possono invitare. Notare che questa lista non corrisponde esattamente a [B], ma rappresenta semplicemente i contatti non registrati che sono **anche** nella rubrica del device (i.e. non appaiono altri contatti collezionati precedentemente in [B]):

![](https://68.media.tumblr.com/984febf65ea96e3c4ac54b92b71e9226/tumblr_inline_obaf9i36mJ1rc5rnw_540.png)

Dopodiché ho eliminato il contatto e tolto a Telegram l’accesso ai contatti (a dimostrazione che i permessi non influenzano in alcun modo la lista [B]). A quel punto ho registrato il numero su Telegram da un altro client:

![](https://68.media.tumblr.com/b86e143595cb48d08d688755f9481c06/tumblr_inline_obafdqDwXb1rc5rnw_540.png)

Ora osservate attentamente, il nome che ho scelto alla registrazione è “Someone’s Test”, ma il contatto sull’iPad è stato salvato (e memorizzato in [B]) come “Someone”, non a caso all’atto della registrazione è il nome che è apparso:

![](https://68.media.tumblr.com/541e4e690d4f62291ff083c1856cc563/tumblr_inline_obafgaAprZ1rc5rnw_540.png)

Ora poiché Telegram non ha accesso ai contatti dell’iPad non ne può creare nuovi, ma se avesse avuto l’accesso avrebbe prontamente (ri)creato in rubrica il contatto “Someone” con relativo numero (dato che ora non è più in [B] ma in [A]).

In maniera più o meno involontaria avevo già fatto questo esperimento e ho avuto una conferma dallo staff stesso:

![](https://68.media.tumblr.com/f686724c486f5af1c3920ac835e28456/tumblr_inline_obafuwpi041rc5rnw_540.png)

## Dove voglio arrivare

Grazie a questo esperimento ho capito il collegamento con i “contatti apparsi dal nulla”. Fondamentalmente deve essere successo che un giorno sono entrato a Telegram dal cellulare di un amico e quindi si sono mescolati i contatti, ma **non** avendo accesso a [B] non me ne potevo rendere conto se non quando questi, piano piano, si registravano su Telegram e passavano così su [A], che invece è visibile da qualsiasi app.

È qualcosa di grave? Assolutamente no. È un problema di privacy? Forse, ma non così drastico come credevo inizialmente. Però è indubbiamente fastidioso e lo riterrei un bug, del tutto risolvibile, quindi vorrei proporre delle...

## Soluzioni

La prima, la più banale, è quella di rendere possibile l’accesso a [B]. Forse non è la soluzione ottimale per l’utente comune, ma almeno permetterebbe una **gestione manuale** di tutti i contatti a cui Telegram ha accesso.

La seconda, più effettiva, ma non risolverebbe del tutto il problema, è quella di **notificare** l’utente ogni volta che si collega su un device che permette la sincronizzazione dei contatti, per evitare (come nel mio caso) che si colleghi su quello di un amico e si ritrovi i contatti mescolati (tra l’altro danneggiando anche i suoi). Ad ogni modo questa potrebbe essere una feature distinta implementabile.

La terza è forse la più versatile e invisibile per l’utente, ma la più macchinosa da implementare. Sarebbe quella di effettuare una sincronizzazione unidirezionale in [B] ma **attiva**, in modo che rispecchi sempre i contatti accessibili da qualsiasi sessione attiva di telegram, così che vengano “dimenticati” automaticamente eventuali contatti acquisiti da sessioni non più attive.

L’ultima che mi viene in mente, infine, è manuale, pragmatica e **drastica**, ma indubbiamente semplice da implementare: un bottone _“cancella i contatti collezionati da telegram”_.

Spero di non essere stato troppo prolisso, fatemi sapere se avete avuto esperienze simili o se pensate che sia comunque un argomento valido per migliorare Telegram ;)
