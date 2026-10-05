# Notebook riproducibile e pulito prima del commit

Qui scrivo come ho sistemato `M1_esercizio10.ipynb` per poterlo versionare: deve arrivare in fondo da un kernel vuoto e deve entrare in Git senza output inutili. Ogni sezione è un passaggio dell'esercizio 15.

## 1. Rompere la riproducibilità

Ho aggiunto in fondo al notebook due celle di codice. La prima crea una variabile e la seconda la usa:

```python
margine_minuti = 3
```

```python
print("Margine di sicurezza (minuti):", margine_minuti)
```

Le ho eseguite tutte e due. Poi ho cancellato la cella che crea `margine_minuti` senza riavviare il kernel e ho rieseguito la cella che la usa. Il notebook funziona ancora e stampa `Margine di sicurezza (minuti): 3`.

Il motivo è che il kernel tiene in memoria le variabili finché non lo riavvio. La cella non c'è più nel file, ma il suo effetto è ancora nella memoria. A schermo sembra tutto giusto, ma il file da solo non basta più per ricreare quel valore.

## 2. Mostrare il difetto con il riavvio

Ho scelto **Kernel > Restart Kernel and Run All Cells**. L'esecuzione si è fermata sulla cella che usa la variabile, la quarta cella di codice, con il numero `[4]`. Questo è l'errore:

```text
NameError                                Traceback (most recent call last)
Cell In[4], line 1
----> 1 print("Margine di sicurezza (minuti):", margine_minuti)

NameError: name 'margine_minuti' is not defined
```

Le celle non hanno un nome. La cella che si ferma è quella con `print("Margine di sicurezza (minuti):", margine_minuti)`. Un compagno che apre il file con un kernel vuoto vede lo stesso errore.

## 3. Correzione e nuova verifica

Ho rimesso la cella che crea `margine_minuti` sopra quella che la usa. Dopo **Restart Kernel and Run All Cells** il notebook arriva in fondo senza errori, con i numeri `[1]`, `[2]`, `[3]`, `[4]`, `[5]` in ordine crescente.

Le due celle servivano solo per la prova. Le ho cancellate e ho rifatto la verifica: il notebook finale arriva in fondo senza errori con i numeri `[1]`, `[2]`, `[3]`.

## 4. Due commit a confronto

Il notebook era già nel repository con gli output, aggiunto con il commit dell'esercizio 10. Questo è il primo commit:

```bash
git add M1_jupyter/M1_esercizio10.ipynb
git commit -m "Aggiunge il notebook di consegna (M1 es. 10)"
```

Poi ho cancellato gli output e ho fatto il secondo commit:

```bash
jupyter nbconvert --clear-output --inplace M1_jupyter/M1_esercizio10.ipynb
git add M1_jupyter/M1_esercizio10.ipynb
git commit -m "Rimuove gli output dal notebook (M1 es. 15)"
```

Ho contato le righe cambiate con `git diff --shortstat`, che confronta due versioni e riassume le righe aggiunte ed eliminate. Per il secondo commit:

```bash
git diff --shortstat HEAD~1 HEAD
```

Il primo commit aggiunge un file nuovo, quindi `git diff` non ha niente da confrontare. Per quello ho guardato la cronologia del solo notebook, che mostra le statistiche di tutti e due i commit:

```bash
git log --shortstat --format="%h %s" -- M1_jupyter/M1_esercizio10.ipynb
```

Risultati:

| Commit | Righe aggiunte | Righe eliminate |
|---|---:|---:|
| Con gli output | 216 | 0 |
| Senza output | 6 | 31 |

Il primo commit aggiunge tutto il file, perché prima non esisteva: sono 216 righe, e dentro ci sono anche gli output e i numeri di esecuzione. Il secondo commit tocca solo 37 righe. Le 31 eliminate sono gli output e i numeri di esecuzione. Le 6 aggiunte sono le coppie `"execution_count": null` e `"outputs": []` delle tre celle di codice. Il testo delle celle non cambia.

Conviene versionare il notebook senza output, perché ogni esecuzione cambia i numeri e a volte il testo stampato. Con gli output salvati, `git diff` mostrerebbe righe cambiate anche se il codice è uguale, e nasconderebbe le modifiche vere.

## 5. Escludere i salvataggi automatici di Jupyter

Jupyter salva copie di sicurezza nella cartella `.ipynb_checkpoints/`, vicino ai notebook. Prima di toccare il `.gitignore`, `git status` la segnalava come non tracciata:

```text
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	M1_jupyter/.ipynb_checkpoints/
```

Ho aggiunto questa riga al `.gitignore` nella radice del repository:

```text
.ipynb_checkpoints/
```

Dopo la modifica ho rifatto `git status` e la cartella `M1_jupyter/.ipynb_checkpoints/` non compare più fra i file non tracciati. Resta solo il `.gitignore`, perché è cambiato e va versionato anche lui.
