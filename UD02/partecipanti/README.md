# UD02 — Cloud, architettura Azure e gestione iniziale delle risorse

In questa unità collegheremo i modelli cloud alla struttura reale di Microsoft Azure. Useremo prima Azure Portal e Cloud Shell per osservare il contesto, poi Azure CLI per creare e interrogare un piccolo ambiente. Tutte le risorse verranno infine eliminate e il cleanup sarà verificato.

## Percorso dell'unità

| Fascia | Attività |
|---|---|
| 09:00–11:00 | Modelli cloud, responsabilità condivisa, architettura Azure, regioni, zone e principali famiglie di servizi |
| 11:15–12:05 | Approfondimento guidato dei concetti: Azure Portal, Cloud Shell, sottoscrizione, località, naming, tag e sequenza operativa |
| 12:05–13:00 | Laboratorio guidato, sezioni 1–4: repository, CLI, account, provider, nomi e variabili |
| 14:00–16:00 | Laboratorio guidato, sezioni 5–12: resource group, VNet, storage, Cloud Shell, Azure PowerShell, evidenze e cleanup guidato |
| 16:15–17:10 | Laboratorio autonomo basato su requisiti operativi |
| 17:10–17:35 | Verifica individuale |
| 17:35–18:00 | Correzione motivata, conferma dei due cleanup e pubblicazione finale |

La pianificazione copre **450 minuti effettivi**. La sezione 11 del laboratorio guidato viene consultata quando si presenta un errore e rimane comunque materiale di studio autonomo. Il guidato termina con cleanup entro le 16:00; l’autonomo comprende il proprio cleanup nei 55 minuti. La chiusura non richiede di tornare al guidato.

## Ordine dei materiali

1. Prima di iniziare, nel repository personale crea `consegne/UD02` e copia i quattro file presenti in `partecipanti/modelli`:

   ```bash
   cd ~/workspace/azure-devops-lab
   mkdir -p consegne/UD02
   cp -i ~/workspace/corso-azure-devops/UD02/partecipanti/modelli/*.md consegne/UD02/
   ```

2. Studia `00_CONCETTI.md` e inserisci le risposte richieste in `consegne/UD02/00_DOMANDE_CONCETTI.md`.
3. Esegui `02_LAB_GUIDATO.md` e documenta i checkpoint in `consegne/UD02/01_LAB_GUIDATO.md`; lo script di variabili creato durante la procedura va salvato come `consegne/UD02/01_VARIABILI_LAB.sh`.
4. Svolgi `03_LAB_AUTONOMO.md` e compila `consegne/UD02/02_LAB_AUTONOMO.md`.
5. Completa `04_VERIFICA.md` in `consegne/UD02/03_VERIFICA.md`.

I file dentro `partecipanti/modelli` sono sorgenti non compilati: le risposte e gli output devono essere inseriti soltanto nelle copie del repository personale.

## Richiamo a UD01

Si presume già noto come:

- distinguere PowerShell dal terminale Ubuntu;
- aprire il repository con `code .` nel contesto WSL;
- usare `git status`, `git diff`, `git add`, `git commit` e `git push`;
- controllare la versione di Azure CLI;
- evitare la pubblicazione di tenant ID, subscription ID, token e codici temporanei.

Quando uno di questi passaggi ricorre, il materiale richiama `UD01` invece di ripeterne integralmente la spiegazione.

## Criterio di completamento

Il repository personale deve contenere:

```text
azure-devops-lab/
└── consegne/
    └── UD02/
        ├── 00_DOMANDE_CONCETTI.md
        ├── 01_LAB_GUIDATO.md
        ├── 01_VARIABILI_LAB.sh
        ├── 02_LAB_AUTONOMO.md
        └── 03_VERIFICA.md
```

Il completamento richiede anche che:

- le risorse create non siano più presenti;
- il resource group del laboratorio risulti eliminato;
- i file pubblicati non contengano identificativi o credenziali non necessari;
- il commit finale sia visibile su GitHub.

## Pubblicazione e stato da conservare per UD03

Prima di copiare i modelli verifica che la cartella sorgente esista. `cp -i` chiede conferma sui file esistenti: rispondi no quando contengono lavoro già compilato. Non cancellare né ricopiare le risposte. Le consegne devono contenere prove reali e date; in assenza di un controllo scrivi Non eseguito con motivo.

Dopo la verifica, da Bash nel repository personale controlla i file modificati e tutti quelli nuovi. `git diff` non mostra i file non tracciati: aprili in VS Code prima di aggiungerli. La staging area è l'insieme preparato per il prossimo commit; se contiene lavoro estraneo, fermati e concorda come conservarlo senza reset o cancellazioni. Poi pubblica i soli cinque file UD02:

```bash
git status --short
git diff -- consegne/UD02/
git diff --cached --name-only
git add consegne/UD02/00_DOMANDE_CONCETTI.md consegne/UD02/01_LAB_GUIDATO.md consegne/UD02/01_VARIABILI_LAB.sh consegne/UD02/02_LAB_AUTONOMO.md consegne/UD02/03_VERIFICA.md
git diff --cached --name-only
git commit -m "Consolida consegne UD02 e cleanup"
git push
git log -1 --oneline
```

La lista staged deve contenere solo i file voluti; un commit vuoto non è richiesto. Il push deve riuscire e gli stessi contenuti devono essere visibili su GitHub. Registra nella conferma di consegna l'hash del commit già pubblicato: non promettere che un documento possa contenere il proprio hash futuro. L'eventuale conferma successiva ha un nuovo commit.

Per UD03 conserva repository, cinque consegne, località verificata e conoscenza di Portal/CLI/Cloud Shell. Non conservare RG, VNet o storage dei due laboratori; verifica separatamente entrambi i nomi con `az group exists`. Nessuna risorsa della UD02 è prerequisito della UD03. Riporta eventuali cleanup incompleti al docente prima di proseguire: non attribuire un `false` di un altro gruppo al tuo ambiente.
