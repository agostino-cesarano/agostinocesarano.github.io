---
title: Sistemi Informativi Multimediali (Indicizzazione e Recupero)
date: 2022-06-03T13:49:12.572Z
author: Agostino Cesarano
summary: Appunti per il corso di SIM, Professore Balzano; seconda parte,
  Indicizzazione e Recupero dei Dati.
tags:
  - SIM
---
##### Indicizzazione e Recupero

**Differenze tra DBMS e IR**

**DBMS**

Struttura omogenea dei record, i componenti del record sono per lo più gli attributi.

Un record è definito completamente ed univocamente dai propri attributi.

> Retrieval con match esatto.

**IR**

* Records non strutturati
* Attributi non prefissati

Indicizzazione del documento, recupero di keywords.

> Retrieval con match approssimato o parziale.

**Processo base del Document Retrieval**

Il processo di Document Retrieval si divide in due fasi:

* Online
* Offline

![Retrieval dei Documenti](/static/img/retrieval.png "Retrieval dei Documenti")

**Retrieval Off-Line**

Riceve dei Documenti è li processa in modo da estrarre le caratteristiche fondamentali.

**Retrieval On-Line**

Riceve una Query, analizza quelle che sono le informazioni da ricercare.

Successivamente confronta le informazioni da cercare con le caratteristiche dei dati precedentemente processati nella parte Off-Line dell' processo di ricerca.

Una volta trovati i documenti che abbiano caratteristiche simili a quelli ricercate, vengono mostrate all'utente che può:

* Raffinare la sua ricerca.
* Fornire un feedback sui documenti visualizzati ( Caratteristica non sempre presente in tutti gli IR).

**Problema?**

Come memorizzo le caratteristiche pre-processate?

##### Inverted Files

L’inverted file contiene un insieme di record che contengono:

* il termine che si vuole cercare
* una sequenza di puntatori a documenti e/o records che contengono quel termine

La ricerca può essere effettuata tramite Operatori Booleani OR AND NOT

Query con composizione booleana delle chiavi di ricerca

*Esempio:* termine_1 ANT NOT termine_2

> Il processo di ricerca è più efficiente rispetto al **flat‐file** non si analizzano i documenti interi ma solo l’inverted file da cui si ricavano i collegamenti ai documenti che soddisfano la query.

![Inverted File](/static/img/inverted-file.png "Inverted File")

**Inverted File con operazioni estese**

È possibile raffinare la ricerca tenendo conto di:

* Differenza di importanza tra un termine e un altro.
* Posizione in cui un termine compare.
* La frequenza in cui un termine compare all’interno di un documento.

Definiamo 2 nuovi operatori di «prossimità» quali “**WITHIN SENTENCE**” e “**ADJACENT**”

> *WITHIN SENTENCE* i termini ricercati sono presenti nello stesso paragrafo del record recuperato.
>
> A*DJACENT* termini ricercati confinanti nel record recuperato.

##### Indicizzazione automatica del testo

Il processo di indicizzazione del file di testo prevede diverse fasi; lo scopo principale è quello di filtrare il testo in modo da mantenere solo le informazioni da considerare per le ricerche.

![Indicizzazione automatica testo](/static/img/indicizzazione-testo.png "Indicizzazione automatica testo")

Fasi di filtraggio:

1. **Stop Words**, si escludono elementi insignificanti per la ricerca come “articoli”, preposizioni”,…
2. **Stemming**, se nel testo compare più volte parole analoghe, per la ricerca si considera solo il
   termine comune delle parole analoghe. *Esempio:* se nel testo sono presenti i termini
   “pescare”, “pescatore”, “pesce” allora considero solo il loro prefisso comune, cioè “pesc”.
   Anche se tale operazione rende il file più compatto, d’altro canto occorre considerare che,
   per esempio, a causa della brevità del termine comune esso non sia più molto significativo.
3. **Thesaurus**, possibilità di sostituire diversi termini simili che compaiono nel testo con un
   unico termine (usando un vocabolario). Esempio: se nel testo sono presenti i termini
   “lavare”, “pulire”, “detergere” allora potrei considerare solo il termine “lavare”.
4. **Weighting,** I termini che compaiono nel testo hanno diversa importanza; la loro importanza
   può essere ricavata valutando le loro frequenze di occorrenza ed il risultato della ricerca
   viene mostrato in ordine di frequenza.

**Calcolo dei pesi**

Il peso di un termine deve considerare il numero di volte in cui il termine compare sia nel documento sia nell’insieme complessivo dei documenti.

La formula comunemente utilizzata per il calcolo dei pesi è:

> W = f * log (N/dfj)

In cui:

* W = peso del termine j nel documento i
* f = frequenza del termine j nel documento i
* N = numero totale dei documenti del DataBase
* dfj = numero dei documenti del DataBase che contengono il termine j

##### Retrival con modello vettoriale