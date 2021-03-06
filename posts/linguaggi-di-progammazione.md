---
title: Linguaggi di Progammazione (Proprietà e Funzionalità di base)
date: 2022-03-31T08:31:09.343Z
author: Agostino Cesarano
summary: Appunti per il corso di LP, Professore Bonatti; prima parte, di
  introduzione ai linguaggi di programmazione, con introduzione a quelle che
  sono le principali proprietà e funzionalità presenti in essi.
tags:
  - LP
---
**Terminologia**

> **Linguaggio di programmazione:** è un linguaggio che è usato
> per esprimere (mediante un programma) un processo con il quale
> un processore può risolvere un problema.
>
> **Processore:** e la macchina che eseguirà il processo descritto dal
> programma; non si deve intendere come un singolo oggetto, ma
> come una architettura di elaborazione.
>
> **Programma:** è l’espressione codificata di un processo.

**Come vedere se un linguaggio è Completo?**

I linguaggi di programmazione *computazionalmente completi*, sono quelli che possono
programmare qualunque funzione calcolabile.

1. Un linguaggio di programmazione è completo se può simulare una macchina di Turing.
2. Sono completi solo quelli che riescono ad esprimere anche programmi di cui non è decidibile la terminazione.

**Macchine Astratte**

Una macchina astratta per un linguaggio di Programmazione è un insieme di strutture di dati e algoritmi che permettono di memorizzare programmi scritti in quel linguaggio.

> Quando traduciamo il linguaggio di programmazione non lo traduciamo su una **macchina hardware** ma su una macchina di livello superiore.

Ad esempio Java utilizza una macchina astratta JVM che traduce tramite Software il codice da tradurre.

*Compilazione per macchina intermedia.*

> **Interpreti:** traducono ed eseguono un costrutto alla volta.

**PRO**: debug - fase di sviluppo: interazione più snella.

> Compilatori: prima traducono l’intero programma; poi la
> traduzione può essere eseguita (anche più volte).

**PRO**: velocita di esecuzione finale - fase di rilascio.

**PRO**: più controlli e in anticipo

Interprete nella compilazione per macchina intermedia è detta **Supporto Run Time (SRT)**

*L'SRT* ha funzionalità aggiuntive

*Funzioni di basso livello / interfacce col S.O. ;* 

ad es. funzioni di I/O.

*Gestione della memoria;* 

garbage collector; gestione dell’heap; gestione dello stack.

##### Proprietà dei linguaggi

> Semplicità

*( concisione ) vs ( leggibilità )*

*Semantica:* minimo numero di concetti e strutture.

*Sintattica:* unica rappresentazione di ogni concetto.

> Astrazione

*Dati:* nasconde i dettagli dei vari oggetti.

*Procedure:* facilitare la modularità del progetto.

> Espressività

*( facilità di rappresentazione di oggetti ) vs (semplicità)*

> Ortoganità

meno eccezioni alle regole del linguaggio.

> Portabilità

**Criterio di scelta del linguaggio**

* Disponibilità dei traduttori
* Maggiore conoscenza da parte del programmatore
* Esistenza di standard di portabilità
* Comodità dell’ambiente di programmazione
* Sintassi aderente al problema
* Semantica aderente alla architettura fisica?
  *con le moderne tecniche di implementazione dei linguaggi non è più un criterio stringente*

**Paradigmi computazionali**

> *Programmi di tipo ( iterativo )*
>
> **Imperativo:** Un programma specifica sequenze di modifiche da apportare allo stato della macchina (memoria).
>
> *Programmi di tipo ( ricorsivo )*
>
> **Funzionale:** Il programma e le sue componenti sono funzioni. Esecuzione come valutazione di funzioni.
>
> **Logico:** Programma come descrizione logica di un problema. Esecuzione analoga a processi di dimostrazione di teoremi. 
>
> **Orientato ad oggetti:** Programma costituito da oggetti che scambiano messaggi.
>
> **Parallelo:** Programmi che descrivono entità distribuite che sono eseguite contemporaneamente ed in modo asincrono.

*I linguaggi di programmazione moderni permettono di usare più paradigmi in base alle nostre esigenze.*

*Esempio:*

*Vogliamo scrivere in un linguaggio imperativo, funzionale e logico la funzione* **membro(X,L)** *che decida se l’elemento X appartiene alla lista L.*

*Useremo tre funzioni* 

* empty() restituisce **true** se la lista è vuota.
* testa() restituisce il valore di testa.
* coda() restituisce la coda tagliando il valore di testa.

*In pseudo codice, paradigma imperativo.*

```
procedure membro (X,L)
local L1 = L
while not vuota (L1) and not X= testa (L1)
do L1 = coda (L1)
return not vuota (L1)
```

*In C ( linguaggio di tipo imperativo )*

```c
bool member (X,L) {
List L1 = L;
while ( ! empty (L1) && ! X= testa (L1 ))
L1 = coda (L1 );
return (! empty (L1 ));
}
```

*pseudo codice ( paradigma funzionale )*

```lisp
function member (X,L)
if vuota (L) then false
else if X == testa (L) then true
else member (X, coda (L))
```

*In LISP ( linguaggio di tipo funzionale )*

```lisp
( defun membro (x l)
( cond (( null l) nil )
(( equal x ( first l)) T)
(T ( membro x ( rest l )))))
```

*C si potrebbe usare in stile funzionale se evitassimo di usare i costrutti imperativi:*

```ags
bool member (X,L) {
return ( vuota (L)) ? false :
(X == testa (L ))? true :
member (X, coda (L)) }
```

*In Prolog ( linguaggio di tipo Logico, paradigma logico )*

```
membro (X, [X|L]).
membro (X, [Y|L]) :- membro (X, L).
```

##### Memoria

*Consiste in un insieme di “contenitori di dati”.*

Ad es. parole (o celle) della memoria centrale.

Tipicamente rappresentate dal loro indirizzo associati ai valori in essi contenuti, i valori delle variabili.

Dunque (concettualmente) la memoria è:

* Una funzione da uno spazio di locazioni ad uno spazio di valori
* mem(loc) = “valore contenuto in loc”

> **mem(loc)** *\= locazione di memoria  --> valore*

**Assegnazioni**

Definizione grammaticale (sintassi):

```pascal
<name > <assignment - operator > <expression >

//Esempio in Pascal:
a := b + c;
```

*<name>* rappresenta la locazione dove viene posto il risultato.
*<expression>*sono specificati una computazione (espressione matematica) e i riferimenti ai valori necessari alla computazione.

**Modello Imperativo**

I programmi sono descrizioni di sequenze di modifiche della “memoria” del calcolatore.

Ogni unità di esecuzione consiste di 4 passi:

1. ottenere indirizzi delle locazioni di operandi e risultato;
2. ottenere dati di operandi da locazioni di operandi;
3. valutare risultato;
4. memorizzare risultato in locazione risultato.

In sostanza un assegnamento!

Il modello imperativo usa dei nomi come astrazione di indirizzi di locazioni di memoria **(variabili)**.

Quindi l'ambiente di esecuzione *(environment)* comprende:

Un insieme di nomi di variabili e parametri, non indirizzi di memoria ma identificatori.

Quindi l'ambiente di esecuzione associato ad un modello imperativo è una funzione, identificata come **env(id)** che dato un certo identificatore, per lo più variabili, ci restituisce la locazione di memoria identificata con quel nome.

> **env(id)** = identificatore --> locazione

A sua volta le funzioni *env* sono associate a funzioni *mem* che restituiscono i valori delle locazioni.

Il **valore di una variabile x è**:

>  mem( env ( x ))

Nel **paradigma funzionale**, non esiste la funzione *mem* e la funzione *env* associa direttamente gli identificatori al contenuto della memoria.

Nel paradigma imperativo la funzione *env* identifica una associazione immutabile (la locazione di memoria associata a un nome non cambia);

*Esempi di esercizi, può uscire all'esame!*

**\*(x+1)**=... **\-->** mem( env( x )) + 1

A destra si aggiunge un **mem** davanti.

...=**\*(x+1)** **\-->** **mem**( mem( env( x ) + 1)

...=**\*(x+y) --> mem**( mem( env(x) ) + mem( env(y) ))

> **Sempre SBAGLIATI!**
>
> env ( mem (...) )
>
> env ( x +1 )

**v\[ i ]** vettore di dimensione i = **\*(v+i) -->** mem( env(v) + mem( env(i))

**p\[ i ]** puntatore di dimensione i = **\*(p+i) -->** mem( mem( env(p) + mem( env(i))

Il puntatore è gestito come una locazione di memoria mentre il vettore no.

Quando c'è una & si toglie un mem, ad esempio.

v\[ 3 ] = &v\[ 3 ] **\-->** env( v ) + 3 = env ( v ) +3

**NO** v\[ 3 ] **\-->** **mem(** env ( v ) +3 **)**

**NO** &v\[ 3 ] **\--> mem(** env ( v ) +3 **) oppure env(mem(env**... **GRAVE! mai fare.**

Perché il vettore non viene visto come una variabile?

es. v\[ 3 ] = 1 indica dove scrivere "1" quindi quello che mi interessa è il solo indirizzo di quella casella del vettore.

p\[ 3 ] = &p\[ 3 ] **\-->** mem( env (p) +3 ) = mem( env ( p ) + 3 )

**NO mem(**mem( env ( p ) + 3 )**)**

&x = ... non c'è un mem da togliere **ERRORE non è un  l-value**

> **l-value** oggetto che occupa una posizione identificabile in memoria ( cioè ha un indirizzo ).
>
> **r-value** sono i restanti oggetti che non hanno un indirizzo.

##### Legame di tipo

Per definizione è correlato al legame di valore (ad es. il tipo di una variabile e il tipo del suo valore devono corrispondere).

Ogni volta che il legame di valore viene modificato, occorrerebbe controllare (**type checking**) la consistenza con il legame di tipo.

> Un linguaggio si dice **dinamicamente tipizzato** se il controllo del legame di tipo e di conseguenza anche il controllo di consistenza avviene durante l’esecuzione.

*Esempio: nei linguaggi di scripting e Python*

```python
x = 1; 
...
x= " abc ";
```

Inizialmente il tipo di x è un numerico, successivamente diventa un tipo stringa.

1. Gli identificativi non vengono dichiarati.
2. Gli assegnamenti determinano il tipo dell'identificatore.

Il tipo della variabile dipende dal valore che gli assegniamo, *avviene un type checking al cambio di valore.*

> Un linguaggio è **staticamente tipizzato** se il legame avviene durante la compilazione; in questo caso il controllo di consistenza può avvenire in entrambe le fasi.

##### Type checking

È il meccanismo di controllo di consistenza della coppia dei legami valore-tipo.

*Può avvenire:* 

1. durante la compilazione
2. durante l’esecuzione
3. per nulla

> Un linguaggio è **fortemente tipizzato** se il controllo di consistenza avviene sempre.

*Esempio di linguaggi fortemente tipizzati*

* Java è fortemente tipizzato.
* Pascal è quasi fortemente tipizzato (una sola eccezione di assenza di controllo: i record con varianti).

> Un linguaggio e **debolmente tipizzato** se il controllo di consistenza può non avvenire affatto in numerosi casi.

*Esempio di linguaggi debolmente tipizzati*

* C è debolmente tipizzato:
  in esso esistono le operazioni di casting, che consentono di forzare, in esecuzione, l’interpretazione di un qualunque valore secondo un qualunque tipo (anche un tipo diverso da quello a cui il valore è stato precedentemente associato);
  esistono puntatori a void, che godono, in esecuzione, di conversione di tipo implicita verso qualunque altro tipo puntatore;
  esistono le unioni, che sovrappongono la locazione di variabili di tipo diverso, senza controllare se il valore corrisponde al tipo con cui viene usato.

I linguaggi staticamente e fortemente tipizzati sono i più “forti” tra i fortemente tipizzati.

Quindi la strategia per i linguaggi **fortemente e staticamente tipati** è fare quanti più controlli possibile a tempo di compilazione ed eseguire i rimanenti a tempo di esecuzione perché prima si scoprono gli errori e più il testing diventa economico.

##### Blocchi di istruzioni

Le istruzioni nei linguaggi di programmazione moderni sono definiti in blocchi, questo è necessario per distinguere le varie componenti del codice ed assegnargli un nome.

Definiamo un piccolo pseudo-linguaggio per rappresentare un blocco:

```
...
BLOCK A;
  DECLARE I;
BEGIN A
  ... {I DEL BLOCCO A}
END A;
...
```

**Scoping**

In ambito **statico o lessicale.**

Blocchi annidati *vedono e usano i legami dei blocchi più esterni* (legami non locali) e, di solito, possono aggiungere legami locali o sovrapporne di nuovi.

In ambito **dinamico.**

Concetto qui esaminato solo in relazione ai blocchi annidati, ma che assume il proprio senso maggiore quando vi sono procedure chiamanti e chiamate. In questo caso *la procedura* *chiamata vede e usa i legami visti e usati dalla procedura chiamante.*

*Esempio Scoping Statico*

```
PROGRAM P;
  DECLARE X;
BEGIN P
... {X da P}
  BLOCK A;
    DECLARE Y;
  BEGIN A
    ... {X da P, Y da A}
    BLOCK B;
      DECLARE Z;
    BEGIN B
      ... {X da P, Y da A, Z da B}
    END B;
      ... {X da P, Y da A}
  END A;
    ... {X da P}
     BLOCK C;
       DECLARE Z;
     START C
        ... {X da P, Z da C}
     END C;
... {X da P}
END P;
```

Ogni blocco vede le variabili dichiarate dai blocchi più esterni è nel caso in cui è dichiarata una variabile locale con lo stesso identificativo, la variabile globale sarà sovrapposta con quella locale.

**Mascheramento**

Il processo descritto precedentemente è detto mascheramento.

*Esempio di Mascheramento*

```
PROGRAM P;
DECLARE X,Y;
BEGIN P
... {X e Y da P}
  BLOCK A;
    DECLARE X,Z;
  BEGIN A
  ... {X e Z da A, Y da P}
  END A;
... {X e Y da P}
END P;
```

**Allocazione statica della memoria**

Si dice allocazione statica di memoria (load-time) quando le variabili conservano il proprio valore ogni volta che si rientra in un blocco (il legame di locazione è fissato e costante al tempo di caricamento).

**Allocazione dinamica della memoria**

Si dice allocazione dinamica di memoria (run-time) quando il legame di locazione (e anche di nome) è creato all’inizio dell’esecuzione di un blocco e viene rilasciato a fine esecuzione.

##### Stack di attivazione

In ogni momento dell’esecuzione lo stack di attivazione contiene i record “attivi”:

1. il top dello stack contiene sempre il record del blocco correntemente in esecuzione;
2. ogni volta che si entra in un blocco, il record di attivazione del blocco viene posto sullo stack (push);
3. ogni volta che si esce da un blocco, viene eliminato il record al top dello stack (pop).

##### Procedure

Procedure sono astrazioni di parti di programma in unita di esecuzione più piccole, che consentono il loro (ri-)uso.

**Vantaggi:**

* Programmi più semplici da scrivere, leggere o modificare;
* suddivisione dei compiti in più programmi;
* progettazione top-down ( un algoritmo complesso viene suddiviso in unità più piccole );
* Riusabilità dei programmi; riduzione errori.

**Astrazione procedurale** la rappresentazione di una unità di esecuzione attraverso un’altra unita più semplice.

Ogni volta che una procedura viene invocata il suo **record di attivazione** viene aggiunto al cosiddetto **stack di esecuzione**.

Sul top dello stack c'è sempre il record relativo alla procedura correntemente in esecuzione.

Alla terminazione della procedura, il record di attivazione viene rimosso dallo stack.

**Record di attivazione**

Include:

1. Tutte le variabili dichiarate localmente.
2. Puntatore alla prossima istruzione (permette di riprendere l’esecuzione quando il controllo viene restituito alla procedura chiamante).
3. Memoria temporanea necessaria alla valutazione delle espressioni contenute nella procedura.

**Propagazione dei data object**

Viene realizzata aggiungendo al record di attivazione un puntatore al record di attivazione della procedura da cui vengono propagate le definizioni o i dati.

Se viene richiesto l’accesso ad un dato che non è definito localmente, esso viene ricercato in modo ricorsivo nei record di attivazione precedenti.

Tre tipologie di realizzazione della propagazione.

1. *Propagazione in ambito statico.* In questo caso la procedura è propagata dal programma che la contiene.
2. *Propagazione in ambito dinamico.* In questo caso la procedura è propagata dal programma chiamante.
3. *Nessuna propagazione.* L’uso di ambienti non locali è scoraggiato perché produce effetti collaterali non facilmente prevedibili.

*Esempio di propagazione in ambito statico*

```
program p;
  var a, b, c: integer ;
  
  procedure q;
    var a, c; integer ;
    
    procedure r;
      var a: integer ;
    begin {r}                  {variabili : a da r; b da p; c da q;
      ...                      procedure : q da p; r da q}
    end ; {r}
    
  begin {q}                    {variabili : a da q; b da p; c da q;
      ...                      procedure : q ed s da p; r da q}
  end ; {q}
  
  procedure s;
  var b: integer ;
  begin {s}                    {variabili : a da p; b da s; c da p;
      ...                      procedure : q ed s da p}
  end ; {s}
  
begin {p}                      {variabili : a, b, c da p;
   ...                         procedure : q, s da p}
end ; {p}
```

**Propagazione in ambito statico**

Supponendo una sequenza di attivazione (p, s, q, q, r), lo stack di esecuzione ha questa forma:

![Propagazione in ambito statico](/static/img/propagazione-statica.jpg "Propagazione in ambito statico")

**Propagazione in ambito dinamico**

La stessa sequenza di attivazione precedente (p, s, q, q, r), genera allora lo stack di esecuzione:

![Propagazione in ambito dinamico](/static/img/propagazione-dinamica.jpg "Propagazione in ambito dinamico")

Nella propagazione in ambito dinamico è praticamente impossibile determinare chi andrà a chiamare quella procedura durante la scrittura del codice sorgente.

##### Parametrizzazione di procedure

Sono il mezzo per il quale le informazioni transitano tra l’unita chiamante e quella chiamata.

Possiamo distinguere:

1. parametri di **IN (input):** sono passati dalla unità chiamante alla unità chiamata al momento dell’invocazione;
2. parametri di **OUT (output):** sono passati dall’unità chiamata alla unità chiamante al momento della terminazione della prima;
3. parametri **IN-OUT (input-output):** servono a far transitare le informazioni in entrambe le direzioni.

Devono essere specificati in due punti:

* nella definizione della procedura: *parametri formali;*
* nelle invocazioni della procedura: *parametri attuali.*

**Associazione dei parametri**

*Regola comune:* nella definizione deve essere specificato il *tipo* dei parametri formali; nella invocazione è richiesta la corrispondenza di tipo tra parametri formali e attuali.

*Eccezioni:* lasciare i parametri formali senza alcun legame di tipo; il legame si instaura durante l’esecuzione (*run time*) allo stesso tipo dei parametri attuali (*impossibile il type checking in compilazione*).

**Metodi di associazione:**

1. *per posizione:* a seconda della posizione relativa nella sequenza dei parametri;
2. *per nome:* il nome del parametro formale è aggiunto come prefisso al parametro attuale;

*Esempio*

ADA permette di associare i parametri delle funzioni sia per posizione che per nome.

Data la seguente procedure dichiarata in (ADA):

```
procedure TEST (A: in Atype ; b: in out Btype ; C: out Ctype )
```

allora una invocazione che usi *associazione per posizione* è:

```
TEST (X, Y, Z);
```

I **parametri attuali** sono inseriti nell'ordine di dichiarazione.

Mentre un invocazione che usi *associazione per nome* può essere:

```
TEST (A=>X, C=>Z, b=>Y);
```

I parametri non rispettano l'ordine di dichiarazione, la definizione dei **parametri attuali** viene fatta tramite nome.

Una ulteriore tecnica è la cosiddetta *associazione di default*.

Introdotta dal Lisp è successivamente implementato in molti linguaggi, essa permette di specificare valori di default ai parametri formali che non sono stati legati a valori da parametri attuali.

**Parametri di IN (input)**

Possono essere realizzati in due modi:

* *con un riferimento*; in questo caso la locazione del parametro attuale diventa la locazione del parametro formale;

  poiché il parametro formale è di tipo IN, allora si deve impedire la modifica all’interno della procedura; il parametro formale non può essere a sinistra di un assegnazione.
* *con una copia*; in questo caso in una nuova locazione, quella del parametro formale, viene copiato il valore del parametro attuale; parametro formale visto come variabile locale;

  modifica permessa, perché valida solo nell’ambiente di esecuzione della procedura.

Il secondo modo è meno efficiente del primo, sia rispetto allo spazio sia al tempo, ma è più flessibile e richiede meno variabili locali.

Se passo il parametro attuale tramite riferimento, la funzione env() del parametro formale e attuale sono uguali, "aliasing".

In C/C++ il passaggio dei parametri attuali di IN viene fatto tramite copia.

In Pascal se c'è var prima del parametro formale, il passaggio è fatto per riferimento.

**Parametri di OUT (output)**

Possono essere realizzati:

* con un riferimento;
* con una copia;

  Rappresentano risultati -> alcuni linguaggi assumono che i parametri
  OUT non siano inizializzati e ne proibiscono la “lettura”, ad es.

  * uso a destra di un assegnamento
  * passaggio a un parametro IN o IN OUT di un’altra procedura

Non esistono regole generali nemmeno tra diverse versioni di uno stesso linguaggio, ad es.

* Ada 83 proibisce di “leggere” i parametri OUT 
* Le versioni successive invece lo permettono

Altri linguaggi non hanno parametri di tipo OUT multipli, se devo restituire più elementi, restituisco un "oggetto".

**Parametri di IN OUT (input) e (output)**

Sono la combinazione dei due precedenti. Anch’essi possono essere realizzati:

* con un riferimento; non ci sono limitazioni all’uso all’interno della procedura;
* con una copia; avvengono due processi di copia, uno durante l’attivazione ed uno durante la terminazione della procedura.

Non tutti i linguaggi hanno parametri di input e output, i parametri di input/output non hanno vincoli  di non "lettura" dei parametri di OUT e vincoli di non "modifica" dei parametri IN.

**Aliasing**

È la possibilità di riferirsi alla stessa locazione con nomi diversi.

Nel passaggio dei parametri può causare notevoli problemi di interpretazione. Per esempio:

```pascal
program MAIN ;
  var
    A: integer ;
  procedure TEST ( var X, Y: integer );
  begin
    X:= A + Y;
    writeln (A, X, Y)
  end ;
begin
  A:= 1;
  TEST (A, A)
end .
```

Pascal ha scoping statico, quindi la procedure vede le variabili locali dei blocchi più esterni.

In questo caso tutte le variabili valgono due, effettuando un passaggio per riferimento, le variabili che passo alla procedure sono le stesse, cioè l'env() dei parametri attuali e della variabile locale A sono uguali, questo può portare a **risultati indesiderati.**

**Procedure come parametri di procedura**

Alcuni linguaggi permettono l’uso di procedure come argomento di altre procedure.

**Macro**

Procedure in cui i nomi dei parametri attuali sostituiscono i nomi dei parametri formali.

Esempio: data la macro

```pascal
procedure swap (a, b: integer );
var temp : integer ;
begin
temp := a;
a:= b;
b:= temp
end ;
```

La differenza tecnica, è che la macro non ha bisogno di un record di attivazione, allora la chiamata swap(x, y) esegue il seguente brano di codice, la procedure non viene eseguita nel record, ma localmente:

**Funzioni**

Sono procedure che restituiscono un valore alla procedura chiamante.

Sono realizzate:

* o creando una pseudovariabile nell’ambiente locale della procedura chiamata, che verrà restituita al termine della funzione. 

  Tale variabile può essere solo modificata; non è possibile l’accesso in lettura.
* o utilizzando una istruzione di return per restituire esplicitamente il valore di una espressione.