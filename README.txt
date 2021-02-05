Il codice riguardante l'elaborato è essenzialmente suddiviso in sezioni, e separate da markdown nel notebook e può essere eseguito senza difficoltà su jupyter notebook /jupyter lab.

Le varie sezioni comprendono:
-sezione 1: 
codice per la rappresentazione di variabili con i loro rispettivi dominii, dei vincoli e di un generico problema CSP a dominio finito ;

-sezione 2: 
implementazione della classe Solver contenente la funzione MinConflicts e le varie funzioni ausiliarie al funzionamento, che implementa l'algoritmo su cui si sta effettuando lo studio ;

-sezione 3: 
definizione del costruttore del problema delle n regine, la funzione NQueensConstructor necessita solo del parametro n (il numero di regine) e sulla base di questo procede alla costruzione delle variabili del problema e dei suoi vincoli, restituendo infine un'oggetto di classe Problem che potrà essere poi risolto tramite il solver

-sezione 4: 
codice per la costruzione di un grafo casuale a partire dal numero di nodi secondo la tecnica riportata nell'eserczio  6.10 in R&N 2009;

-sezione 5: 
definizione del costruttore del problema del map coloring, la funzione mapConstructor necessita solo del parametro n (il numero di regioni) e k (il numero di colori utilizzabili) e sulla base di questi valori procede del grafo casuale e sulla base di esso alla costruzione delle variabili del problema e dei loro vincoli, restituendo infine un'oggetto di classe Problem che potrà essere poi risolto tramite il solver;

-sezioni 6 e 7: 
piccoli test di funzionamento delle funzioni precedentemente descritte, in particolare sulla base della  definizione del parametro n (e k nel mapColoring), si può andare a costruire una istanza per ognuno di questi problemi e tentarne la risoluzione tramite il solver, dopo la risoluzione sullo schermo vengono rappresentate rispettivamente:
la scacchiera con la posizione delle regine all'interno di essa e il numero di conflitti tra le regine nella attuale configurazione;
il grafo delle regioni con scritto all'interno di ogni nodo un numero rappresentante il colore e anche per questo problema il numero di conflitti nella configurazione attuale.
in entrambe le sezioni è possibile testare il funzionamente del codice del risolutore e dei costruttori andando a assegnare un valore al parametro n (e k) e al numero di step massimi effettuabili dal solver poi eseguendo la sezione essendosi prima assicurati che le sezioni precedenti siano state eseguite almeno una volta;

-sezione 8 e 9:
test e studio del tempo di esecuzione (quantificato in numero di operazioni) in base all'aumentare della dimensione del problema, in seguito all'esecuzione della sezione viene riportato un grafico in cui sono visualizzate le relazioni tra dimensione del problema e numero di operazioni necessarie per risolverli.

CREAZIONE DI UN NUOVO PROBLEMA CSP

CREARE UNA VARIABILE

Per creare un oggetto di classe variabile si deve invocare il metodo init di quest'ultima,
il metodo prende in ingresso 2 elementi:
-un elemento "tag" di qualsiasi tipo confrontabile che farà da identificatore univoco della variabile all'interno del problema
-un set di elementi (generalmente una lista) che rappresenti il dominio della variabile


CREARE UN VINCOLO 

Per creare un oggetto di classe vincolo si deve invocare il metodo init di quest'ultima, il metodo prende in ingresso 2 argomenti:
-un set di variabili (generalmente una lista di oggetti di classe variabile)
-la condizione del vincolo che deve essere espressa tramite una funzione lambda in modo che questa possa essere invocata in seguito per verificare tramite il metodo verify se le variabili soddisfano il vincolo

un piccolo esempio ripreso dal codice:

Constraint([nQueens.variables[i],nQueens.variables[j]], lambda a: a[0].value!=a[1].value);

AGGIUNGERE UNA VARIABILE AL CSP

Una volta inizializzato un oggetto di classe problema (non necessita argomenti in quanto inizialmente il problema contiene una lista vuota di variabili e vincoli) è possibile aggiungere una variabile al problema tramite il metodo add_variable che prende in ingresso una variabile e la "appende" alla lista delle variabili

AGGIUNGERE UN VINCOLO AL CSP

E' possibile inoltre aggiungere un vincolo al problema tramite il metodo add_constraint che prende in ingresso un vincolo definito sulle variabili del problema e lo "appende" alla lista dei vincoli

RISOLZUIONE DEL CSP TRAMITE MIN CONFLICT

Una volta creato un problema si può creare un oggetto di tipo solver,l'oggetto prende in ingresso per la sua inizializzazione un oggetto di classe problema 
Sul solver a questo punto può essere invocato il metodo min_conflicts che prende in ingresso il numero di step massimi eseguibili e restituisce una tupla di 3 elementi :
-il primo elemento è il problema da risolvere con le variabili assegnate
-il secondo elemento è il numero di conflitti nello stato attuale del problema
-il terzo elemento è il numero di passi eseguiti dal metodo min_conflicts

TESTARE IL CODICE

Al fine di poter testare il funzionamento del codice sarà necessario eseguire in sequenza le 9 sezioni in cui è suddiviso il programma.
Le sezioni da 1 a 5 servono solo per poter definire i codici.

La sezione 6 permette di testare la costruzione e risoluzione del problema delle n regine, al fine di ottenere un output basterà indicare nel codice la dimensione della variabile n e quanti passi far eseguire al metodo minconflict.
A schermo verrà stampata la configurazione della tastiera dopo la risoluzione e il numero di conflitti

La sezione 7 permette di testare la costruzione e risoluzione del problema del map coloring, al fine di ottenere un output basterà indicare nel codice la dimensione della variabile n,il numero di colori k e quanti passi far eseguire al metodo minconflict.
A schermo verrà stampata la configurazione della mappa visualizzata come grafo dopo la risoluzione e il numero di conflitti

La sezione 8 e 9 analizzano i dati, anche qua basterà eseguire il codice dopo aver impostato dimensione massima raggiungibile e (numero di colori per il map coloring) per veder visualizzato a schermo dopo un pò di attesa i grafici di analisi.

FONTI ESTERNE PER SEGMENTI DEL CODICE

Al fine di implementare la funzione intersect che determina se due segmenti si intersecano o meno (utile nella costruzione di un grafo a partire da n punti ), il codice della realizzazione della funzione e dei metodi ausiliari per essa sotto riportati sono stati reperiti dalle seguenti pagine web:
Al di fuori delle seguenti parti il resto del codice dell'elaborato è stato sviluppato in totale autonomia.

https://algorithmtutor.com/Computational-Geometry/Determining-if-two-consecutive-segments-turn-left-or-right/

https://algorithmtutor.com/Computational-Geometry/Check-if-two-line-segment-intersect/


def subtract(self, p2):
        return Point(self.x - p2.x, self.y - p2.y);

def cross_product(p1, p2):
    return p1.x * p2.y - p2.x * p1.y;

def direction(p1, p2, p3):
    return  cross_product(p3.subtract(p1), p2.subtract(p1));


def on_segment(self, p):
        p1=self.e1;
        p2=self.e2;
        return min(p1.x, p2.x) < p.x < max(p1.x, p2.x) and min(p1.y, p2.y) < p.y < max(p1.y, p2.y);
        
    def intersect(self,other):
        p1=self.e1;
        p2=self.e2;
        p3=other.e1;
        p4=other.e2;
        
        d1 = direction(p3, p4, p1)
        d2 = direction(p3, p4, p2)
        d3 = direction(p1, p2, p3)
        d4 = direction(p1, p2, p4)

        if ((d1 > 0 and d2 < 0) or (d1 < 0 and d2 > 0)) and ((d3 > 0 and d4 < 0) or (d3 < 0 and d4 > 0)):
            return True

        elif d1 == 0 and other.on_segment(p1):
            return True
        elif d2 == 0 and other.on_segment(p2):
            return True
        elif d3 == 0 and self.on_segment(p3):
            return True
        elif d4 == 0 and self.on_segment(p4):
            return True
        else:
            return False


