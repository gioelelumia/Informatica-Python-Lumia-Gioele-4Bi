# Come compilare ed eseguire un programma Java

Queste istruzioni partono da un repository già clonato, nella cartella `mediavoti`. I sorgenti sono in `src/`, il codice compilato va in `bin/` e la classe con il `main` si chiama `MediaVoti`. Scrivi i comandi in un terminale `bash`, per esempio quello di Visual Studio Code.

## Passi

1. Entra nella cartella del progetto. Tutti i percorsi dopo sono relativi a `mediavoti`:

   ```bash
   cd mediavoti
   ```

2. Controlla che il JDK sia installato. Servono due programmi:
   - `javac`, il compilatore, che trasforma i file `.java` in file `.class`;
   - `java`, che esegue le classi compilate.

   Controllali con `javac --version` e `java --version`. Se `javac` non risponde, guarda l'errore in fondo alla pagina.

3. Crea la cartella `bin/` se non c'è. L'opzione `-p` di `mkdir` evita l'errore quando la cartella esiste già:

   ```bash
   mkdir -p bin
   ```

4. Compila il sorgente. L'opzione `-d bin` dice a `javac` di mettere i file `.class` dentro `bin/`:

   ```bash
   javac -d bin src/MediaVoti.java
   ```

5. Esegui il programma. L'opzione `-cp bin` dice a Java dove trovare le classi, e `MediaVoti` è la classe con il `main`:

   ```bash
   java -cp bin MediaVoti
   ```

6. Controlla che in `bin/` ci sia il file `MediaVoti.class` e che nel terminale compaia l'output del programma.

## Errore più comune: JDK non installato

Se il JDK manca, al passo 4 il terminale scrive questo:

> bash: javac: command not found

Per sistemare, installa un JDK (per esempio il 17), riapri il terminale e riprova `javac --version` finché mostra la versione.
