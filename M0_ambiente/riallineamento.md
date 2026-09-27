# Descrizione del problema
Questo problema si verifica perché il computer e il sito di GitHub si sono "separati": sul sito web è stato modificato un file (il README.md), mentre sulla postazione locale il lavoro è stato svolto su un file differente (versioni.md).

## messaggio di errore ottenuto

```
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/gioelelumia/Informatica-Python-Lumia-Gioele-4Bi'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref. If you want to integrate the remote changes, use
hint: 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

## comando usato

```
git pull origin main --rebase
git push
git log --oneline --graph --decorate
```

