# Relazione: quanto ci mette l'ordinamento a bolle

Indice:

- [Obiettivo](#obiettivo)
- [Materiale](#materiale)
- [Procedimento](#procedimento)
- [Risultati](#risultati)
- [Conclusioni](#conclusioni)

## Obiettivo

Ho misurato quanto tempo impiega l'ordinamento a bolle su array di numeri sempre più grandi. Volevo vedere se il tempo cresce come dice la teoria.

## Materiale

Ho usato Linux con OpenJDK 21. Il programma è un solo file Java, `OrdinamentoTempi.java`.

## Procedimento

Il programma crea un array di numeri casuali, lo ordina e misura il tempo con `System.nanoTime()`.[^1] Lo fa con 100, 1000, 10000 e 100000 numeri. Questo è il codice:

```java
import java.util.Random;

public class OrdinamentoTempi {

    static void ordinaABolle(int[] v) {
        for (int i = 0; i < v.length - 1; i++) {
            for (int j = 0; j < v.length - 1 - i; j++) {
                if (v[j] > v[j + 1]) {
                    int t = v[j];
                    v[j] = v[j + 1];
                    v[j + 1] = t;
                }
            }
        }
    }

    public static void main(String[] args) {
        int[] dimensioni = {100, 1000, 10000, 100000};
        Random casuale = new Random(42);
        for (int n : dimensioni) {
            int[] v = new int[n];
            for (int i = 0; i < n; i++) {
                v[i] = casuale.nextInt(1_000_000);
            }
            long inizio = System.nanoTime();
            ordinaABolle(v);
            long fine = System.nanoTime();
            System.out.println(n + " " + (fine - inizio) / 1_000_000.0);
        }
    }
}
```

Per provarlo basta salvare il file e lanciare questo comando. Io l'ho lanciato tre volte.

```bash
java OrdinamentoTempi.java
```

## Risultati

La tabella ha il tempo in millisecondi (la mediana delle tre prove).[^2]

| Numeri nell'array | Tempo (ms) |
|------------------:|-----------:|
| 100 | 0,21 |
| 1000 | 9,35 |
| 10000 | 74,86 |
| 100000 | 19144,10 |

## Conclusioni

Con 100000 numeri il programma ci mette circa 19 secondi, quindi l'ordinamento a bolle va bene solo per array piccoli. Se i numeri diventano dieci volte di più, la teoria dice che il tempo diventa cento volte più grande. Nelle mie prove il tempo è cresciuto di circa 44, 8 e 256 volte. Non so bene perché i numeri non siano uguali a cento e non l'ho verificato.

[^1]: `System.nanoTime()` dà il tempo in nanosecondi. Nel programma divido per un milione per avere i millisecondi.
[^2]: Per 10000 numeri una prova è durata 370,24 ms e le altre due circa 74 ms. Ho tenuto la mediana perché un valore così diverso falsa la media.
