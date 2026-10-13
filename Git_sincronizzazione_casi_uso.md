# Git: sincronizzazione e casi d’uso

**Non è obbligatorio eseguire `fetch` prima di `pull`: `pull` include già il fetch.** Separare le operazioni permette di controllare gli aggiornamenti prima di integrarli. Il fetch non elimina i conflitti: consente di valutare la situazione in anticipo.

Gli esempi presuppongono il ramo locale `main` collegato a `origin/main`. Esegui i comandi nella cartella del repository, nell’ordine indicato; prosegui soltanto se il comando precedente riesce.

## 1. Cosa fanno i comandi

| Comando | Effetto | Ragione |
|---|---|---|
| `git status` | Mostra modifiche locali e confronto con il ramo remoto di riferimento. | Prima del fetch, il confronto può essere basato su informazioni vecchie. |
| `git fetch origin` | Scarica commit e aggiorna riferimenti come `origin/main`, senza modificare il ramo corrente o i file di lavoro. | Conoscere gli aggiornamenti senza integrarli. |
| `git pull --ff-only` | Esegue fetch e aggiorna il ramo solo se può avanzare direttamente, senza unire storie divergenti. | Aggiornarsi con un comportamento esplicito; se i rami divergono, si ferma. |
| `git push` | Pubblica i commit locali sul remoto. | Rendere disponibili agli altri le modifiche già salvate in un commit. |

`origin/main` è un riferimento locale all’ultima situazione remota recuperata: non è una lettura in tempo reale di GitHub.

## 2. Sequenza di controllo

```bash
git status
git fetch origin
git status
```

Poi scegli il caso appropriato. Le indicazioni `ahead`, `behind` e `diverged` confrontano i commit; le modifiche non ancora salvate in un commit sono un controllo separato.

## 3. Casi d’uso

| Caso concreto | Situazione dopo il fetch | Comandi successivi | Perché |
|---|---|---|---|
| Un partecipante ha aggiornato i materiali; voglio scaricarli. | `behind`, nessuna modifica locale. | `git pull --ff-only`, poi `git status`. | Integra i commit remoti nei file locali. |
| Ho creato un commit con UD02; devo pubblicarlo. | `ahead`, nessuna modifica locale. | `git push`, poi `git status`. | Il commit esiste solo in locale; non serve un pull. |
| Voglio solo sapere se ci sono novità. | Qualsiasi stato. | Nessuna integrazione; usa i comandi di ispezione sotto. | Il fetch ha già aggiornato le informazioni. |
| Ho lavoro incompleto e devo scaricare aggiornamenti. | Modifiche non committate e ramo `behind`. | `git stash push -u -m "Lavoro in corso"`, poi `git pull --ff-only`, poi `git stash pop`. | Accantona il lavoro, aggiorna, ripristina. `-u` include i nuovi file non tracciati, ma non quelli ignorati. Il ripristino può generare conflitti. |
| Io e un collega abbiamo creato commit diversi. | `diverged`, nessuna modifica locale. | `git merge origin/main`, poi `git push` dopo aver completato il merge e verificato il risultato. | Unisce le due storie conservando i commit. Se ci sono conflitti: correggi i file, esegui `git add <file>` per ciascuno e `git commit`. |
| Nessuno ha aggiunto commit. | `up to date`. | Nessun pull o push necessario. | I rami sono allineati; puoi continuare il lavoro. |

Per storie divergenti, il rebase è un’alternativa secondo il flusso del gruppo: `git rebase origin/main` riapplica i commit locali e ne cambia gli identificatori. Usalo per commit non ancora pubblicati; non eseguire merge e rebase in successione come passaggi obbligatori.

## 4. Ispezionare prima di integrare

Dopo il fetch, con il ramo corrente `main`:

| Comando | Cosa mostra |
|---|---|
| `git log --oneline main..origin/main` | Commit remoti assenti dal ramo locale. |
| `git log --oneline origin/main..main` | Commit locali assenti dal remoto. |
| `git diff main...origin/main` | Modifiche sul ramo remoto dalla base comune; non include il lavoro locale non committato. |

Dopo aver controllato, `git merge --ff-only origin/main` integra quanto già scaricato senza un secondo fetch. `git pull --ff-only` recupera invece anche eventuali novità pubblicate nel frattempo.

## Riferimenti ufficiali

- [Git fetch](https://git-scm.com/docs/git-fetch)
- [Git pull](https://git-scm.com/docs/git-pull)
- [Git stash](https://git-scm.com/docs/git-stash)

