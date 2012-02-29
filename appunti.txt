---
layout: default
title: Architettura degli elaboratori
---

22/02/12 - Rappresentazione dell'informazione
=============================================

La memoria è finita

L'elemento di memoria è il bit (0,1)
I bit si raggruppano in:
    -  4 bit -> nibble
    -  8 bit -> byte
    - 16 bit -> word
    - 32 bit -> double word
    - 64 bit -> quad word

Con un gruppo di n bit ho a disposizione 2^n valori
Codifiche:
    - caratteri (ASCII)
    - tonalità di grigio
    - colori
    - codifiche compresse

    - **NUMERI**
        - Naturali
        - Interi
        - Razionali
        - Reali -> Non possono essere rappresentati nei calcolatori
        - Complessi -> Tanto meno

Come rappresento con memoria finita infiniti numeri? Non posso
Posso rappresentare numeri molto grandi
Ho due limiti:
    - Numero massimo e minimo che posso rappresentare
    - Minima distanza tra due numeri rappresentabili (risoluzione)

Rappresentazione binaria
Un numero P si può rappresentare come
    P = b_0*2^0 + b_1*2^1 + ... + b_(n-1)*2^(n-1)
Che n mi serve?
    2^n > P
    log_2(2^n) > log_2(P)
    n*log_2(2) > log_2(P)
    n > log_2(P)
Conversione base10 -> base2
    Prendo i resti delle successive divisioni per 2

Rappresentazione esadecimale
Gruppi di 4 bit corrispondono ad una cifra esadecimale
Cifre Hex: 0 1 2 3 4 5 6 7 8 9 A B C D E F
    Esempio: 1000 0001 _2
              8    1   _16
                   129 _10
Conversione base10 -> base16
    Prendo i resti delle successive divisioni per 16

Nella somma tra naturali (unsigned int) posso avere un risultato
non rappresentabile (overflow), in questo caso troverò settato
il bit CF (carry flag) del processore.

Rappresentazione degli interi...
    1. Il primo bit rappresenta il segno
    o
    2. Usare l'aritmetica modulare (orologio)
L'opposto di un numero è: il suo complemento bit a bit + 1
La valutazione della correttezza del risultato è più complicata
Es: 6 + 3       0 1 1 0 +
                0 0 1 1 =
                ---------
                1 0 0 1  <=>  -1 ## Sbagliato
Devo verificare che non ci siano inconsistenze nei segni



27/02/12 - Valutazione delle prestazioni
========================================

Differenza tra velocità (tempo medio di risposta) e throughput

Spesso quando si aumenta il clock lo si fa a spese della complessità
delle istruzioni base (e quindi aumenta il n° di istruzioni necessarie
ad eseguire un dato compito) [vedi CISC vs RISC]

Tempo CPU = Cicli clock / Frequenza clock

CPI = n° medio di Cicli Per Istruzione
Tempo CPU = Istruzioni * CPI * T_clock
            
            Istruzioni * CPI
          = ----------------
            Frequenza Clock

Rendere efficiente l'algoritmo significa:
* Usare meno istruzioni
* Usare le istruzioni più veloci (ridurre il CPI)

Il compilatore cerca di ottimizzare, tenendo conto anche di effetti
complessi (es. pipeline e caching)

ISA = Instruction Set Architecture
* Influisce su n° istruzioni, CPI e frequenza

Efficienza energetica
Potenza consumata = Capacità * Tensione^2 * Frequenza
Tensione: 5V (TTL) -> 1.2V (CMOS)
Non si può abbassare ancora (aumenterebbero troppo le correnti parassite)



29/92/12 - Aritmetica dei calcolatori
=====================================

Divisioni e moltiplicazioni per 2*n equivalgono a shift a destra/sinistra

Moltiplicazioni in comp. a 2:   -1 = 1111 * 2
                                -2 = 1110 * 2
                                -4 = 1100 * 2
                                -8 = 1000 * 2
Si inserisce a destra 0
Funziona sempre se sono all'interno del range di rappresentabilità

Divisioni in comp. a 2: Si inserisce a sinistra il bit di segno (se appl.)

Moltiplicazioni tra naturali: in colonna; per numeri di n bit ne servono 2n
Molt.           tra interi: bisogna "estendere" i numeri in comp. a 2
es. 0110 -> 00000110
    1010 -> 11111010 (si copia il bit del segno)
    (la correttezza si dimostra per induzione)

es.         1101 *
            0010
    -------------
        00000000
       11111101
      00000000
     00000000
   --------------
       111111010 --comp--> -00000110 = -6 OK

Divisioni tra naturali:
es. 11010010 / 110 = 100011
    110
    0001
       10
       100
       1001
        0110
         000
   (210 / 6 = 35)


=== Virgola fissa ===

11.01 = 3 + 0*2^-1 + 1*2^-2 = 3.25

3.25 = ?
Per la parte intera è uguale
Per la parte decimale 
