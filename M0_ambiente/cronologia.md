# comando usato
git log --oneline --graph --decorate
git log -5 --pretty=format:"%h %ad %an %s" --date=short

# output ottenuto
* 2653e87 (HEAD -> main, origin/main, origin/HEAD) FEAT: Aggiunta del file gitignore_verifica.md per riportare il controllo dei file ignorati
* a80943b FEAT: Aggiunta del file .gitignore per escludere file temporanei e cache
* 98ef208 FEAT: Aggiunta di file README e .gitkeep per le directory di progetto
* 6ed5054 FEAT: Aggiunta di file di configurazione e script di esempio per l'ambiente di sviluppo
* 5e108dd Initial commit
2653e87 2026-09-18 gioelelumia FEAT: Aggiunta del file gitignore_verifica.md per riportare il controllo dei file ignorati
a80943b 2026-09-18 gioelelumia FEAT: Aggiunta del file .gitignore per escludere file temporanei e cache
98ef208 2026-09-18 gioelelumia FEAT: Aggiunta di file README e .gitkeep per le directory di progetto
6ed5054 2026-09-14 gioelelumia FEAT: Aggiunta di file di configurazione e script di esempio per l'ambiente di sviluppo
5e108dd 2026-09-14 gioelelumia Initial commit

# commento
Il primo commit del 14 settembre, sono stati inseriti i file di configurazione iniziali e gli script di esempio per l'ambiente di sviluppo. Nei tre commit successivi del 18 settembre, il lavoro è proseguito con l'aggiunta di file di base come il README e .gitkeep, la creazione del file .gitignore per escludere file temporanei e cache, e infine l'inserimento del file gitignore_verifica.md per documentare il controllo dei file ignorati.
Sulla riga dell'ultimo commit compaiono le etichette HEAD, main e origin/main: HEAD indica il punto esatto del ramo in cui ci si trova attualmente a lavorare; main rappresenta il nome del ramo locale principale; origin/main indica invece l'ultimo stato noto del ramo remoto salvato sul server. Poiché tutte queste etichette si trovano esattamente sullo stesso commit, al momento dell'estrazione il repository locale era perfettamente allineato con quello remoto, senza alcuna modifica arretrata o in sospeso.