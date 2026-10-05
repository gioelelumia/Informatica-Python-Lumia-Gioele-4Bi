# Conversione della relazione con Pandoc

Qui scrivo come ho trasformato `relazione.md` in un file HTML e in un file PDF con Pandoc 3.1.3. I comandi si lanciano dalla cartella `M1_markdown/`. I file `.html` e `.pdf` non vanno nel repository.

## Comando per l'HTML

```bash
pandoc relazione.md -o relazione.html --standalone --embed-resources --toc --toc-depth=2 --shift-heading-level-by=-1 --metadata title="Relazione: quanto ci mette l'ordinamento a bolle"
```

Opzioni usate:

- `-o relazione.html` è il file di uscita.
- `--standalone` crea una pagina HTML completa.
- `--embed-resources` mette dentro il file stili e immagini, così funziona anche su una chiavetta.
- `--toc` crea l'indice in cima alla pagina.
- `--toc-depth=2` ferma l'indice al secondo livello.
- `--shift-heading-level-by=-1` abbassa di un livello i titoli. Senza questa opzione il titolo compare due volte.
- `--metadata title="..."` imposta il titolo del documento.

## Comando per il PDF

```bash
pandoc relazione.md -o relazione.pdf --pdf-engine=xelatex -V geometry:margin=2.5cm -V fontsize=11pt -V lang=it -V papersize=a4
```

Opzioni usate:

- `-o relazione.pdf` è il file di uscita.
- `--pdf-engine=xelatex` usa `xelatex`, che rende bene le lettere accentate.
- `-V geometry:margin=2.5cm` mette i margini a 2,5 cm.
- `-V fontsize=11pt` mette il carattere a 11 punti.
- `-V lang=it` dice che il testo è in italiano.
- `-V papersize=a4` usa il formato A4. Senza, Pandoc usa il formato Letter.

## Controlli fatti

L'HTML ha l'indice con le cinque sezioni e i link funzionano. Il PDF ha due pagine A4 e le lettere accentate si leggono bene. Con `pdftotext -bbox` ho misurato i margini del testo: circa 2,5 cm a sinistra e in alto. A destra qualche riga esce un po' dal margine, fino a circa 2,1 cm, perché LaTeX non ha spezzato alcune parole lunghe.

## Messaggi ottenuti

Il comando per l'HTML non ha dato avvisi. Il comando per il PDF al primo tentativo ha dato questo errore:

```text
! LaTeX Error: File `lmodern.sty' not found.
```

Il pacchetto non era installato: `kpsewhich lmodern.sty` non trovava niente. Nel mio ambiente non avevo la rete, quindi ho creato un file `lmodern.sty` vuoto in `~/texmf/tex/latex/lmodern/` e dopo il PDF è uscito senza altri messaggi. Con la rete è meglio installare il pacchetto vero.

## Controllo del `.gitignore`

Nel `.gitignore` ci sono le righe `*.html` e `*.pdf`. Ho controllato che funzionino con questo comando, che dice quale riga ignora ogni file:

```bash
git check-ignore -v M1_markdown/relazione.html M1_markdown/relazione.pdf
```
