# Calamus Automaticus

![Brevetto meccanico](https://img.shields.io/badge/BREVETTO%20MECCANICO-1.2-b8860b)
![Licenza](https://img.shields.io/badge/licenza-AGPL--3.0-blue)
![Linguaggio](https://img.shields.io/badge/linguaggio-Logo-informational)
![Lingue](https://img.shields.io/badge/comandi-italiano%20%7C%20inglese-informational)
![HTML5](https://img.shields.io/badge/HTML5-canvas-e34f26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-vanilla-f7df1e?logo=javascript&logoColor=black)
![Web Audio](https://img.shields.io/badge/audio-Web%20Audio%20API-informational)

Interprete Logo in un unico file HTML, con grafica a tartaruga in versione steampunk: un automa-pantografo traccia su un foglio le figure descritte da un programma. I comandi si scrivono in inglese o in italiano. Il linguaggio è un sottoinsieme del nucleo di FMSLogo. Machina N° 009 della serie OFFICINA DEGLI ENIGMI. Il nome è provvisorio.

**BREVETTO MECCANICO 1.2 – 1894**

[Puoi giocarci qui](https://tagtthespellcaster.github.io/Calamus-Automaticus/)

## Requisiti

- Un browser moderno con supporto per HTML5 Canvas e Web Audio.
- Nessuna installazione, nessuna dipendenza, nessuna risorsa esterna, nessun file audio: i suoni sono sintetizzati dal browser. Non c'è colonna sonora.

## Avvio

Aprire `calamus-automaticus.html` nel browser (doppio clic, oppure `File > Apri`). Con un server statico qualsiasi funziona allo stesso modo:

```
python3 -m http.server 8000
```

e poi `http://localhost:8000/calamus-automaticus.html`.

Il browser attiva l'audio solo dopo un'azione dell'utente: il suono parte al primo clic, tocco o tasto premuto.

## Come si usa

- **Programma:** nell'area di testo si scrive il programma. **ESEGUI IL PROGRAMMA** (oppure `Ctrl+Invio` nell'editor) lo esegue da capo: azzera lo schermo, le variabili e le procedure, poi esegue il testo.
- **Riga di comando:** sotto l'editor si può scrivere un singolo comando e premere Invio. Il comando viene eseguito subito, senza azzerare nulla: l'automa, le variabili e le procedure del programma restano quelle di prima. Con le frecce su e giù si richiamano i comandi precedenti.
- **Console:** mostra l'output di `PRINT`, `SHOW` e `TYPE` e i messaggi d'errore. In caso di errore, il disegno eseguito fino a quel punto resta sullo schermo.
- **STOP** interrompe l'esecuzione in corso; **PULISCI SCHERMO** cancella il disegno e riporta l'automa al centro.
- **Velocità:** lenta, normale, veloce o istantanea (il disegno compare subito).
- **Pulsanti di scorciatoia** sotto l'editor inseriscono comandi frequenti nel punto in cui si trova il cursore, nel lessico scelto con il pulsante **LESSICO DEI PULSANTI** (italiano o inglese).
- **Guida ai comandi:** una tabella ripiegabile, in fondo alla pagina, con tutti i comandi nelle due lingue.

### Il foglio

Il centro del foglio è la posizione 0 0, con y positiva verso l'alto. La direzione 0 è verso l'alto e gli angoli crescono in senso orario (90 è a destra). Il foglio misura 960 × 560 unità: il disegno fuori da questi limiti non si vede (non sono previsti `WRAP` né `FENCE`). I colori numerati da 0 a 15 seguono la tavolozza di FMSLogo; si possono anche usare nomi come `"red` e `"rosso`, oppure una lista `[rosso verde blu]` con valori da 0 a 255.

### Lingue

Ogni comando ha un nome inglese e uno italiano, e le due lingue si possono mescolare nello stesso programma. Maiuscole e minuscole sono equivalenti. `TO nome ... END` si scrive anche `PER nome ... FINE`.

- I nomi inglesi sono quelli di FMSLogo (con le abbreviazioni più comuni: `FD`, `BK`, `RT`, `LT`, `PU`, `PD`, `HT`, `ST`, `CS`, `SETH`, `SETPC`, `PR`, `OP`, `BF`, `BL`).
- Nomi italiani confermati: FMSLogo ha una localizzazione italiana; dalle segnalazioni pubbliche di errori risultano `AVANTI`, `INDIETRO` e le abbreviazioni `A` e `I`. Sono gli unici nomi italiani confermati.
- Tutti gli altri nomi italiani sono provvisori: l'elenco ufficiale non è stato consultato e potrebbe differire. La tabella degli alias è separata dal resto dell'interprete e si può sostituire.
- In italiano `SE` significa `IF`. L'abbreviazione inglese `SE` (`SENTENCE`) non è disponibile: si usa `SENTENCE` o `FRASE`.
- Una procedura può avere lo stesso nome di un alias italiano (che viene sostituito), ma non quello di un comando inglese.

## Comandi

**Movimento**

| Inglese | Italiano | Dati | Effetto |
|---------|----------|------|---------|
| `FORWARD`, `FD` | `AVANTI`, `A` | `distanza` | Avanza della distanza indicata, in passi (unità del disegno). |
| `BACK`, `BK` | `INDIETRO`, `I` | `distanza` | Arretra della distanza indicata. |
| `RIGHT`, `RT` | `DESTRA` | `gradi` | Ruota in senso orario. 90 gradi sono un quarto di giro, 360 un giro completo. |
| `LEFT`, `LT` | `SINISTRA` | `gradi` | Ruota in senso antiorario. |
| `HOME` | `CASA` |  | Torna al centro dello schermo, rivolto verso l'alto. |
| `SETXY` | `IMPOSTAXY` | `x y` | Va alla posizione x y (il centro è 0 0; y positiva verso l'alto). Disegna se la penna è abbassata. |
| `SETX` | `IMPOSTAX` | `x` | Cambia solo la coordinata x. |
| `SETY` | `IMPOSTAY` | `y` | Cambia solo la coordinata y. |
| `SETPOS` | `IMPOSTAPOS` | `[x y]` | Come SETXY, ma con una lista. |
| `SETHEADING`, `SETH` | `IMPOSTADIREZIONE` | `gradi` | Imposta la direzione: 0 verso l'alto, 90 verso destra, 180 verso il basso, 270 verso sinistra. |

**Penna**

| Inglese | Italiano | Dati | Effetto |
|---------|----------|------|---------|
| `PENUP`, `PU` | `ALZAPENNA` |  | Solleva la penna: i movimenti successivi non lasciano traccia. |
| `PENDOWN`, `PD` | `ABBASSAPENNA` |  | Abbassa la penna: i movimenti lasciano traccia. |
| `SETPENCOLOR`, `SETPC` | `IMPOSTACOLOREPENNA` | `colore` | Colore della penna: numero da 0 a 15 (0 nero, 1 blu, 2 verde, 3 ciano, 4 rosso, 5 magenta, 6 giallo, 7 bianco, 8 marrone, 9 sabbia, 10 verde scuro, 11 acqua, 12 salmone, 13 viola, 14 arancione, 15 grigio), un nome come "red o "rosso, oppure una lista [rosso verde blu] da 0 a 255. |
| `SETPENSIZE` | `IMPOSTASPESSOREPENNA` | `spessore` | Spessore del tratto (da 1 a 40). |
| `SETSCREENCOLOR`, `SETSC` | `IMPOSTACOLORESFONDO` | `colore` | Colore del foglio. I colori si indicano come in SETPC. |
| `HIDETURTLE`, `HT` | `NASCONDIAUTOMA` |  | Nasconde l'automa (il disegno resta). |
| `SHOWTURTLE`, `ST` | `MOSTRAAUTOMA` |  | Mostra l'automa. |
| `CLEARSCREEN`, `CS` | `PULISCISCHERMO` |  | Cancella il disegno e riporta l'automa al centro. |
| `CLEAN` | `PULISCI` |  | Cancella il disegno senza spostare l'automa. |
| `LABEL` | `ETICHETTA` | `testo` | Scrive un testo sul disegno, nella posizione dell'automa. |

**Stato**

| Inglese | Italiano | Dati | Effetto |
|---------|----------|------|---------|
| `XCOR` | `COORDX` |  | Coordinata x attuale. |
| `YCOR` | `COORDY` |  | Coordinata y attuale. |
| `POS` | `POSIZIONE` |  | Posizione attuale come lista [x y]. |
| `HEADING` | `DIREZIONE` |  | Direzione attuale in gradi. |
| `PENDOWNP`, `PENDOWN?` | `PENNA?` |  | VERO se la penna è abbassata. |
| `PENCOLOR`, `PC` | `COLOREPENNA` |  | Colore attuale della penna. |
| `TOWARDS` | `VERSO` | `[x y]` | Direzione da prendere per puntare verso la posizione indicata. |
| `REPCOUNT` | `CONTARIPETIZIONI` |  | Numero della ripetizione in corso dentro REPEAT (1, 2, 3...). |

**Controllo**

| Inglese | Italiano | Dati | Effetto |
|---------|----------|------|---------|
| `REPEAT` | `RIPETI` | `n [istruzioni]` | Esegue n volte le istruzioni fra parentesi quadre. |
| `IF` | `SE` | `condizione [istruzioni]` | Esegue le istruzioni solo se la condizione è vera. |
| `IFELSE` | `SESENNO` | `condizione [se vera] [se falsa]` | Esegue il primo gruppo se la condizione è vera, altrimenti il secondo. |
| `WHILE` | `MENTRE` | `[condizione] [istruzioni]` | Ripete le istruzioni finché la condizione (scritta fra parentesi quadre) è vera. |
| `FOR` | `PEROGNI` | `[variabile inizio fine passo] [istruzioni]` | Ripete le istruzioni facendo variare la variabile da inizio a fine; il passo è facoltativo. |
| `STOP` | `FERMA` |  | Termina la procedura in corso. |
| `OUTPUT`, `OP` | `RESTITUISCI` | `valore` | Termina la procedura e ne restituisce il valore, così si possono scrivere procedure che calcolano. |
| `RUN` | `ESEGUI` | `[istruzioni]` | Esegue una lista come se fosse un programma. |
| `WAIT` | `ATTENDI` | `n` | Pausa di n sessantesimi di secondo. |

**Variabili**

| Inglese | Italiano | Dati | Effetto |
|---------|----------|------|---------|
| `MAKE` | `ASSEGNA` | `"nome valore` | Crea (o cambia) una variabile. Il nome va preceduto da virgolette; per leggerne il valore si usano i due punti: :nome. |
| `LOCAL` | `LOCALE` | `"nome` | Crea una variabile valida solo dentro la procedura in corso. |
| `THING` | `COSA` | `"nome` | Valore della variabile con quel nome (come :nome). |

**Stampa**

| Inglese | Italiano | Dati | Effetto |
|---------|----------|------|---------|
| `PRINT`, `PR` | `SCRIVI` | `valore` | Scrive nella console e va a capo. Con le parentesi accetta più valori: (PRINT 1 2 3). |
| `SHOW` | `MOSTRA` | `valore` | Come PRINT, ma le liste conservano le parentesi quadre. |
| `TYPE` | `DIGITA` | `valore` | Come PRINT, ma senza andare a capo. |

**Liste**

| Inglese | Italiano | Dati | Effetto |
|---------|----------|------|---------|
| `LIST` | `LISTA` | `a b` | Crea una lista con i valori dati. |
| `SENTENCE` | `FRASE` | `a b` | Unisce valori e liste in un'unica lista. |
| `WORD` | `PAROLA` | `a b` | Unisce parole in una sola. |
| `FPUT` | `METTIPRIMO` | `elemento lista` | Inserisce un elemento all'inizio della lista. |
| `LPUT` | `METTIULTIMO` | `elemento lista` | Inserisce un elemento in fondo alla lista. |
| `FIRST` | `PRIMO` | `lista` | Primo elemento di una lista (o primo carattere di una parola). |
| `LAST` | `ULTIMO` | `lista` | Ultimo elemento. |
| `BUTFIRST`, `BF` | `SENZAPRIMO` | `lista` | Tutto tranne il primo elemento. |
| `BUTLAST`, `BL` | `SENZAULTIMO` | `lista` | Tutto tranne l'ultimo elemento. |
| `COUNT` | `CONTA` | `lista` | Numero di elementi (o di caratteri). |
| `ITEM` | `ELEMENTO` | `n lista` | Elemento numero n (il primo è 1). |
| `EMPTYP`, `EMPTY?` | `VUOTO?` | `dato` | VERO se la lista o la parola è vuota. |
| `LISTP`, `LIST?` | `LISTA?` | `dato` | VERO se il dato è una lista. |
| `WORDP`, `WORD?` | `PAROLA?` | `dato` | VERO se il dato è una parola o un numero. |
| `NUMBERP`, `NUMBER?` | `NUMERO?` | `dato` | VERO se il dato è un numero. |
| `EQUALP`, `EQUAL?` | `UGUALE?` | `a b` | VERO se i due dati sono uguali (come l'operatore =). |

**Numeri**

| Inglese | Italiano | Dati | Effetto |
|---------|----------|------|---------|
| `SUM` | `SOMMA` | `a b` | Somma (come +). |
| `DIFFERENCE` | `DIFFERENZA` | `a b` | Sottrazione (come -). |
| `PRODUCT` | `PRODOTTO` | `a b` | Moltiplicazione (come *). |
| `QUOTIENT` | `QUOZIENTE` | `a b` | Divisione (come /). |
| `REMAINDER` | `RESTO` | `a b` | Resto della divisione. |
| `INT` | `INTERO` | `n` | Parte intera (toglie i decimali). |
| `ROUND` | `ARROTONDA` | `n` | Arrotonda all'intero più vicino. |
| `SQRT` | `RADICE` | `n` | Radice quadrata. |
| `ABS` | `ASSOLUTO` | `n` | Valore assoluto (toglie il segno). |
| `SIN` | `SENO` | `gradi` | Seno di un angolo in gradi. |
| `COS` | `COSENO` | `gradi` | Coseno di un angolo in gradi. |
| `ARCTAN` | `ARCOTANGENTE` | `n` | Arcotangente, risultato in gradi. |
| `POWER` | `POTENZA` | `base esponente` | Elevamento a potenza. |
| `EXP` | `ESPONENZIALE` | `n` | e elevato a n. |
| `LN` | `LOGARITMO` | `n` | Logaritmo naturale. |
| `RANDOM` | `CASUALE` | `n` | Numero intero a caso da 0 a n-1. |
| `PI` | `PIGRECO` |  | Il numero pi greco (3,14159...). |

**Logica**

| Inglese | Italiano | Dati | Effetto |
|---------|----------|------|---------|
| `AND` | `E` | `a b` | VERO se tutte le condizioni sono vere. |
| `OR` | `O` | `a b` | VERO se almeno una condizione è vera. |
| `NOT` | `NON` | `a` | Inverte VERO e FALSO. |
| `TRUE` | `VERO` |  | Il valore vero. |
| `FALSE` | `FALSO` |  | Il valore falso. |

**Definizioni e operatori**

| Forma | Effetto |
|-------|---------|
| `TO nome :a :b ... END` / `PER nome :a :b ... FINE` | Definisce una procedura con parametri. Può richiamare sé stessa (ricorsione) e restituire un valore con `OUTPUT`. |
| `+ - * /` | Aritmetica; `*` e `/` precedono `+` e `-`; le parentesi tonde cambiano l'ordine. |
| `= <> < > <= >=` | Confronti, che danno `TRUE` o `FALSE`. |
| `:nome` | Valore di una variabile. Le variabili si creano con `MAKE "nome valore`. |
| `;` | Il resto della riga è un commento. |

Con le parentesi tonde `PRINT`, `SHOW`, `TYPE`, `LIST`, `SENTENCE`, `WORD`, `SUM`, `PRODUCT`, `AND` e `OR` (e i loro nomi italiani) accettano un numero qualsiasi di dati, per esempio `(PRINT 1 2 3)` e `(SUM 1 2 3)`. Senza parentesi prendono i due dati (o uno, per `PRINT`, `SHOW` e `TYPE`) indicati dal loro uso normale.

Un segno meno con uno spazio prima e nessuno dopo è letto come segno di un numero negativo (`SETXY 0 -250`); in tutti gli altri casi è una sottrazione (`:a - 3`, `:a-3`).

## Esempi

Nel menu **ESEMPI** sono presenti nove programmi, scritti in italiano o in inglese: un quadrato, poligoni con una procedura, una stella, un fiore di quadrati, una spirale ricorsiva, un albero ricorsivo, il fiocco di Koch, una ruota dentata e un ciclo con variabili. Caricando un esempio, un file o un programma salvato sopra un testo non salvato, il testo precedente viene conservato fra i salvati con il nome "(precedente)".

## Salvataggio e file

- **SALVA**, **CARICA** ed **ELIMINA** gestiscono i programmi nel browser (`localStorage`). `ELIMINA` richiede una seconda pressione per confermare.
- **ESPORTA (.logo)** scarica il programma dell'editor come file di testo; **IMPORTA FILE** carica un file `.logo` o `.txt` (massimo 500 kB) nell'editor.
- Il testo dell'editor è salvato automaticamente come bozza e ricompare alla riapertura della pagina.
- Chiavi usate: `co_progs`, `co_draft`, `co_speed`, `co_lex`, `co_snd`, `co_vol`. L'accesso è protetto da `try/catch`: senza storage il gioco funziona, ma non salva.

## Suoni

- Mentre l'automa avanza si sente un "ciuf-ciuf" di motore a vapore (ronzio basso e soffio), il cui ritmo segue la velocità scelta. Mentre gira si sentono scatti di cricchetto, uno ogni 14 gradi circa, con un leggero ronzio. Un colpo sordo segnala la penna che si abbassa o si solleva, un ronzio grave segnala un errore.
- Quando l'automa è fermo, il motore resta acceso a livello molto basso, con un ciuf lento.
- A velocità istantanea non ci sono suoni di movimento.
- Pulsante **SUONO: ON/OFF** e cursore del volume logaritmico (da −50 dB a 0 dB). Volume e stato sono salvati nel browser.

## Limiti

- Un programma si ferma con un messaggio d'errore se esegue più di 3.000.000 di passi di interpretazione, se produce più di 250.000 operazioni di disegno o se la ricorsione supera 450 livelli: sono protezioni contro i cicli infiniti.
- Non sono previsti: `FILL`, più tartarughe, suoni e musica programmabili, accesso ai file dal linguaggio, `WRAP`, `FENCE`, `WINDOW`, `CATCH`/`THROW`, template con `?` e le altre primitive di FMSLogo non elencate nella tabella.
- I messaggi d'errore sono in italiano e non riproducono il testo di FMSLogo.

## Dettagli tecnici

- Un unico file HTML con CSS e JavaScript inline. Il disegno è su `<canvas>`, con scala per densità di pixel e un livello separato per il tracciato.
- L'interprete è separato dall'interfaccia e non usa il DOM: tokenizzazione (le liste sono token unici), analisi per priorità degli operatori, variabili con visibilità dinamica come in Logo. Esegue l'intero programma in modo sincrono producendo un elenco di operazioni di disegno, che l'interfaccia poi riproduce con animazione e suono. Per questo un errore compare dopo il disegno eseguito fino a quel punto.
- I suoni sono generati con Web Audio: oscillatori e rumore filtrato, modulati dal ritmo del movimento.

## Verifiche

- Prove automatiche dell'interprete (aritmetica e precedenze, segno meno, variabili, liste, procedure e ricorsione, `OUTPUT`, `FOR`, `WHILE`, `REPCOUNT`, errori, limiti anti-ciclo, alias italiani, geometria della tartaruga) e dei nove esempi, che vengono eseguiti senza errori e restano dentro il foglio.
- In Chromium: esecuzione di tutti gli esempi dall'interfaccia, riga di comando, salvataggio, caricamento e persistenza dopo il ricaricamento, pulsanti di scorciatoia, avvio dell'audio e livelli del motore a riposo, in movimento e a suono spento. Nessun errore di script.

Non verificati: il confronto dei risultati con FMSLogo (non è stato possibile eseguirlo); i nomi italiani oltre `AVANTI`, `INDIETRO`, `A` e `I`; l'ascolto dei suoni (timbro, volume, ritmo); esportazione e importazione di file; tastiera e tocco su dispositivi reali; Safari.

## Licenza

Distribuito con licenza GNU Affero General Public License, versione 3 (AGPL-3.0). Il testo completo è nel file `LICENSE`, da scaricare da <https://www.gnu.org/licenses/agpl-3.0.txt>. Chi ospita una versione modificata come servizio di rete deve offrire agli utenti il codice sorgente corrispondente.

## Serie

OFFICINA DEGLI ENIGMI · Machina N° 009 · BREVETTO MECCANICO 1.2 – 1894
