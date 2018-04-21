### Crea da zero un clone di Bitcoin

Cosa ci serve?

 - Python 3 installato
 - Il programma "python" eseguibile da terminale ("cmd" su Windows)
 - Un editor di testo per programmatori

<style> .slides:first-child { font-size: 75% !important; } </style>

---

## Benvenuti al workshop!

 > "I had to write all the code 
 > before I could convince myself that I could
 > solve every problem"

 > "Ho dovuto scrivere da zero tutto il codice,
 > per convincermi che potevo risolvere ogni problema"

__*L'autore di Bitcoin.*__

<style> .slides:nth-child(2) { background-color: red!important; } </style>

---

## Rigel Di Scala
### Digital Architect
![Logo](assets/wd.png)

Per contattarmi: https://linkedin.com/in/rigeldiscala

---

![](assets/chiedimi.png)

---

## Obiettivi del workshop

 - Capire come funziona Blockchain e le criptomonete
 - Creare un piccolo clone di Bitcoin:
 - Divertirci

---

## Programma

 - Abbiamo 3 ore e mezza
 - 3 sessioni da un'ora e 3 pause di 10 minuti
 - Le domande sono benvenute in qualsiasi momento

---

## Metodo

 - Python 3 (ovviamente)
 - Scriveremo **tutto** da zero

---

## Cos'è il denaro?

 - una riserva di valore |
 - un mezzo di scambio |
 - un'unità di conto |

---

## ... e il valore del denaro?

 - deriva la sua scarsità |
 - corrisponde ad un bene materiale |
 - corrisponde a un debito |

---

## Domanda

Cosa ci impedisce di creare la nostra moneta personale?

---

 > Dobbiamo risolvere tre problemi fondamentali:
 > 1. Come scambiare informazioni in rete con sconosciuti e in maniera anonima
 > 2. Come creare identità autentiche che possono riscuotere il credito
 > 3. Come inviare informazioni da una identità all'altra, globalmente e in perfetta sicurezza

__*Pieter Hintjens*__, "Hacking the Edges"

---

## Di cosa abbiamo bisogno?

 - Uno o più computer
 - Una rete di comunicazione
 - Un protocollo comune
 - ... e forse qualcos'altro...

---

## Atto Primo: la rete peer-to-peer

 > La privacy è necessaria per una società aperta nell'era digitale. 
 > Non possiamo aspettarci che i governi, le aziende o altre grandi organizzazioni senza volto ci concedano la privacy.
 > Dobbiamo difendere la nostra privacy se ci aspettiamo qualcosa. 
 
 > I cypherpunk scrivono il codice. Sappiamo che qualcuno deve creare i software per difendere la privacy, e ... lo stiamo facendo.
 > Il software non può essere distrutto, e un sistema decentralizzato non può essere smantellato.

__*Eric Hughes*__, A Cypherpunk's Manifesto

---

Esempi di sistemi decentralizzati che non possono disattivati? 

---

## Radio

 - Informazioni audio trasmesse usando l'energia elettromagnetica
 - Chiunque abbia un sistema radio full-duplex puo ricevere e inviare segnali
 - I tuner radio si sintonizzano sulla banda 3kHz - 300GHz

![](assets/radiolondra.jpg)

---

In Italia, la banda cittadina si trova attorno ai 27 mHz, usata principalmente dagli autotrasportatori.

![](assets/cb2.jpg)
---

![Video](https://www.youtube.com/embed/8lNFfRR73iU)

---
## Stazioni numeriche
### (Number stations)

Usano il sistema crittografico chiamato "Il cifrario di Vernam" o "one time pad", dalla segretezza perfetta.

![](assets/otp.jpg)

---

![](assets/otp2.png)

Note:
Le stazioni numeriche sono esempi di reti decentralizzati che usano la crittografia per comunicare in maniera sicura.

---

## Nel nostro caso...

 - Un protocollo (la frequenza, il linguaggio, etc..) |
 - Un client (il sintonizzatore radio) |
 - Un mezzo di trasporto dati, il TCP/IP (l'etere) |

---

## Riscaldamento: il REPL

```
10 READ
20 EVAL
30 PRINT
40 GOTO 10
```

![](assets/repl.png)

---

`Cos'è Internet? Un mucchio di protocolli!`

__*Pieter Hintjens*__, FOSDEM '13

---

## Il protocollo (v0.1.0)
### REPL
Lo script esegue un loop infinito che chiede input interattivo all'utente, 
nel formato `COMANDO ARGOMENTI`, ad esempio `echo ciao`. L'unico comando supportato e' `echo` che stampa il comando sul terminale.

#### Requisiti

 - Script chiamato "main.py"
 - Invoca `main()` automaticamente
 - Usiamo `input()` per chiedere all'utente di digitare un comando
 - Un unico comando eseguibile `echo`

Cheat mode: https://tinyurl.com/pyconnove1 

---

## La rete
### Il broadcasting dei messaggi sulla rete

 - Siamo tutti collegati alla stessa rete
 - Possiamo *broadcastare* messaggi tra di noi
 - Dobbiamo solo accordarci su un protocollo per la comunicazione (v0.2.0)

---

## Where to send our messages

 - Apriamo il terminale
 - Inseriamo:
    `ipconfig` su Windows
    `ifconfig` su Linux/Mac OS

### Esempio
```
inet addr:192.168.0.115  
Bcast:192.168.0.255 
Mask:255.255.255.0
```

---

![](assets/broadcast.png)

---

### Server

Usando il netcat tradizionale (non OpenBSD) su Linux: 

```
nc -ulk -p 8000
```

Su OSX:

```
nc -ul 8000
```

### Client

Su Linux:

```
echo "hello" | nc -b -u 192.168.0.255 8000
```
---

## Mille modi per programmare in UDP con Python... e noi useremo...

---

## ASYNCIO
### Segue brevissima introduzione

Note:
Una delle librerie Python più popolari in Sardegna...

---
## Asyncio

 - Il modulo standard in Python 3 per la programmazione asincrona |
 - Ruota (*ahah*) attorno al concetto di **event loop** |
 - Mettiamo in moto il *loop* e gli diamo compiti ( *task* ) da eseguire |
 - Oppure possiamo chiedergli rimanere in ascolto e chiamarci se succede qualcosa di interessante |

---

## Mostrami il codice!

```python
import asyncio

async def f(uid):
    await asyncio.sleep(uid ** 2)
    print(uid)

loop = asyncio.get_event_loop()
loop.run_until_complete(asyncio.gather(
    f(2),
    f(1)
))
loop.close()
```

---
