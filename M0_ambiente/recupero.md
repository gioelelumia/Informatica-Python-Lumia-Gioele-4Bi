# Descrizione del problema 
A volte capita di aggiungere dei file o delle cartelle con i comandi `git add` e `git commit` prima di inserirli all'interno del file `.gitignore`. 

Quando si verifica questo errore, il file `.gitignore` da solo non basta a risolvere la situazione, i file continuano a essere monitorati da Git perché sono già stati inseriti nel database del progetto.

---

## Sequenza dei comandi da terminale

```
echo "M0_ambiente/temporanei/" >> .gitignore
git status
git ls-files M0_ambiente/temporanei
git check-ignore -v M0_ambiente/temporanei/nota.txt
git rm --cached -r M0_ambiente/temporanei/
```