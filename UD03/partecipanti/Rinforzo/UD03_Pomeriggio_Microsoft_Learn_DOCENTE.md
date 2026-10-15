# UD03 – Consolidamento Microsoft Learn
## Percorso AZ-104: Manage identities and governance in Azure
### Versione DOCENTE

Percorso ufficiale:

https://learn.microsoft.com/en-us/training/paths/az-104-manage-identities-governance/

Study guide AZ-104:

https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-104

---

# 1. Obiettivo didattico

Il pomeriggio non deve trasformarsi in una lettura lineare del learning path Microsoft Learn.

Obiettivo:

```text
UD03
  +
selezione Microsoft Learn
  +
laboratorio reale
  +
domande in stile AZ-104
```

La parte di esame **Manage Azure identities and governance** comprende attualmente:

- utenti e gruppi Microsoft Entra;
- licenze;
- external users;
- SSPR;
- built-in Azure roles;
- assegnazioni RBAC a scope differenti;
- interpretazione degli accessi;
- Azure Policy;
- Resource Locks;
- tags;
- Resource Groups;
- subscriptions;
- costi, alert e budget;
- Azure Advisor;
- Management Groups.

Il learning path ufficiale non copre necessariamente con la stessa profondità tutti questi punti; la UD03 deve quindi integrarlo.

---

# 2. Selezione concordata dei 6 moduli Microsoft Learn

| # | Modulo | Decisione | Motivazione |
|---|---|---|---|
| 1 | Understand Microsoft Entra ID | **FARE quasi completo** | Fondamentale per identità e distinzione Entra ID / AD DS |
| 2 | Create, configure, and manage identities | **FARE selettivamente** | Utenti, gruppi e licenze sono core AZ-104; alcune unità possono essere rimandate |
| 3 | Describe the core architectural components of Azure | **SKIP come modulo** | Già affrontato; recuperare solo la gerarchia MG → Subscription → RG → Resource |
| 4 | Azure Policy initiatives | **FARE selettivamente + LAB** | Policy è core AZ-104; la parte Sovereignty/CAF non è prioritaria |
| 5 | Secure your Azure resources with Azure RBAC | **FARE completo** | Priorità massima e perfetta coerenza con UD03 |
| 6 | Allow users to reset their password with SSPR | **FARE concetti; LAB opzionale** | SSPR è esplicitamente nell'esame, ma il lab può dipendere da tenant/licenze/ruoli |

---

# 3. Modulo 1 – Understand Microsoft Entra ID

Durata Microsoft indicativa: 31 minuti.

## Fare

- Introduction
- Examine Microsoft Entra ID
- Compare Microsoft Entra ID and Active Directory Domain Services
- Examine Microsoft Entra ID as a directory service for cloud apps
- Compare Microsoft Entra ID P1 and P2 plans
- Examine Microsoft Entra Domain Services
- Module assessment
- Summary

## Obiettivi docente

I partecipanti devono distinguere:

```text
Microsoft Entra ID
= directory/identity service cloud
```

da:

```text
Active Directory Domain Services
= directory service tradizionale/domain-oriented
```

e inoltre:

```text
Tenant ≠ Subscription
```

### Checkpoint orale

1. Che cosa rappresenta un tenant?
2. Una subscription appartiene a un tenant o viceversa?
3. Entra ID sostituisce in ogni scenario AD DS? → No.
4. A cosa servono in generale P1/P2?
5. Che cosa offre Entra Domain Services?

---

# 4. Modulo 2 – Create, configure, and manage identities

Durata completa Microsoft: 1 h 4 min.

## Fare

- Introduction
- Create, configure, and manage users
- Exercise – Restore or remove deleted users
- Create, configure, and manage groups
- Exercise – Add groups in Microsoft Entra ID
- Manage licenses
- Module assessment
- Summary and resources

## Facoltativo / lettura veloce

- Exercise – Assign licenses to users
- Exercise – Modify group license assignments
- Exercise – Modify user license assignments

## Rimandare

- Configure and manage device registration
- Create custom security attributes
- Explore automatic user provisioning

## Nota didattica

Non eliminare definitivamente dal corso gli argomenti rimandati: semplicemente non sono prioritari per il consolidamento odierno.

### Scenario orale

> Dodici sistemisti devono ricevere gli stessi permessi sul Resource Group DEV.

Risposta attesa:

```text
Creare/utilizzare un gruppo
        +
assegnare il ruolo al gruppo
```

Messaggio:

```text
preferire gestione per gruppi
+
least privilege
+
riduzione delle assegnazioni individuali
```

---

# 5. Modulo 3 – Core architectural components

Non far svolgere integralmente oggi.

Riprendere per circa 5 minuti:

```text
Management Group
        ↓
Subscription
        ↓
Resource Group
        ↓
Resource
```

Serve immediatamente per spiegare lo scope di:

- RBAC;
- Azure Policy;
- Resource Locks.

---

# 6. Modulo 5 – Azure RBAC

## PRIORITÀ MASSIMA

Durata Microsoft indicativa: 37 minuti.

Far svolgere integralmente:

- Introduction
- What is Azure RBAC?
- Knowledge check
- Get a list of access
- Grant access
- View activity logs for RBAC changes
- Module assessment
- Summary

## Concetto centrale

```text
Role Assignment
=
Security Principal
+
Role Definition
+
Scope
```

## Ruoli

```text
Reader
= legge
```

```text
Contributor
= gestisce risorse
  ma non concede automaticamente accessi RBAC
```

```text
Owner
= gestisce risorse
  + gestisce gli accessi
```

## Ereditarietà

Esempio:

```text
Subscription
Contributor
    |
    +-- Resource Group
        Reader
```

Il ruolo Reader assegnato sul RG non sottrae automaticamente i permessi Contributor ereditati dalla subscription.

Accesso effettivo:

```text
Contributor
```

### Punto d'esame

Le autorizzazioni RBAC sono normalmente additive/cumulative, salvo meccanismi specifici non rappresentati da una semplice assegnazione di ruolo meno permissiva.

---

# 7. Modulo 4 – Azure Policy initiatives

Durata completa Microsoft: 1 h 13 min.

Il modulo è utilizzato sia nel learning path AZ-104 sia in Microsoft Cloud for Sovereignty. Non va quindi seguito integralmente con lo stesso peso.

## Fare

- Introduction
- Azure Policy design principles
- Azure Policy resources
- Azure Policy definitions
- Evaluation of resources through Azure Policy
- Check your knowledge
- Summary

## Solo lettura rapida / spiegazione docente

- Cloud Adoption Framework for Azure

## Non approfondire oggi

- aspetti specialistici Cloud for Sovereignty;
- framework normativi verticali;
- uso avanzato di iniziative per compliance settoriale.

## Concetti da fissare

```text
Policy Definition
= singola regola
```

```text
Initiative
= insieme coordinato di Policy Definition
```

```text
Assignment
= applicazione della Policy/Initiative a uno scope
```

```text
Compliance
= valutazione dello stato delle risorse rispetto alle regole
```

---

# 8. Laboratorio – Training Governance Baseline

## Obiettivo

Mostrare che:

```text
RBAC ≠ Policy
```

e costruire una baseline di governance con due requisiti:

1. regioni autorizzate;
2. tag obbligatorio:

```text
Environment = Training
```

## Preparazione docente

Verificare prima del laboratorio:

- accesso al portale;
- subscription attiva;
- permessi sufficienti per assegnare Policy;
- disponibilità di almeno una regione autorizzata;
- eventuali policy già presenti sulla subscription;
- eventuali limiti della subscription trial.

Non usare necessariamente gli stessi nomi di regione per tutti se le subscription presentano restrizioni differenti.

## Fase 1 – Resource Group

Nome suggerito:

```text
rg-ud03-policy
```

Regione consigliata, se disponibile:

```text
West Europe
```

## Fase 2 – Policy built-in

Portale:

```text
Policy
  → Definitions
```

Far cercare:

```text
Allowed locations
```

e una built-in equivalente a:

```text
Require a tag and its value on resources
```

Non fare affidamento sul nome visualizzato identico in tutte le localizzazioni dell'interfaccia.

Far individuare:

- Definition;
- Effect;
- Parameters;
- Scope/assignment.

---

# 9. Initiative – modalità preferita e fallback

## Modalità preferita

Creare una custom Initiative:

```text
UD03 - Training Governance Baseline
```

contenente:

```text
Allowed locations
+
Require Environment=Training
```

## Fallback didattico

Se:

- la UI è cambiata;
- i permessi non consentono la custom Initiative;
- la creazione richiede troppo tempo;
- la subscription trial presenta limitazioni;

assegnare **le due Policy separatamente allo stesso Resource Group**.

Il concetto rimane:

```text
più Policy
→ stesso obiettivo di governance
```

e il docente può mostrare l'Initiative dalla UI senza obbligare tutti a crearla.

---

# 10. Assignment

Scope:

```text
rg-ud03-policy
```

Parametri:

```text
Allowed locations:
selezionare 1-2 regioni realmente disponibili
```

```text
Tag name:
Environment

Tag value:
Training
```

## Nota temporale

L'applicazione/evaluation delle Azure Policy non è necessariamente istantanea.

Se subito dopo l'assegnazione un test non produce il risultato atteso:

1. controllare che l'assignment sia realmente creato;
2. verificare lo scope;
3. verificare i parametri;
4. attendere alcuni minuti;
5. ripetere il deployment;
6. controllare il messaggio di errore e la sezione Compliance.

Non far interpretare un primo risultato inatteso come prova che la Policy non funzioni.

---

# 11. Test di conformità – risultati attesi

## Test A

```text
Region: consentita
Environment tag: assente
```

Risultato atteso, con policy di tipo Require/Deny:

```text
DENY
```

Motivo:

```text
location → conforme
tag      → non conforme
```

## Test B

```text
Region: NON consentita
Environment=Training
```

Risultato atteso:

```text
DENY
```

Motivo:

```text
location → non conforme
tag      → conforme
```

## Test C

```text
Region: consentita
Environment=Training
```

Risultato atteso:

```text
DEPLOYMENT CONSENTITO
```

a condizione che non intervengano altre policy o limitazioni della subscription.

---

# 12. Troubleshooting laboratorio Policy

Se un deployment viene negato quando dovrebbe essere consentito:

- leggere il dettaglio dell'errore;
- verificare eventuali Policy Assignment ereditati dalla subscription;
- controllare policy organizzative/preesistenti;
- controllare la regione;
- controllare esattamente nome e valore del tag;
- controllare eventuali restrizioni della trial;
- verificare che la Policy scelta si applichi al tipo di risorsa usato.

Se un deployment viene consentito quando dovrebbe essere negato:

- verificare lo scope dell'Assignment;
- controllare che l'Assignment sia abilitato;
- controllare i parametri;
- attendere propagazione/evaluation;
- verificare di non aver scelto una variante Audit al posto di Deny.

---

# 13. Scenario RBAC vs Policy

Domanda:

> Un utente è Owner del Resource Group. Azure Policy consente solo alcune regioni. L'utente tenta un deployment in una regione vietata. Può farlo perché è Owner?

Risposta:

**No, non automaticamente.**

Schema:

```text
RBAC
"Sei autorizzato a creare la risorsa?"
            ↓
           SÌ
```

```text
Policy
"La configurazione richiesta è consentita?"
            ↓
           NO
```

```text
Deployment
            ↓
          NEGATO
```

---

# 14. Modulo 6 – SSPR

Durata completa Microsoft: 31 minuti.

## Fare oggi

- Introduction
- What is Microsoft Entra self-service password reset?
- Implement Microsoft Entra self-service password reset
- Summary

## Lab opzionale

- Exercise – Configure self-service password reset

Eseguire solo se il tenant e le autorizzazioni disponibili lo consentono.

## Rimandare

- tutorial sul branding.

## Concetti da fissare

- funzione SSPR;
- prerequisiti;
- metodi di autenticazione;
- riduzione del carico help desk;
- relazione con identità;
- SSPR non è RBAC.

---

# 15. Scansione pomeridiana consigliata

Se la UD03 termina entro pranzo:

| Orario | Attività |
|---|---|
| 14:00–14:30 | Modulo 1 – Entra ID |
| 14:30–15:00 | Modulo 2 – utenti, gruppi, licenze selezionate |
| 15:00–15:40 | Modulo 5 – RBAC completo |
| 15:40–16:00 | Checkpoint docente + domande |
| 16:00–16:15 | Pausa |
| 16:15–16:45 | Modulo 4 – Policy, parti selezionate |
| 16:45–17:30 | Laboratorio Policy/Initiative |
| 17:30–17:40 | SSPR – concetti essenziali |
| 17:40–18:00 | Quiz e debrief |

Se il laboratorio richiede più tempo:

- SSPR può essere assegnato come lettura autonoma conclusiva;
- **non sacrificare il debrief RBAC/Policy**.

---

# 16. Quiz finale – soluzioni

## Domanda 1

**B – Contributor**

Contributor assegnato alla subscription viene ereditato dal Resource Group. Reader sul Resource Group non revoca Contributor.

## Domanda 2

**B – Contributor**

Può gestire le risorse senza avere automaticamente la possibilità di assegnare ruoli come Owner.

## Domanda 3

**C – Security principal**

Identifica chi riceve l'assegnazione.

## Domanda 4

**A – Role definition**

Definisce le operazioni consentite.

## Domanda 5

**B – Azure Policy**

Policy governa le configurazioni ammesse.

## Domanda 6

**C – Resource Lock CanNotDelete**

Protegge dalla cancellazione accidentale.

## Domanda 7

**B – Può essere modificato ma non eliminato**

```text
CanNotDelete → no delete
ReadOnly     → no update/delete
```

## Domanda 8

**C – Avviso, non blocco automatico della spesa**

Un Budget è principalmente uno strumento di controllo/alerting.

## Domanda 9

**A – Reader**

È il ruolo coerente con il minimo privilegio per sola consultazione.

## Domanda 10

**B**

```text
RBAC   → chi può fare cosa
Policy → quali configurazioni sono ammesse
```

---

# 17. Domande orali aggiuntive

## Scenario 1

> Tutti gli sviluppatori devono leggere le risorse del Resource Group DEV.

Risposta:

```text
Entra Group
+
Reader
+
scope Resource Group DEV
```

## Scenario 2

> È vietato distribuire risorse fuori dalle regioni autorizzate.

Risposta:

```text
Azure Policy
```

## Scenario 3

> Una VM critica non deve essere eliminata accidentalmente.

Risposta:

```text
CanNotDelete Resource Lock
```

## Scenario 4

> Un team può distribuire VM, ma solo in West Europe.

Risposta:

```text
RBAC
+
Azure Policy
```

Spiegazione:

```text
RBAC → autorizza il team a creare VM
Policy → limita le configurazioni/regioni consentite
```

---

# 18. Errori da intercettare

## Entra ID = RBAC

Errato.

```text
Entra ID
identità
```

```text
RBAC
autorizzazione
```

## Reader inferiore annulla Contributor superiore

Errato. Le normali assegnazioni RBAC sono additive.

## Owner può ignorare tutte le Policy

Errato. Essere autorizzati da RBAC non equivale a rendere conforme una configurazione.

## Budget = hard spending limit

Errato. Budget e alert non equivalgono automaticamente a uno shutdown delle risorse.

## Policy = firewall

Errato. Azure Policy è un motore di governance/configuration compliance, non un firewall di rete.

---

# 19. Copertura rispetto alla study guide AZ-104

## Coperto oggi

- users/groups;
- licenses: concetti e gestione;
- SSPR: concetti;
- Azure built-in roles;
- role assignments;
- scopes;
- interpretation of effective access;
- Azure Policy;
- tags;
- Resource Groups;
- Resource Locks;
- budgets: concetto;
- Management Groups: gerarchia.

## Da integrare/rafforzare nelle UD o attività successive

- external users;
- subscriptions: gestione operativa;
- cost alerts più articolati;
- Azure Advisor recommendations;
- gestione più ampia dei costi;
- eventuali approfondimenti di Management Groups;
- casi operativi ulteriori di Policy/remediation.

---

# 20. Criterio di chiusura UD03

La UD può considerarsi consolidata quando i partecipanti sanno spiegare e applicare:

```text
Identity
→ Entra ID
```

```text
Authorization
→ RBAC
```

```text
Configuration governance
→ Azure Policy
```

```text
Grouped governance controls
→ Initiative
```

```text
Protection from destructive operations
→ Resource Lock
```

```text
Cost awareness
→ Budget / alerts
```

e sanno risolvere semplici scenari senza limitarsi a ricordare definizioni.

---

# Riferimenti ufficiali

- AZ-104 – Manage identities and governance in Azure  
  https://learn.microsoft.com/en-us/training/paths/az-104-manage-identities-governance/

- AZ-104 Study Guide  
  https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-104

- Azure Policy initiatives  
  https://learn.microsoft.com/en-us/training/modules/sovereignty-policy-initiatives/

- Azure RBAC module  
  https://learn.microsoft.com/en-us/training/modules/secure-azure-resources-with-rbac/

- Microsoft Entra ID module  
  https://learn.microsoft.com/en-us/training/modules/understand-azure-active-directory/
