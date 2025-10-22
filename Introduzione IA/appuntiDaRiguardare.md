# Intelligenza Artificiale Teoria

## Agenti Intelligenti

**Definizione:** <br>
Un agente è qualsiasi cosa che può percepire l'ambiente circostante tramite sensori e agire su di esso tramite attuatori.

![Agente](./imgs/agente.png)

Le azioni dell'agente sono influenzate dal tipo di ambiente in cui si trova.<br>
Gli ambienti vengono classificati in base ai seguenti criteri:

* **Osservabilità**:
    
    * **Fully Observable**: i sensori dell'agente gli danno accesso allo stato completo dell'ambiente in qualisasi momento.

    * **Partially Observable**: l'agente ha una conoscenza parziale dell'ambiente che lo circonda (può essere causato dalla limitatezza dei sensori o dalla natura stessa dell'ambiente)

* **Single Anget Vs Multi Agent**: possibilità di avere un singolo agente o molteplici che possono essere **Competitivi** o **Cooperativi**

* **Determinabilità**:

    * **Deterministico**: lo stato successivo dell'ambiente è determinato completamente dallo stato attuale e dalle azioni effettuate dall'agente

    * **NON Deterministico**: tutto ciò che non è deterministo è dunque NON Deterministico (`best effort !`)

* **Episodico Vs Sequenziale**:

    * **Episodico**: gli stati futuri non dipendono dalle azioni svolte in precedenza dall'agente (come il controllore di difetti in una linea di assemblaggio)

    * **Sequenziale**: il contrario di Episodico (`best effort !`)

* **Dinamicità**:

    * **Statico**: l'ambiente cambia solamente quando l'agente effettua delle azioni

    * **Dinamico**: l'ambiente può cambiare mentre l'agente sta pensando

* **Discreto Vs Continuo**: dipende dalla maniera in cui il tempo e lo stato dell'ambiente sono gestiti dall'agente, per esempio: una partita di scacchi è discreta mentre un gioco di strategia no.

* **Conoscibilità**: la conoscenza dell'agente rispetto alle leggi dell'ambiente in cui si trova.<br>
_E.g._: In un ambiente conosciuto data una serie di azioni si conosce il risultato.

## Algoritmi di Ricerca

Dato un problema sconosciuto l'agente può operare in 2 modi:

* Compiere azioni random sperando di raggiungere la soluzione

* Seguire il seguente processo di problem solving:

    1. Goal Formulation
    2. Problem Formulation
    3. Search
    4. Execution

Durante le fase di Execution gli agenti possono utilizzare 2 modelli di systemi:

* **Open Loop**: gli agenti hanno la certezza che durante un'azione lo stato dell'ambiente non venga alterato

* **Closed Loop**: l'opposto di Open Loop (`best effort !`)

### Definizioni di Algoritmi di Ricerca

* **Problema**: l'insieme degli stati possibili nei quali l'ambiente può esistere, viene anche chiamato **Spazio degli Stati**

* **Stato iniziale**: lo stato in cui l'agente inizia

* **Stato Goal/Finale**: lo stato che l'agente vuole raggiungere

* **Azioni**: dato uno stato `s` la funzione `action(s)` ritorna un insieme finito di azione che possono essere eseguite in s e sono dette **applicabili in s**.<br>
`ACTION(Arad) = {ToSibiu, ToTimisoara, ToZerind}`

* **Modello di Transizione**: ritorna lo stato che risulta dall'applicazione di una determinata azione `a` in uno stato `s`.<br>
`RESULT(Arad, ToZerind) = Zerind`

* **Funzione Costo Azione**: ritorna il costo numerico richiesto per applicare un'azione `a` in uno stato `s` per raggiungere lo stato `s'`.

* **Nodi di Frontiera**: i nodi visti ma non espansi.

* **Cammino**: la conseguenza di insieme di azioni.

* **Cammino Ridondante**: è un cammino che porta allo stesso nodo ma con costo maggiore. Un ciclo è un particolare tipo di cammino ridondante.

* **Soluzione**: il cammino che va dallo stato iniziale ad uno stato goal/finale.<br>Una soluzione si dice **ottima** se corrisponde al percorso di costo minore tra tutte le soluzioni.

### Rappresentazione di un problema di ricerca

Un problema di ricerca può essere rappresentato in 2 modi:

1. Lo State Space Graph (il grafo dello spazzio degli stati)
2. L'Albero di Ricerca


Le principali differenze tra i 2 sono che:

|State Space Graph|Albero di Ricerca|
|-----------------|-----------------|
|Ad ogni nodo corrisponde uno stato e ogni arco corrisponde ad un'azione che può esser eseguita in quello stato.|Ci possono essere più nodi uguali, però dato un nodo, il cammino che lo riporta alla radice è unico.|
|_Ti fa vedere tutto il problema_| _Qui vedi più chiaramente il cammino_.|
|![Romania ia ia oh](./imgs/romania.png)|![albero di ricerca](./imgs/searchtree.png)|


L'albero di ricerca riportato sopra presenta un ciclo tra `Arad` e `Sibiu`. Poichè i cilci possono essere percorsi infinite volte, l'albero di ricerca **completo** può avere infiniti nodi !


Questa mappa verrà presa in considerazione per i successivi esempi:
![Romania ia ia oh](./imgs/romania.png)


### Il Problema dei Cammini Ridondanti

I cammini ridondanti possono andare a complicare di molto alcuni problemi di ricerca e quindi vanno evitati.<br>
Ci sono 3 diversi modi per farlo:

1. **Memorizzare i nodi visitati**. Questo metodo è particolarmente utile se si hanno tanti cammini ridondanti e se abbiamo abbastanza spazio in memoria per rappresentare la tabella degli stati raggiunti.

2. **Metodo Milani**: se non c'è bisogno di farlo non lo fare ! Eseisto alcuni casi in cui non è necessario tenere traccia degli stati già visti perchè la struttura del problema impedisce a determinate azione di essere effettuate.<br>
_E.g._ una linea di assemblaggio.

3. **Parent Link**: si controlla solo la presenza di cicli e non di cammini ridondanti. Ogni nodo ha un link al proprio nodo padre e si risale all'indietro questa "catena" per vedere se vi è un ciclo.<br>
Alcune implementazini risalgono tutta la catena, impiegano molto tempo ma tolgono tutti i cicli, altre solo una piccola parte (3 o 4 salti all'indietro), impiegano un tempo costante ma riescono a togliere solo piccoli cicli.


### Graph Search vs Tree-like Search

Possiamo fare una distinzione degli algoritmi in base alla necessità di controllare la presenza di cammini ridondanti:


|Graph Search|Tree-like Search|
|------------|----------------|
|Questi algoritmi controllano la presenza di cammini ridondanti|**NON** controllano la presenza di cammini ridondanti.
|Best First Search|Assembly Problem|


### Complessità degli algoritmi di ricerca

Per decidere quale algoritmo di ricerca utilizzare è necessario guardare alle loro diverse caratteristiche di complessità.<br>
Le 4 che vengono prese in considerazione sono:

* **Completezza**: la capacità di un algoritmo di garantire il ritrovamento della soluzione, se ce n'è una, o di riportare il fallimento se non ne viene trovata nessuna.
* **Ottimalità di costo**: la capacità di trovare il cammino di costo minimo
* **Complessità di tempo**: il tempo richiesto per torvare una soluzione. Può essere misurato in secondi o in numero di stati analizzati e di azioni compiute.
* **Complessità in spazio**: la memoria utilizzata pe l'esecuzione dell'algoritmo.


### Spazio degli stati infiniti

Quando lo spazio degli stati è finito non ci sono grandi problemi per la ricerca di una soluzione. Qunando invece si tratta di uno spazio degli stati infinito, la ricerca deve essere fatta **sistematicamente** per evitare di applicare sempre la stessa azione e non tornare mai indietro per controllare stati vicini allo stato iniziale.


### State Space Graph Implicito ed Esplicito

In un State Space Graph **Esplicito** generalmente il calcolo della complessità non è difficoltoso poichè basta rappresentarlo con un search tree e la complessità risulterà: `|V| + |E|` con:

* `|V|` numero di nodi
* `|E|` numero degli archi

In alcuni problemi di IA, tuttavia, il grafo può essere rappresentato in maniera **Implicita**.<br>
In questi casi la complessità può essere misurata in funzione di 3 fattori:

* `d` (**_depth_**): il numero di azioni in una soluzione ottimale
* `m`: massimo numero di azioni in un cammino qualsiasi
* `b` (**_brancing factor_**): il numero di successori ad un nodo che deve essere preso in considerazione


### Best First Seach

Uno degli algoritmi di ricerca più semplici è il **Best First Search**, esso basa la scelta del nodo su una funzione di valutazione, scelta arbitrariamente, chiamata `f(n)`.<br>
Ad ogni iterazione viene scelto il nodo di frontiera con `f(n)` minimo e:

* se è lo stato Goal ritorna il corrispondente cammino
* altrimenti applica la funzione `EXPAND()` per generare altri nodi figli e li aggiunge alla frontiera se non sono mai stati raggiunti o sono riaggiunti se ora possono essere raggiunti con un cammino di costo inferiore a quello precedente.<br>
Questo algoritmo ritorna un avviso di fallimento o un cammino che rappresenta la soluzione.

```javascript
//problem contiene:
//  Insieme degli Stati
//  Stato Iniziale
//  Stato Goal/Finale
//f:
//  funzione di valutazione costo
function BestFirstSerach(problem, f) {
    // stato iniziale del problema
    node = problem.getInitalNode()

    // priority queue basata su F e inizia con node
    frontier = []
    frontier.add(node)

    // tabella di LookUp (tipo una HashMap) inizializzata 
    // con key=NodoIniziale value=CostoDelNodo
    reached = LookUpTable()
    reached[node.STATE] = node

    // fin quando non ci sono più elementi in frontiera
    while (frontier is not Empty) {
        // prende l'elemento di costo minore
        node = frontier.pop()

        if isGoal(node.STATE)
            return node
        
        foreach (child in expand(problem, node)) {
            s = child.STATE

            // aggiunge il nodo alla frontiera se:
            //  non è mai stato visitato
            //  è raggiungibile con costo minore
            if (s not in reached) or (child.PATH_COST < reached[s].PATH_COST) {
                reached[s] = child
                frontier.add(child)
            }
        }
    }

    return failure
}

//problem contiene:
//  Insieme degli Stati
//  Stato Iniziale
//  Stato Goal/Finale
//node:
//  il nodo da espandere
function expand(problem, node) {
    s = node.STATE

    // trova tutti i nodi raggiungibili da node e ne calcola i costi
    foreach (action in problem.actions(s)) {
        s1 = problem.result(s, action)
        cost = node.PATH_COST + problem.actionCost(s, action, s1)
        yield Node(STATE=s1, PARENT=node, ACTION=action, PATH_COST=cost)
    }
}
```

In questo algoritmo vengono scartati i **Cammini Ridondanti**.


### Agente Informato vs Non Informato

Un Agente **non informato** non sa se scegliendo una soluzione andrà ad avvicinarsi al Goal, quindi date 2 possibili azioni,  mentre un agente informato si.


### Ricerca Non Informata

A questa famiglia di ricerca appartengono:

* **Breadth First Search**
* **Best First Search** (Dijisktra) <!-- ricordarsi che Jhonson fa un pompino a Dijkstra -->
* **Depth First Search**
* **Depth Limited Search**
* **Iterative Deeping Search**

#### Breadth Firs Search

<!-- Aggiungere BREACKFAST -->

Quando le azioni hanno tutte quante lo stesso costo può essere una buona idea utilizzare la Breadth First Search. Essa è molto simile alla Best First Search, ma come funzione di valutazione `f(n)` considera non il costo delle azioni, ma la **profondità** del nodo, ovvero il numero di azioni richieste per raggiungerlo.

Nell'implementazione è possibile migliorarlo alterando alcuni aspetti della Best First Search:

* La coda **frontier** può essere impelemntata come una coda FIFO dato che darà una coda che rispetta già l'ordine di visita per la Bereadth First Search (i più vecchi vengono visitati prima)
* La tabella **reached** può essere impostata con gli stati piuttosto che con una mappatura stati-nodi
* E' possibile effettuare un **early goal test** poichè, una volta trovato un cammino, saremo sicuri che non ci saranno altri cammini migliori per raggiungere quel nodo

Questo algoritmo è **Completo** e **Ottimo**.<br>
Ha una complessità in **tempo** e **spazio** equvalenti che sono: $O(b^d)$

Quando lo spazio delle soluzioni è molto ampio e si ha un brancing factor elevato, non è possibile applicare algoritmi di ricerca non informati poichè si va in contro a limitazioni fisiche di memoria e, anche ipotizzando una memoria infinita, si raggiungono tempi di esecuzione impraticabile (per uno stato goal con d = 14 e b = 10 il tempo di esecuzione richiesto sarebbe di 3.5 anni)

```javascript
function breadthFirstSearch(problem) {
    // stato iniziale del problema
    node = problem.getInitalNode()

    // goal test per terminare immediatamente se in stato finale
    if isGoal(node.STATE)
        return node
    
    // coda FIFO inizializzata con il nodo node
    frontier = []
    frontier.append(node)

    // lista di stati visitati
    reached = []
    reached.append(node.STATE)

    while (frontier is not Empty) {
        node = frontier.pop()

        // espande i figli del nodo estratto dalla fifo
        foreach (child in expand(problem, node)) {
            s = child.STATE

            // early goal test
            if isGoal(s)
                return child
            
            // aggiunge il figlio alla frontiera
            if (s not in reached) {
                reached.append(s)
                frontier.append(child)
            }
        }
    }

    return failure
}
```

#### Algoritmo di Dijkstra o Uniform Cost Search

Questo algoritmo, a differenza della breadth first serach che espande i nodi in base alla profondità, espande i nodi in base al costo del cammino totale: guarda prima i commini con lo stesso costo.<br>
Non si espande nodo in nodo ma cammino in cammino.

Il costo di questo algoritmo in **spazio** e **tempo** è ![Costo Uniform Cost Search](./imgs/uniform_cost.gif) con:

* ![C star](./imgs/c_star.gif): il costo della soluzione ottimale
* ![b](./imgs/b.gif): brancing factor
* ![epsilon](./imgs/epsilon.gif): il minimo costo di un'azione
  
Questo algoritmo può essere utilizzato come la breadth first search se il costo di tutte le eazioni è equivalente ed il suo costo in tempo e spazio è di ![costo](./imgs/o_b_d1.gif)

La Uniform Cost Search è un algortimo **Completo** e **Ottimale** perchè la prima soluzione che trova sarà sempre il cammino di costo minore perchè basato su un algoritmo greede (best first search).

```javascript
function uniformCostSearch(problem) {
    //PATH_COST è una funzione che si basa sul costo totale del percorso
    return bestFirstSearch(problem, PATH_COST)
}
```

#### Depth First Search

La DFS espande sempre il nodo più in profondità nella frontiera.
Può essere implementata in due modi differenti:

* **Invocando la Best First Search**: con una `f(n)` che è il negativo della profondità <!-- va guardato meglio -->
* **Con Tree-Like Search**: non tiene traccia dei nodi visitati a differenza del graph search.

Generalmente si predilige l'implementazione con **Tree-Like Searh** all'utilizzo della Best First Search.

_Esempio di funzionamente della DFS:_
![dfs_example](./imgs/dfs_example.png)

Per uno spazio degli stati ad albero è **Efficiente** e **Completa**.<br>
Per uno spazio degli stati **aciclico** può risultare che espande più volte lo stesso stato (attraverso differenti percorsi), ma alla fine riuscirà a completare la ricerca in maniera sistematica.<br>
In un insieme degli stati **con cicli** può rimanere bloccata in un ciclo infinito e perciò alcune implementazioni controllano la presenza di cicli.<br>
Con uno spazio degli stati invinito la DFS non è sistematica perchè può bloccarsi in un percorso di lunghezza infinita.

Il costo per uno spazio degli stati and albero è: ![costo dfs](./imgs/o_b_m.gif) con:

* `b`: il branching factor
* `m`: profondità massima

Una variante della DFS è la Backtracking Search che utilizza ancora meno memoria perchè espande un solo nodo successore alla volta, garantendo così la possibilità di "annullare" un'azione.

#### Depth Limited Search & Deepening Search

**Depth Limited Search**

Un implementazione concreta della DFS per AI è la **Depth Limited Search** (DLS), nella quale viene definito un limite di profondità `l` oltre il quale i nodi non verrano considerati.

La sua complessità in tempo è: ![tempo](./imgs/o_b_l.gif)
La complessità in spazio è: ![spazio](./imgs/o_bl.gif)

```javascript
function depthLimitedSearch(problem, l) {
    // coda LIFO inizializzata con il nodo stato iniziale
    frontier = []
    frontier.add(problem.getInitalNode())

    result = failure

    while (frontier not Empty) {
        // prende l'ultimo nodo aggiunto
        node = frontier.pop()

        // controlla se ha trovato il goal
        if (isGoal(node.STATE))
            return node
        
        // controlla se ha superato il limite l
        if (node.DEPTH > l)
            result = cutoff

        // controlla di non essere in un ciclo
        else if (if not isCycle(node)) {
            // espande i nodi e li aggiunge alla frontiera
            foreach (child in expand(problem, node)){
                frontier.add(child)
            }
        }
    }

    return result
}
```

Con la funzione `isCycle()` si vanno ad eliminare, con un costo di computazione leggermente maggiore, i cicli "corti" (considerando 3 o 4 elementi prima). I cicli "lunghi" vengono gestiti con il limite `l`.

La scelta del limite `l` può essere abbastanza problematica: in generale non sappiamo quale sia un "buon limite" fin quando non abbiamo risolto il problema.
Per uno spazio degli stati a modi grafo, come quello della Romania, possiamo utilizzare il **diametro** del grafo come limite `l`.

_Il **diametro** di un grafo è il cammino più lungo che collega 2 nodi senza cicli al suo interno._

**Iterative Deepening Search**

Questo algoritmo risolve il problema di scegliere un buon valore per il limite `l`: prova tutti i limiti possibili<br>
Combina i benefici della Depth First Search e della Bredth First Serach:

* la memoria richiesta è modesta: ![o b d](./imgs/o_bd.gif) se c'è una soluzione, altrimenti è ![o b m](./imgs/o_b_m.gif)
* come la Bredth First Search, è ottimale se tutte le azioni hanno costo uguale
* la complessità in tempo è di: ![obd](./imgs/o_b_d.gif) se c'è una soluzione, altrimenti ![obm](./imgs/o_bm.gif)

Generalmente la IDS è il metodo di ricerca **non informato** più usato quando il lo spazio degli stati è più grande della memoria utilizzabile e la profondità della soluzione non è conosciuta anche se il suo tempo è asintoticamente uguale a quello della breadth first search.

```javascript
function iterativeDeepningSearch(problem) {
    for (depth=0 to inf) {
        result = depthLimitedSearch(problem, depth)

        if (result != cutoff)
            return result
    }
}
```

_Esempio di funzionamento della IDS_
![IDS example](./imgs/ids_example.png)


#### Comparazione tra algoritmi di ricerca non informati

|Criterio|Bredth First|Uniform Cost|Depth First|Depth Limited|Iterative Deepnening|Bidirectional|
|:------:|:----------:|:----------:|:---------:|:-----------:|:------------------:|:-----------------:|
|**Completo?**|SI|SI|NO|NO|SI|SI|
|**Ottimale?**|SI|SI|NO|NO|SI|SI|
|**Tempo**|![](./imgs/o_b_d.gif)|![](./imgs/uniform_cost.gif)|![](./imgs/o_bm.gif)|![](./imgs/o_b_l.gif)|![](./imgs/o_b_d.gif)|![](./imgs/o_b_d2.gif)|
|**Spazio**|![](./imgs/o_b_d.gif)|![](./imgs/uniform_cost.gif)|![](./imgs/o_b_m.gif)|![](./imgs/o_bl.gif)|![](./imgs/o_bd.gif)|![](./imgs/o_b_d2.gif)|


### Ricerca Informata (con Euristica)

La ricerca informata utilizza delle funzioni chiamate **Euristiche**, indicate con `h(n)`, per trovare in maniera più efficiente la soluzione ad un problema.<br>
La funzione `h(n)` corrisponde alla **stima in costo** del cammino meno costoso dallo stato `n` allo stato finale.


#### Greedy Best First Search

E' la versione informata dell Best First Search che, piuttosto di basare la sua scelta su una funzione di valutazione `f(n)`, si basa su una funzione euristica `h(n)` detta Straight Line Distance Heuristic (`f(n) = h(n`). Questa euristica fornisce informazioni su quale nodo ci permette di avvicinarci sempre di più al goal, senza però prendere in considerazione la distanza richiesta per percorrere il cammino.

Il costo di questo algoritmo sia in tempo che in spazio è: ![O mod V](./imgs/o_mdV.gif), però, utilizzando un'euristica molto buona, può essere ridotto a ![O bm](./imgs/o_b_m.gif).

E' **completa** negli **spazi** degli **stati finiti** ma non in quelli infiniti.

![Greedy best Example](./imgs/greedy_best_first_example.png)


#### A* Search

L'algoritmo definitivo per la ricerca informata è chiamato **A STAR**. Esso basa la sua scelta di cammino su due fattori:

* il costo del cammino fino al nodo n (`g(n)`)
* il costo dell'euristica (vista prima) `h(n)`

`f(n) = g(n) + h(n)`

Il risultato di questa somma corrisponde al cammino di costo minimo che permette di avvicinarsi sempre di più allo stato goal.

A* è un algoritmo completo ma la sua ottimalità in costo dipende da alcune proprietà dell'euristica:

* **Ammissibilità**: capacità dell'euristica di non sovrastimare mai il costo per raggiungere il goal (l'euristica è _ottimistica_).
* **Consistentza**: la capacità dell'euristica di mantenere sensate le sue previsioni, ovvero l'euristica per raggiungere un nodo, deve essere minore o uguale alla somma tra un nuovo cammino figlio del nodo di partenza e l'euristica del nuovo nodo (la distanza in line d'aria del punto di partenza è il valore minimo per raggiungere il goal e quindi aggiungendo altri percorsi non si potrà fare meglio). Viene chiamata regola dell'**inequità del triangolo**.
![inequita](./imgs/inequita.png)

Un eurisitica consistente è sempre ammissibile, ma non è detto il contrario.<br>
L'euristiche possono peggiorare la performance della ricerca costringendo l'algoritmo a tornare su più nodi già visitati.

Con un abuona euristica, non avremo necessità di ricontrollare e aggiornare la tabella `reached`.

_Esempio di funzionamento di A*_
![esempio di A*](./imgs/esempio_astar.png)

Quindi con una euristica Consistente A* è:

* **Completo**
* **Ottimo**

#### Ricerca Soddisfacente

A* è un ottimo algoritmo ma può presentare problemi (tempo e spazio) in alcuni tipi di ambienti. Se però ci si accontenta di una soluzione che non è ottima si possono raggiungere dei risultati soddisfacienti esplorando un numero significativamente minore di nodi. Queste soluzioni sono chiamate **soddisfacienti** e sono derivate dall'uso di un'euristica inammissibile, ovvero che può sovrastimare `h(n)`. Così facendo, c'è il rischio di mancare la soluzione ottima però l'euristica può essere più precisa nell'avvicinarsi alla soluzione scartando quelle che non ritiene opportune e permettendo così la visita di meno nodi.

##### A* Pesato

Un implementazione con A* consiste nel dare un maggior peso all'euristica utilizzando una funzione di valutazione `f(n) = g(n) + W * h(n)`, con `W > 1` 

_Esempio di A* pesato contro A*_
![A Star Pesato](./imgs/a_star_peso.png)

La funzione di valutazione di A* Pesato può essere vista come una generalizzazione delle funzioni di valutazione viste in precedenza:

|Algoritmo|`f(n)`|`W`|
|-|-|-|
|A* Search|`g(n) + h(n)`|`1`|
|Uniform-cost Search|`g(n)`|`0`|
|Greedy Best First Search|`h(n)`|`infinito`|
|A* Pesato|`g(n) + W * h(n)`|`1 < W < infinito`|


#### Memory Bounded Search

Il problema principale di A* è il suo utilizzo della memoria. Ci sono degli stratagemmi per aggirare questo problema.

Una prima soluzione è quella di cercare di eliminare la tabella dei nodi raggiunti (`reached`) a costo di complicare l'algoritmo e di rallentarne l'esecuzione.

Un'altra possibilità è quella di eliminare dagli stati raggiungi gli stati non più necessari. Questo può essere fatto assicurandosi che le azioni possano solamente muoversi verso la frontiera o su altri nodi di frontiera e mai tornare indietro. Successivametne cercare nella frontiera cammini ridondanti ed eliminarli dalla tabella `reched`.

Un altro modo è quello di tenersi un contatore che controlla quante volte un nodo è stato visitato eliminandolo poi dalla tabella degli stati raggiunti se viene visitato da tutti i suoi vicini (risulterà quindi inutile).


##### Iterative Deepening A*

Questo algoritmo è l'equivalente della Iterative Deepening Search per A*. Invece di limitare le ricerche con la profondità, utilizzerà il valore di `f(n)`. Ad ogni iterazione, se non trova lo stato goal, ritorna all'iterazione successiva il nuovo valore di cutoff che sarà il nodo con minor peso che supera il valore attuale di cutoff.

Questo algoritmo è ottimo per problemi come l' 8 Puzzle dove il valore di `f(n)` è un intero.

Se il valore ottimale della soluzione è `C*` allora non verranno effettuate più di `C*` iterazioni.


##### Recursive Best First Search

Cerca di imitare le operazioni della Best First Search, ma utilizza uno spazio lineare.
Per ovviare alla mancanza della tabella `reached`, la RBFS ogni volta che espande un nodo salva il valore `f(n)` della sua migliore alternativa (limite). Se tutti i figli del nodo corrente superano quel limite, la ricorsione "torna indietro" alla migliore alternativa, cambiando il valore del nodo appena espanso al valore del suo miglio figlio.

```javascript
function recursiveBestFirstSearch(problem) {
    // avvia la ricorsione
    solution, fvalue = rbfs(problem, problem.getInitalNode(), inf)

    return solution
}

function rbfs(problem, node, f_limit) {
    // controlla se ha trovato lo stato goal
    if isGoal(node.STATE)
        return node
    
    // espande il nodo
    successors = expand(node)

    // se non ha figli ritorna un fallimento
    if (successors is Empty)
        return failure, inf
    
    // aggiorna il costo dei nodi figli
    foreach (s in successors) {
        s.f = max(s.PATH_COST + h(s), node.f)
    }

    while (true) {
        // prende i successore con la minore f-value
        best = successors.getBestSuccessor()

        // fa backtracking
        if (best.f > f_limit)
            return failure, best.f
        
        // prende il secondo successore con la minor f-value
        alternative = successors.getSecondBestSuccessor()

        // continua la ricorsione
        result, best.f = rbfs(problem, best, min(f_limit, alternative.f))

        // ritorna la miglior scelta
        if( result != failure)
            return result, best.f
    }
}
```

_Esempio di funzionamento della RBFS_
![RBFS Esempio](./imgs/rbfs_example.png)

Questo algoritmo è un po' più efficente di IDA* ma soffrre dell'utilizzo di troppa poca memoria portandolo a riiterare degli stessi cammini più volte prima di torvare una soluzione.
RBFS è ottimo con una funzione euristica `h(n)` ammissibile, ma la sua complessità nel tempo è difficile da calcolare perchè connessa all'accuratezza dell'euristica e a quanti "cambi di idea" l'algoritmo ha durante la sua esecuzione.


##### Memory Bounded A* & Simplified A*

Sembra ragionevole poter far sfruttare ai nosti algoritmi tutta la memoria a loro disposizione. Esistono due algoritmi che la sfruttano appieno:

* Memory Bounded A* (MA*): è troppo complicato per le nostre piccole menti.
* Simplified Memory Bounded A* (SMA*): il suo funzionamento è molto semplice, l'algoritmo procede come un normalissimo A* fin quando non finisce la memoria per poi eliminare il nodo con la `f-value` più grande e ne salva quest ultima sul suo nodo predecessore cosicche si possa ricordare la miglior f-value, trovata fin ora, nel sottoalbero generato da quel nodo.

L'SMA* può avere problemi di tempistiche, perchè quando finisce la memoria, eliminando i nodi con costo maggiore potrebbe andare a riespanderli e quindi passare più volte sugli stessi nodi. Questo può accadere in problemi molto difficili, il che significa che dei problemi risolvibili con un A*, dalla memoria infitia, non sono risolvibili dalla SMA* ma ovviamente non si può avere una memoria infinita e quindi per poter trovare una soluzione dobbiamo accontentarci non del miglior cammino ma di uno che sia "abbastanza buono".


##### Funzioni Euristiche

Il problema dell'8 puzzle possiamo fare a meno delle euristiche dato che può essere tutto rappresentato in memoria, ma per il 15 puzzle iniziano ad esserci un numero eccessivamente grade di stati per essere rappresentati in memoria, quindi è necessario ricorrere a delle euristiche ammissibili. Le principali euristiche utilizzate per questi tipo di porblema sono 2:

* `h1`: il numero di tasselli in posizioni sbagliate (escluso quello vuoto)
* `h2`: la somma della distanza dei tasselli dalla loro posizione finale, viene anche chiamata **city block distance** o **Mhanattan distance**

Un fattore che viene spesso perso in cosiderazione per misurare la qualità di una euristica è il **branchin factor effettivo**: è il branching factor che viene calcolato su un albero di profondità `d` formato da `N+1` nodi che sono quelli esplorati da un algoritmo di ricerca (più è vicino ad 1 e migliore sarà l'euristica).

Nella seguente tabella vediamo i differenti branching factor effettivi relativi all'euristica `h1`, `h2` e nessuna euristica. Evice che generalmente `h2` è la migliore scelta.
![H1 vs H2](./imgs/h1h2.png)

Possiamo dire che `h2` domina `h1`, ovvero che `h2(n) >= h1(n)`. La dominazione si può tradurre direttamente in efficenza, in quanto implica che `h2` non espanderà mai più nodi di `h1` per un dato algoritmo di ricerca.


##### Problemi rilassati per individuazione di Euristiche

Un problema rilassato è caratterizzato da minori condizioni vincolanti rispetto a un problema di riferimento.

Si ricorre alla tecnica dei problemi rilassati (**relaxed problem**) per agevolare la ricerca delle soluzioni o di una euristica di ricerca. Nel caso dei problemi rilassati l'agente ha maggiore libertà di azione e può intraprendere strade altrimenti inibite nel problema di riferimento. Questa maggiore libertà di azione consente di individuare una funzione euristica più efficiente, da applicare successivamente nelle operazioni di ricerca informata del problema di riferimento.

Il problema rilassato è caratterizzato da un albero di ricerca più grande rispetto a quello di origine. La complessità spaziale e temporale è, pertanto, maggiore. È utile ricorrere a queste tecniche soprattutto per individuare una funzione euristica efficiente, al fine di poterla utilizzare successivamente negli algoritmi di ricerca informata.

Essendo l'albero di ricerca del problema di riferimento, quello con maggiori condizioni, un sottoinsieme dell'albero di ricerca del problema rilassato, la migliore euristica di ricerca individuata nella versione "rilassata" del problema è altrettanto valida anche nella versione "rigida" del problema (problema originale). Inoltre, essendo una euristica derivata, questa eredita le medesime caratteristiche di ammissibilità e di consistenza nell'applicazione sia nel problema rilassato che nel problema originale.


## Adversarial Search & Games

Degli ambienti competitivi nei quali ci sono 2 o più agenti, con obbiettivi contrastanti, fanno nascere il problema dell'**Adversarial search**. Ci sono 3 possibili approcci per gestire gli ambienti multiagenti:

1. si applica quando c'è un gran numero di agenti e consiste nel trattarli come un aggregato, quindi non si andrà a predire le azioni degli agenti individuali, ma quelle del proprio gruppo.

2. l'agente può essere considerato parte dell'ambiente che lo rende **non deterministico**, bisogna però stare attenti a quale modello si sceglie per l'agente avversario (esempio della pioggia)

3. modellarlo in maniera esplicita con le tecniche dell'**adversarial tree search** (verrà approfondito in seguito)


### Giochi a somma 0 con 2 giocatori

Questo tipo di giochi sono quelli più studiati nei campi dell'intelligenza artificiale e sono caratterizzati dalle seguenti proprietà:

* **Deterministici**
* **A 2 Giocatori**
* **A turni**
* Perfect information (**Fully Observable**)
* **A somma 0**: ad ogni azione positiva per un giocatore, corrisponderà un'azione altrettanto negativa per l'altro.

Un gioco di questo tipo può essere definito dai seguenti elementi:

* `S0`: stato iniziale del gioco
* `To-Move(s)`: il giocatore che deve muoversi allo stato `s` (a chi sta il turno)
* `Actions(s)`: un set di mosse eseguibili dal giocatore nello stato s
* `Result(s, a)`: definisce il rislutatio di un azione `a` effettuata nello stato `s`
* `Is-Terminal(s)`: controlla se lo stato `s` è uno **stato terminale**
* `Utility(s, p)`: assegna un punteggio predetermintato `p` al vincitore del gioco (in scacchi la vittoria vale 1, perdita 0 e pareggio 1/2)

Le **Azioni**, lo **Stato Iniziale** e la funzione `Result` definiscono lo **State Space Graph**. Possiamo applicare un **albero di ricerca** da un determinato nodo per capire quale mossa fare.

Definiamo il **Game Tree** come un albero di ricerca che segue ogni sequenza di mosse fino alla fine del gioco (stato terminale). Se il gioco lo permette o se lo state space è infinito, allora il Game Tree può essere infinito.

### MinMax Search

L'idea fondante di questo algoritmo è che andrà a scegliere la sua mossa migliore per ogni giocatore, puntando a massimizzare il proprio obbiettivo e cercare di minimazzre il punteggio dell'altro.

La funzione su cui si basa questo algoritmo è `MinMax`. Questa funzione ritorna un valore numerico che viene scelto in base a chi effettua l'azione: 

* se è il turno di MAX allora MinMax cercherà il nodo con valore maggiore
* se è il turno di min, cercherà il nodo con valore minore.

```javascript
global player

function minMaxSearch(game, state) {
    player = game.toMove(state)
    value, move = maxValue(game, state)

    return move
}

function maxValue(game, state) {
    if (game.isTerminal(state))
        return game.utility(state, player), null

    v = -inf

    foreach (a in game.actions(state)) {
        v2, a2 = minValue(game, game.result(state, a))

        if (v2 > v)
            v, move = v2, a
    
    }

    return v, move
}

function minValue(game, state) {
    if (game.isTerminal(state))
        return game.utility(state, player), null

    v = +inf

    foreach (a in game.actions(state)) {
        v2, a2 = maxValue(game, game.result(state, a))

        if (v2 < v)
            v, move = v2, a
    }

    return v, move
}
```

Proprietà dell'algoritmo:

* è **Completo** per alberi finiti
* è **Ottimo** contro avversari ottimi (vince comunque contro avversari non-ottimi)
* Ha una complessità in tempo di ![o b m](./imgs/o_bm.gif)
* Ha una complessità in spazio di ![bm](./imgs/o_b_m.gif) se vengono generate tutte le azioni, se ne viene generata una per volta è ![o m](./imgs/o_m.gif)


### Alfa Beta Prugne

L'algoritmo funziona raggiungendo le foglie del Game Tree (che noi chiameremo Albero di Prugne) e ne guarda il valore dell'utility. Sul primo ramo l'algoritmo salva il valore minimo che poi andrà a confrontare con i vaoliri minimi degli altri rami. Se incontra un valore minimo minore di quello salvato ferma l'esplorarione di quel ramo e passa a quello successivo (_pruning_).

C'è un euristica chiamata _Killer Move_ che sono le migliori mosse conosciute di quel problema a seconda di determinati stati.

Il costo in tempo nel caso migliore (le mosse vengono ordiante dal costo più piccolo al costo più grande) è: ![obm2](./imgs/o_bn2.gif).<br>
Il costo in tempo nel caso peggiore è: ![obm](./imgs/o_bm.gif) come quello del MiniMax.

_Funzionamento dell'agoritmo_
![alfa beta prugna](./imgs/alfabetaprugna.png)

_Esempio di pseudocodice dell'algoritmo_
![alfa beta code](./imgs/alfabetacode.png)


### Giochi con alberi molto grandi :palm_tree:

Per giochi con branching factor molto grande, come Go e Schacchi, il MinMax anche se potenziato con AlfaBetaPrugna e il Clever Ordering, non è in grando di trovare una soluzione in un tempo utile. Per questo sono state proposte 2 strategie teoriche:

* **Tipo A**: consiste nel considerare tutte le possibilità fino ad un certo livello di profondità e poi calcolare l'utiliti a quel livello prestabilito
* **Tipo B**: ignora le mosse che sembrano poco promettenti e segue la linea promettente il più a lungo possibile, quindi esplora una porzione stretta dell'albero andando in profondità

## Machine Learning

### Tipi di Learning

* **Supervised Learning (inductive)**: vengono passati i dati per fare il training e i corrispettivi output
* **Unsupervised Learingn**: vengono forniti solamente i dati per il treaning e non gli output
* **Semi-supervised Learning**: vengono forniti i dati per fare il training e parte degli output
* **Renforcement learing**: ogni sequenza di azioni corrispende una ricompensa (rewareds).

**Supervised Learning**

Delle applicazioni di Supervised Learning sono la funzione di regressione lineare (previsioni) e classificazione.

**Unsupervised Learingn**

L'utilizzo principale del Unspuervised Learning è l'individuazione di pattern nascosti nei dati di input.
Delle applicazioni concrete possono essere:

* l'organizzazione di cluster di computer
* analisi di social network
* segmentazione del mercato

**Renforcement learing**

Il Reinforcemetne Learning si basa su un sistema di reworwd ritartadato con il quale viene fornita in output una policy che è una mappatura stato - azione (in un dato stato ti dice quale azione eseguire).
Alcuni esempi possono essere:

* Game Playing
* Robot in a maze
* Bilanciare un palo nella mano

### Progettare un sistema di Learning

Per progettare un sistema di leaning vanno seguiti i deguneti passi:

1. Scegliere il tipo di learning (supervised, unsupervised, ...)
2. Scegliere che cosa si vuole imparare (l'obbiettivo da raggiungere)
3. Scegliere come rappresentare l'obbiettivo
4. Scegliere un algoritmo di learning per dedurre la funzione obbiettivo dall'esperienza

![progettare_ai](./imgs/progettare_ai.png)

Ogni algoritmo è costituito da 3 componenti:

* Rappresentazinoe
* Ottimizzazione
* Valutazione

Alcune funzioni di rappresentazini:

* Funzioni Numeriche
    * Regressione Lineare
    * Neural Network
* Funzioni simboliche
    * Decison Tree :palm_tree:
* Funzioni Instance-based
    * Nearest neigthbour
* Modelli Probabilistic Gaphical
    * Naive Bayes
    * Hidden Markov Models (HMMS)
    * Probabilistic Context Free Grammars (éCFGs)
    * Markov Networks

Algoritmi di Ricercara/Ottimizzazinoe:

* Gradient decent
    * Perceptron ([Pompotron](https://www.youtube.com/watch?v=0YQmE21aMnw&ab_channel=OrionNebula))
    * BackPropagation
* Dynamic Programming
    * HMM Learning
    * PCFG Learning
* Divide and Conquer 
    * Decision tree induction
    * Rule learingn
* Evalutaionary Comutation
    * Genetic Algorhtim (GAs)
    * Genetic Progarmming (GP)
    * Neuro evolution 

Alcuni criteri di valutazione:

* Accuracy
* Precision ad Recall
* Squared error
* Likelihood
* Posterior probability
* Cost / Utility
* Margin
* Entropy
* K-L Divergence

### Alberi (di nuovo diocane)

**Definizione Classificazione**: dato un training set, ogni elemento è caratterizzato da una tupla `(x, y)` dove:

* `x` è un inisme di attributi (_input_)
* `y` è il nome della classe (_lable_)

Il nostro obbiettivo è quello di imparare un modello che mappa ogni set di attributi `x` in una dela classi `y`.

![schema_classificazione](./imgs/schema_classificazione.png)

Ci sono vari modi per effettuare la classificacazione che si dividono in 2 principali categorie:

* Base Callificacazione
    * Decision Tree :palm_tree:
    * Rule Based
    * Nearest Neigthbour
    * Neural Netwroks
    * Deep Learning
    * Naive Bayes and Bayesina Belief metods
    * Support Bector Machines
* Ensemble Classificacazione
    * Boosting
    * Bagging
    * Random Forest (:palm_tree: :palm_tree: ? :palm_tree: ?? :palm_tree:)

![decision_tree_example](./imgs/decision_tree_example.png)

ALcuni algortmi per la classificacazione basati su decison tree sono:

* Hunt's Algorithm
* CART(s)
* ID3 (volkswagen), C4.5 (Picasso Cytroen)
* SLIQ, SPRINT

#### Hunt's Algorithm

**Funzionamento**: sia Dt un set di dati di training si ha la segunete procedura:

* se Dt contiene record che apparengono alla stessa classe yt, allora t è un nodo foglia ed appartiene alla classe yt
* se Dt contiene record che appartengono a più di una classe, allora testa un attributo per dividere i dati in sottoinsiemi più piccoloi. Poi viene applicata ricorsivamente la procedura di prima.

![hunt_example](./imgs/hunt_example.png)

### Problemi di design di alberi ad induzione elettromagnetica

Due problemi principali sono: 

* la determinazione di una metodologia di split che dipende da due fattori principali:
    * specifica di una condizione di test, che dipende dal tipo di attributo
    * unità di misura per valutare la correttezza di una misura di test (quanto bene un attributo rappresenta la classe)
* determinare quando terminare la divisione:
    * fermarla anticipatamente (Eraly termination :robot:)
    * fermarla se tutti i record appartengono alla stessa classe (foglia raggiunta) oppure se hanno tutti gli attributi uguali (porteranno allo stesso risultato)

#### Metodi per effettuare i test

Questi metodi variano in base al:

* Tipo di Attributo
    * Binary
    * Nominal
    * Ordinal
    * Continussssss
* Numero di vie per lo split
    * 2 way split
    * multy way split

**Multiway or Biniary Split**:

![multi_binary](./imgs/multi_binary.png)

**Splitting di Attributi Continui**

Possono essere gestiti i 2 modi principali:

* Discretizzazione: permettono di formare categorie ordinali. Possono essere raggruppati in cluster, in insiemi di frequenze equivalenti o intervalli equivalenti. Questa divisione può essere effettuata in maniera **Statica** (solo all'inizio) o **Dinamica** (per ogni nodo)
* Decisione Binaria: esegue dei test binari come `A > v` o `A <= V`

Un possibile approccio è quello greedy che guarda l'indice di purezza della divisione delle classi:

![purezza](./imgs/purezza.png)

Indici per misurare l'impurità sono :

* GEEEEENEEEEEE Index<br> ![gini](./imgs/gini.png)
* Entropy<br> ![entropy](./imgs/entropy.png)
* Miscalssification error<br> ![error](./imgs/error.png)

**Come scegliere lo split migliore**: 

1. Calcolare l'indice di impurità `P` prima dello split
2. Calcolare l'indice di impurità `M` dopo lo split
    * `M` è l'impurità pesata dei figli
3. Scegliere l'attributo che produce il valore `Gain` maggiore: `Gain = P - M` (equivalente a scegliere l'attributo con `M` minore)


![grafo](./imgs/grafico.png)

#### Gini

`p(j|t)` è la frequenza relativa della classe j al nodo t

Il valore massimo che può assumere è `1 - 1/nc` quando i record sono distribuiti in maniera equa e quinid si ha un alto livello di impurità

Il minimo è 0.0 che implica che titti i record appartengono ad una sola classe (l'informazione più interessante)

L'indice Gini è usato negli algoritmi CART, SLIQ SPRINT

#### Entropy

L'entropia è come l'indice geany, serve per trovare lo split migliore (quello che ha valore di entropia più vicino allo 0). Questi indici però tendono a tenere in considerazione la purezza degli attributi, senza tenere conto della larghezza dell'albero.

Per aggirare questo problema viene introdotto il Gain Ration che penalizza le partizioni piccole con molti elementi.

![gain_ratio](./imgs/gain_ratio.png)

#### Pro Vs Cons

Pro:

* Costruzione poco costosa
* Incedibile velocità della classificaizone di record sconosciuti :rocket: 
* Di facile interpertazione per alberi di piccole dimenzioni
* Resistente al rumore (IP68)
* Può gestire facilmente attributi ridondanti o irrilevanit

Contro:

* lo sapzio delle decisioni piò essere esponenziale e quindi l'approccio greedeeeee non reisce spesso a trovare l'albero migliore
* Non considera le interazioni tra gli attributi
* Il confine decisionale considera solo un attributo alla volta

### Caratteristiche degli Alberi

Se viene utilizzato 1 attributo per test condition le decision baundary corrisponderanno a rette perpendicolari agli assi dei corrisponednti attributi.

![rette](./imgs/rette.png)
_Test condition con un singolo attributo_

Per avere delle decision baoudery più elaborate è necessario creare test condition che considerano attributi multiply.

![attributimultipli](./imgs/attributimultipli.png)
_Test condition con più attributi: `x + y < 1`_

## Errori

Ci sono 2 tipi di errori:

* **Training**: sono gli errori effettuati nel dataset di training  
* **Testing** o **Generalization**: sono gli errori effettuati nel dataset di testing

### Overfitting e Underfitting

![overfitting](./imgs/overfitting.png)

**Overfitting**: 
Se i dati di training sono sottorappresentativi (non rappresentano bene l'ambiente), all'aumnetare dei nodi aumentano gli errori di testing e diminuiscono gli errori di training. Aumentando la dimenzione dei data di training riduce questa differenza tra i dati ad un qualsiasi numero di nodi.

__In breve__: se vengono forniti dati che non reappresentano completamente il problema allora l'algoritmo andrà ad imaparare solamente come risolvere quelle situazioni e non riuscirà a gestirne di diverse (esempio: vengono fornite 2 razze di primati per il problema del riconscimento di scimmie, l'algoritmo impareaà a conoscere perfettamente quelle 2 razze, ma quando gli verrà presentata una nuova razza non comprednerà che è una scimmia).

Le cause dell'orvefittingo sono:

* Dimenzioni dei dati di Training limitate
* Alto livello di complessità del modello

L'overfitting porta ad avere Decision Trees molto più complessi del dovuto.
Gli errori di Training non forniscono una buona stima degli errori di Testing.

## Model Selection

Serve per assicurare che il modello non incappi in overfitting e per stimare il Generalization Error.
E' quindi necessario stimare il Generalization Error nei seguenti modi:

* Usando un Validation Set
    * E' un set di dati, diverso dal training, che serve per stimare quanto sia affidabile il modello, ma non è sufficiente per il testing (esempio dell'esame di Bartoli). Si creano e trainano più modelli differenti e con il validation set si sceglie quello più preciso.
* Incorporando il Model Complexity
    * Un alta complessità tende a causare un numero maggiori di errori, quindi, dati 2 modelli è sempre meglio preferire quallo con complessità minore. La complessitàsi equivale a: `GenError(Model) = TrainError(Model, TrainData) + a * Complexity(Model)`
* Stimando i Limiti Statistici

### Approccio pessimistico

Questa formula serve per calcolare il Generalization Error e quindi la complessità del Decision Tree

![pessimo](./imgs/pessimistico.png)
_E' equivalente alla forumla `GenError(Model) = TrainError(Model, TrainData) + a * Complexity(Model)`_

### Approccio Ottimistico

Nel caso in cui non si voglia calcolare il Generalization Error, può essere fatta una stima molto ottimistica dell'errore con il Training Error.

### PrePruning

Per evitare che un modello incappi in overfitting si può applicare la strategia del pruning: ovvero la potatura di alcune foglie per semplificare l'albero.

Il PrePruning avviene prima del completamento del Decision Tree e per decidere quando potare vengono usate dei valori di threshold che, se superati, portano all'eliminazione di un sottoalbero.

![preprunin1](./imgs/prepruning1.png)
![prepruning2](./imgs/prepruning2.png)

### PostPruning

E' simile al prepruning solo che la potatura viene effettuata solo dopo che il Decision Tree viene calcolato completamente, con modalità BottomUp.
E' più preciso del PrePruning però richiede più calcoli.

## Valutazione delle Performance di un Classificacatore

Ci sono vari modi per valutare le performance di un classificacatore:

* **Medoto Holdout**: consiste nel dividere i dati originali in 2 set: uno di training e uno di testing (la divisione è a discrezione dell'analista). Successivamente il calssificatore viene allenato col set di training e poi viene testata la sua accuratezza con il set di testing. Questo modello presenta svariati problemi: se forniamo troppi dati di testing e pochi di training, il modello potrebbe non operare al massimo delle sue potenzialità, mentre se vengono forniti troppi dati di training e pochi di testing, la stima finale potrebbe non essere affidabile al 100%. Inine, poiche i set di training e di testing sono derivati dallo stesso insieme di dati, potrebbe capitare che uno dei 2 sottoinsieme sia più rappresentatidvo del dataset orgiginale, mentre l'altro no. Per migliorare la precisione di questo metodo piò essere applicato il Random Subsampling che consiste nel ripetere più volte l'allenamento e il tesing con sottoset differenti per ogni iterazione.

* **Cross-Validation**: un'alternativa al Random Subsempling è il Cross-Validation che consisnte nel dividere il dataset in `k` partizioni di dimenzioni equivalenti e successivamente di utilizzare `k -1 ` partizioni per il training e 1 per il testing. Queste partizioni si scambieranno fin quando tutti gli elementi verranno utilizzati per il testing 1 sola volta. Un metodo speciale è il _leav on out_, che è simile al metodo descritto sopra ma ha `k = N` (dove `N` è la dimenzione del dataset) e consiste nell'usare un solo record alla volta per il tesing. Questa procedura risulta molto precisa ma molto costosa.

# Artificial Neural Network (ANN)

Le ANN si ispirano al funzionamento del cervello umano, si basano su:

* Neuroni
* Assoni
* Dendridi
* Sinapsi

Le ANN non hanno tutti questi elemnti ma solo i Neuori (Nodi) e gli Assoni (link pesati) che fungono anche da Dendridi e Sinapsi.

Il modello più semplice di ANN è chiamato Percettrone e vedremo che sarà utile per risolvere porblemi di classificazione.

## Percettrone (pompotron :robot: )

Il percettrone consiste in 2 tipo di Nodi:

* Più Nodi di Input: che rappresentano i dati di input
* Un Nodo di Output: che rappresenta l'output del modello

I nodi vengono anche chiamati Neuroni o Unità.

Ogni nodo input è connesso con il nodo outpit tramite un collegamento pesato che emula il collegamento sinaptico. Allenare dunque un percettrone vuol dire aggiustare il valore dei pesi finchè non si adattano alla relazione di input-outpu richiesta. Il risultato del neurone di output è la somma pesata di tutti i neuroni di input più l'aggiunta di un bias (threshold di attivazione)

![percettrone1](./imgs/percettrone1.png)

_Esempio di un percettrone_

Il risultato di un neuroen di output può essere scritto come:

![output_percettrone](./imgs/output_percettrone.png)

## Modello di Apprendimento del Pompotron

Come detto prima la fase di Training di un Percettrone vuol dire aggiustare i pesi dei collegamenti. La seguente formula indica come effettivamente viene aggiornato il valore dei pesi dei collegamenti:

![perceptron_learning](./imgs/perceptron_learning.png)

In modo molto intuitivo, il nuovo peso `w(k+1)` è la combinazione del vecchio peso `w(k)` e un valore proporzionale all'errore di predizione `(y - y^)`. Se la predizione è corretta (il risultato di `(y - y^)` è `0`) allora il peso rimane invariato. Altrimenti viene modificato nel seguente modo:

* Se `y = +1` e `y^ = -1` : l'errore è dunque uguale a `2` e per compensare l'errore bisogna aumentare il peso dei link positivi e diminurie il peso dei link negativi.

* Se `y = -1` e `y^ = +1`: l'errore è dunque uguale a `-2` e per compensare l'errore bisogna diminuire il peso dei link positivi e aumentare il peso dei link negativi.

Lambda è chiamato _Learning Rate_, che è un valore che varia tra 0 e 1 e serve per controllare quanto fini devo essere gli aggiustamenti durante il processo di learning. Se lambda è più vicino a 0, i nuovi pesi variano meno rispetto a quelli precedenti. Se è più vicina ad 1, i nuovi pesi possono variare molto rispetto a quelli vecchi. Alcune volte si può usare il valore lambda in modo adattivo: all'inizio sarà più vicino ad 1 in quanto "deve imparare di più" per poi avvicinarsi sempre più allo 0 pere effettuare delle piccole modifiche per raggiungere la precisione.


Il percettrone sa fare operazioni di classificazione solo se  i dati sono linearmente separabili, altrimenti è necessario aumentare la complessità del percettrone aggiungendo degli Hidden Layer.

I set di dati linearmente separabili possono essere visti come un Hyperpiano che può essere separato da una retta. L'algoritmo di leraning del percettrone converge in problemi linearmente separabili, altrove non converge.
La funzione XOR non è lineramente separabile.

![ipercubo](./imgs/ipercubo.png)

## MultyLayer ANN

Per creare strutture più complesse per classificare dati non linearmente divisibili si possono utilizzare 2 metodi:

* Il primo è quello di inserire vari livelli, detti _Hidden Layer_, tra il livello di input e quello di outpt. La struttura risultante si chiama **MultyLayer Neural Network** può essere distinta in base ai link tra i livelli in 2 categorie:
    * Feed-Forward, dove i noodi in un livello possono solamente connettersi al livello successivo
    * Recurrent, dove i link possono connettere nodi tra lo stesso livello o tra un livello precedente.

![mnn](./imgs/mnn.png)

* Il secondo è quello di utilizzare funzioni di attivazioni diverse da quella segno, come funzioni lineari, sigmoidi, tangente, ecc..
Queste funzioni di attivazione permettono ai nodi nascosti e di output di produrre valori di output che hanno valori di input non lineari (come la funzione XOR).
![funzioni](./imgs/funzioni.png)


![xor](./imgs/xor.png)

_MNN per classificazione di funzione XOR_

### Learning per ANN

<!-- 
Lo scopo dell'algoritmo di learning di un ANN è quello di determinare un seti di pesi che deve minimizzare la somma totale degli errori quadratici:

![quadratici](./imgs/quadratici.png)
-->

Il processo di learning si basa sul continuo aggiustamento dei pesi e dei bias, che vengono ricalcolati tramite una funzione costo che varia da implementazione ad implementazione.

Quella più utilizzata è la Gradient Descent che utilizza il gradiente(rappresenta il cammino più ripido verso l'alto) invertito per raggiungere dei minimi locali dell'errore.

Tramite la tecnicla del Back-Propagation si utilizza l'errore nel layer di output per modificare i pesi e i bias degli hidden layer.

![differenziali](./imgs/differenziale.png)

### Convolutional Neuarl Network

Questo tipo di rete neurale ha dei layer chiamati Convolutional che hanno a disposizione una matrice detta kernel che verrà sovrapposta ai pixel dell'immagine di input generando una nuova immagine "filtrata" che verrà poi utilizzata dagli hidden layer successivi.
Questo filtraggio serve per trovare pattern e più la rete sarà profonda e più questi pattern saranno complessi (si va da linee e cerchi, fino a volti e animali)

![kernel](./imgs/kernel.png)

## Problemi di Design delle ANN

Quando si sviluppa una ANN bisogna tenere in cosiderazione questi problemi di design:

* Il numero di nodi di input deve essere determinato, solitamente bisogna creare un nodo di input per ogni variabile, tuttavia, per le variabili categoriche è accettabile codificarle in una variabile k-arry avente `int_sup(log2(k))` nodi di input.

* Il numero di nodi di output deve essere prestabilito: per un problema a 2 calssi basta un solo nodo di output, ma per un problema con k classi ne servono k

* Deve essere scelta una topologia per la rete poichè essa andrà ad influenzare la target function. Per scegliere la giusta topologia si può procedere in 2 modi:
    1. Creare una fully connected network e iterarci sopra per costriure una nuova rete ogni volta con un numero minore di nodi (si reitera la procedura di model-buildin e ha una complessità di tempo mooolto alta)
    2. Creare una fully connected network e togliergli nodi per poi ripetere il processo di valutazione della rete.

* Vanno inizializzati i pesi e i bias. E' comunemente accettata una inizializzazione randomica

* Gli esempi di trainign con valori mancanti dovrebbero essere sostituiti o rimossi

## Nearest Neightor Classification

Esistono dei tipi di algoritmi di learning che non costruiscono un modello a priori per classificare i dati ma che li classificano solamente nel momento del bisogno, essi sono detti leazy learners. Un esempio è il Rote Classifier che si ricorda tutti i suoi esempi di training e una volta passati dei dati di testing li calssifica solo se corrispondono esattamente a dati già visti nella fase di training. Questo implica una scarsa flessibilità nella classificazione. E' stato quindi ideato un approccio più generale chiamato Nearest Neighto Classifire.

Esso si basa sullo stesso concetto della Rote Classifire ma non guarda l'equivalenza ma la similarità tra il dato di testing e quelli di training, ovvero cerca i vicini più vicini al record di testing.

I dati con n attributi vengono rappresenati su uno spazio ndimenzionale e la precisione della classificazione dipende da una variabile distanza `k`. Ci sono altre varianti di questo algoritmo che alternao il modo di determinare i vicini più vicini basandosi non solo sulla distanza ma anche sulla _classe di maggioranza_

![near](./imgs/near.png)

oppure sulla _classe di maggioranza con distanze pesate_ dove non conta solamente la classe che compare più volte ma anche la sua distanza dal record di testing (più lontano sarà e minore sarà l'importanza).

![voronoioioioioi](./imgs/voronoi.png)
![euclide](./imgs/euclide.png)

_Diagramma di Voronoi per 1-nearest Neightbotr e Distanza Euclidea_

### Vantaggi e Svantaggi in breve

* Non hanno bisogno di manterere un modello astratto derivato dai dati
* Non richiedono model building ma richiedono più computazione degli eager learner nella fase di testing
* Poichè fanno classificazioni basate su informazioni locali sono molto suscettibili al rumore
* Poichè possono genereare decision boundaries arbitrariamente dispongono di una maggiore flessibilità rispetto agli eager lerner
* Possono generare errori di classificazione se non avvengono step di preprocessing (aggiustamento delle scale dei dati)

## Bayesian Classification

Un classificatore bayesiano basa il suo processo di learning su un importatne teoria statistico: Il teorema di Bayes.

![bayes](./imgs/bayes.png)

Questo teorema fornisce un modo per revisionare delle predizioni o teorie esistenti, aggiornandone le probabilità in seguito alla scoperta di informazioni aggiuntive.
Il teorema afferma che: la _probabilità a posteriori_ `P(Y|X)` è data dal prodo dotto della _probabilità condizionale di classe_ `P(X|Y)` per la _probabilità a priori_ `P(Y)` fratto le _nuove inofrmazioni_ `P(X)`

**N.B.** quando si confrontano varie probabilità per differenti valori di Y, il denominatore può essere ignorato.

Tale teorema può essere applicato da un algoritmo di ML in due modi in base a come viene implementato il calcolo della _probabilità condizionale di classe_:

* Naive 
* Belif Network

Per la classificazione si va a vedere il valore più alto tra le varie probabilità a posteriori `P(Y|X)` e la classe con probabilità maggiore sarà la vincente.

### Naive Bayesin Calssifier

Il metodo Naive calcola il valore di `P(X|Y)` nel seguente modo:
![produttoria](./imgs/produttoria.png)

Va però fatta una distinzione in base ai tipi di attributo che si prendono in considerazione:

* **Categorici**: si calcola il rapporto tra il numero di volte che l'attributo compare all'interno dei record che contengono la classe in questione fratto il numero di volte che compare la classe Y in questione

* **Continui**: per trattare questi dati si può procedere in 2 modi diversi:
    * **Discretizzando**: si dividono i dati in intervalli più piccoli trasformando quindi l'attributo continuo in un attributo categorico e si procede come visto sopra. Bisogna fare attenzione a come vengono scelti gli intervalli: troppo grandi sono poco precisi e troppo piccoli causano overfitting

    * **Utilizzano le distrubuzioni di Probabilità**: si cerca una distribuzione di probabilità più adatta alle variabili continue e si stimano i parametri della distribuzione usando i dati di training. Generalmente la ditribuzione Gaussaina è la più utilizzate e quindi ne deriva la seguente formula: ![gauss](./imgs/gauss.png)
 
Se una probabilità condizionale è `0` allora verrà azzerata tutta l'espressione. Per questo motivo sono state implementate delle variazioni che permettono di evitare il problema:

![variazioni](./imgs/variazioni.png)

#### In Bveve

* Sono resistenti a punti di rumore isolati che vengono cancellati durante i calcoli
* Sono resistenti ad attributi irrilevanti
* Le performance vengono peggiorate da attributi correlati perchè non esiste più l'assunzione dell'indipendenza condizionale (per risolvere questo problema si usa il BBN spiegato dopo)

### Bayesian Belife Netowrk

Se sono presenti degli attributi correlati questo algoritmo offre performance migliori. Esso fornisce una rappresentazione grafica delle relazioni probabilistiche tra un insieme di variabili random tramite un DAG (Grafo Orentato Aciclico).
A seconda del numero di nodi padri viene fatta una distinzione:

* Se non ha genitroi allora contiene la probabilità a priori `P(X)`

* Se ha 1 solo genitore, contiene la probabilità condizionale `P(X|Y)`

* Se ha più genitori, contine la probabilità condizione `P(X|Y1, Y2, ..., Yn)`
![dag](./imgs/dag.png)

Queste probabilià vengono poi inserite in una tabala relativa ad ogni nodo. Durante la classificazione vengono presi questi valori per caloclare la classe di appartenenza.

#### In Bveve

* Permette la visualizzazione grafica tramite un DAG
* La prima costruzione richiede molto tempo e risorse, ma una volta costruito è di facile gestione
* Gestiscono facilmente i dati incompleti (attributi mancanti)
* Resistente al Model Overfitting