## **Panoramica**

Il **sistema operativo (OS)** di un computer ha il compito di memorizzare e gestire i dati in diversi punti del sistema. I dati volatili vengono costantemente spostati tra l’unità di elaborazione centrale (CPU) e la memoria di sistema. Quando non sono in uso, questi dati vengono trasferiti su dispositivi di archiviazione più lenti ma più capienti, come i dischi rigidi (HDD) o le unità a stato solido (SSD/NVMe).

L’utente interagisce con questa memoria a lungo termine tramite il **file system**, ovvero il componente del sistema operativo che organizza file, cartelle, dispositivi di archiviazione e periferiche.

---

## **Struttura del File System**

Nei sistemi Linux, il file system segue una struttura gerarchica organizzata attorno a una **directory principale**, chiamata anche **root directory**, rappresentata dal simbolo `/`. Tutti i file e le cartelle del sistema si trovano sotto questa directory. Persino **i dispositivi fisici vengono rappresentati come file all’interno della struttura del file system**.

Sebbene ci possano essere leggere differenze tra le varie distribuzioni Linux, la maggior parte segue il **Filesystem Hierarchy Standard (FHS)** definito dalla Linux Foundation.

![[Immagine 2025-04-10 122209.png]]

A titolo di confronto, il sistema operativo **Microsoft Windows** utilizza una struttura gerarchica basata su **volumi**, **cartelle** e **file**. I volumi possono essere dispositivi fisici o partizioni logiche, e Windows assegna a ciascuno di essi una lettera (es. C:, D:, ecc.). Ogni volume contiene una gerarchia di cartelle e file.

![[Pasted image 20250410121955.png]]

---

## **Tipi di File System**

Ogni file system memorizza **metadati**, ovvero informazioni come dimensione, attributi, posizione fisica, data di creazione/modifica, permessi di accesso e altro ancora.

Ecco alcuni dei file system più comuni:

- **Windows**: FAT, NTFS
    
- **macOS**: HFS, APFS
    
- **Linux**: EXT, XFS

Nel mondo Linux, il file system **EXT** (Extended File System) è il più diffuso. Introdotto nel 1992, ha subito diverse evoluzioni: EXT2, EXT3 e l’attuale versione EXT4. Questo file system utilizza strutture di dati chiamate **inodi** (**inode**), che memorizzano i **metadati** dei file e ne indicano la posizione fisica sul disco.

Sebbene per la maggior parte degli utenti questi dettagli tecnici rimangano nascosti, comprendere il funzionamento dei file system è essenziale in ambiti specialistici come la **Digital Forensics** o la **Cybersecurity**, dove l’analisi approfondita di FAT, NTFS, HFS ed EXT diventa fondamentale per investigazioni e operazioni avanzate.

---

