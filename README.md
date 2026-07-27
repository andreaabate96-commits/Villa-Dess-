# Villa Dessì — sito vetrina

Sito statico in un unico file (`index.html`). Nessun framework, nessuna build,
nessuna dipendenza da installare: si apre con doppio clic e si pubblica gratis
con GitHub Pages.

Il deploy è automatico: **ogni modifica salvata su `main` finisce online da sola**
in un paio di minuti, tramite GitHub Actions.

```
villa-dessi/
├── index.html                     ← il sito intero (testi, stile, script)
├── immagini/                      ← qui dentro vanno le foto
├── README.md                      ← questo file
├── .nojekyll                      ← dice a Pages di servire i file così come sono
├── .gitignore                     ← file da non caricare (.DS_Store, zip, RAW…)
├── .editorconfig                  ← formattazione uniforme fra editor
└── .github/
    ├── workflows/
    │   ├── deploy.yml             ← pubblica il sito a ogni push su main
    │   └── verifica.yml           ← controlla HTML e foto mancanti
    └── pull_request_template.md   ← checklist prima di pubblicare
```

I file che iniziano con un punto sono nascosti nel Finder: per vederli premi
**⌘ + Shift + .** (comando, shift, punto).

---

## 1. Metterlo online su GitHub (10 minuti, una volta sola)

1. Crea un account su [github.com](https://github.com) se non ce l'hai.
2. In alto a destra: **+ → New repository**.
   - Nome: `villa-dessi`
   - Visibilità: **Public** (necessaria per GitHub Pages gratuito)
   - Non spuntare "Add a README" (c'è già)
3. Nella pagina del repository vuoto clicca **uploading an existing file** e
   trascina dentro **tutto il contenuto di questa cartella**, compresa
   `.github` (con ⌘ + Shift + . la vedi nel Finder). Poi **Commit changes**.
4. Vai su **Settings → Pages**.
   - *Source*: **GitHub Actions** ← è questa la voce, non "Deploy from a branch"
   - Non serve scegliere branch né cartella: lo fa il workflow.
5. Vai sul tab **Actions**: vedrai girare "Deploy sito su GitHub Pages".
   Quando il pallino diventa verde il sito è online su
   `https://TUO-NOME-UTENTE.github.io/villa-dessi/`

Se preferisci la riga di comando:

```bash
cd "villa dessi"
git init -b main
git add -A
git commit -m "Primo commit: sito Villa Dessì"
git remote add origin https://github.com/TUO-NOME-UTENTE/villa-dessi.git
git push -u origin main
```

### Come funziona il deploy automatico

Da qui in avanti non devi fare più nulla di manuale: ogni volta che modifichi un
file su `main` (dal sito di GitHub o con `git push`), il workflow
`.github/workflows/deploy.yml` riprende il sito e lo ripubblica. Un secondo
workflow, `verifica.yml`, controlla che l'HTML non sia rotto e segnala le foto
citate ma non ancora caricate — senza bloccare la pubblicazione.

Se qualcosa va storto trovi il dettaglio nel tab **Actions**: clicca sul
tentativo rosso e leggi il passaggio evidenziato. Per tornare alla versione
precedente: **History → il commit buono → Revert**.

Deploy manuale senza modificare nulla: **Actions → Deploy sito su GitHub Pages
→ Run workflow**.

### Dominio personale (facoltativo)
In **Settings → Pages → Custom domain** scrivi `www.villadessi.it`, poi dal
pannello del tuo registrar aggiungi un record CNAME che punta a
`TUO-NOME-UTENTE.github.io`. Lascia attiva la spunta *Enforce HTTPS*.
GitHub crea da sé un file `CNAME` nel repository: non cancellarlo.

---

## 2. Aggiungere o cambiare le foto

Le foto stanno nella cartella `immagini/`. Il sito cerca questi file:

| File atteso | Dove compare | Formato consigliato |
|---|---|---|
| `hero-villa-mare.jpg` | schermata iniziale, a tutto schermo | orizzontale 16:9, min. 2400 px di larghezza |
| `soggiorno.jpg` | Gli spazi 01 | orizzontale 4:3, min. 1600 px |
| `camera-vista-mare.jpg` | Gli spazi 02 | orizzontale 4:3 |
| `porticato.jpg` | Gli spazi 03 | orizzontale 4:3 |
| `esterni-barbecue.jpg` | Gli spazi 04 | orizzontale 4:3 |
| `cucina.jpg` | Gli spazi 05 | orizzontale 4:3 |
| `spiaggia-accesso.jpg` | Gli spazi 06 | orizzontale 4:3 |
| `vista-orizzonte.jpg` | sezione "Dall'alba al tramonto" | orizzontale 16:9 |

**Come si fa da GitHub, senza programmi:**
apri la cartella `immagini` → **Add file → Upload files** → trascina la foto →
**Commit changes**. Se il nome del file è uguale a quello vecchio, la sostituisce.

Finché una foto manca, al suo posto il sito mostra un rettangolo a righe con
scritto quale foto va inserita: puoi pubblicare anche prima di avere tutto.

**Consigli di scatto:** luce del mattino presto o dell'ora prima del tramonto,
orizzonte dritto, casa in ordine e senza persone riconoscibili. Meglio otto foto
grandi e giuste che trenta mediocri. Comprimi i file sotto i 400 kB
(tinypng.com o squoosh.app) prima di caricarli: il sito deve aprirsi veloce anche
in spiaggia con una tacca di rete.

---

## 3. Cambiare testi, contatti, comfort, prezzi

Tutto quello che si modifica normalmente sta **nelle prime 100 righe di
`index.html`**, dentro il blocco segnalato da:

```
▼▼▼  MODIFICA SOLO QUESTO BLOCCO  ▼▼▼
```

Da GitHub: clicca su `index.html` → icona della matita (**Edit this file**) →
modifica → **Commit changes**. Il sito si aggiorna da solo in un minuto.

Cosa trovi lì dentro:

| Voce | Cosa cambia |
|---|---|
| `headline`, `sottotitolo` | il titolo grande della prima schermata |
| `contatti` | email, telefono, numero WhatsApp, Instagram, indirizzo |
| `contatti.whatsappTesto` | il messaggio già scritto che si apre in WhatsApp |
| `formEndpoint` | dove arrivano le richieste del modulo (vedi punto 4) |
| `foto` | nome file e testo alternativo di ogni immagine |
| `datiChiave` | i tre numeri sotto l'introduzione |
| `esperienze` | le card "Intorno": aggiungi o togli blocchi `{ titolo, testo }` |
| `servizi` | la lista dei comfort inclusi: aggiungi righe fra virgolette |
| `tariffe`, `tariffeNota` | la tabella stagionale |
| `testimonianze` | le citazioni degli ospiti |
| `distanze` | l'elenco delle distanze nella sezione blu |
| `mappaLink` | il link "Apri la mappa" |

Regole per non rompere niente: ogni voce va **fra virgolette**, ogni riga di una
lista finisce con la **virgola** (tranne l'ultima), e le parentesi vanno lasciate
come sono. Se qualcosa va storto, GitHub tiene la cronologia: **History → il
commit precedente → Revert**.

I testi delle sei sezioni "Gli spazi" stanno più in basso, nella costante `SPAZI`
dentro l'ultimo `<script>`: stessa logica.

---

## 4. Far arrivare le richieste del modulo

Di serie il modulo apre il programma di posta dell'ospite con la richiesta già
compilata. Funziona sempre, ma qualche richiesta si perde per strada.

Per ricevere le richieste direttamente via email:

1. Registrati su [formspree.io](https://formspree.io) (piano gratuito: 50
   richieste al mese) e crea un form con la tua email.
2. Copia l'indirizzo che ti danno, del tipo `https://formspree.io/f/abcdwxyz`.
3. In `index.html` scrivi:
   `formEndpoint: "https://formspree.io/f/abcdwxyz",`

Da quel momento le richieste arrivano nella tua casella e il visitatore resta
sulla pagina. Alternative equivalenti: Basin, Getform, Web3Forms.

---

## 5. Prima di pubblicare davvero

- [ ] Sostituire numero di telefono e WhatsApp (`+39 000 000 0000`)
- [ ] Inserire il **CIN / CIR** della locazione turistica nel footer (obbligo di legge)
- [ ] Verificare le tariffe della stagione in corso
- [ ] Controllare che le testimonianze siano reali e autorizzate dagli ospiti
- [ ] Aggiungere una pagina privacy se attivi Formspree o statistiche
- [ ] Aprire il sito da telefono e provare il modulo fino in fondo
- [ ] Controllare che in **Settings → Pages** la *Source* sia `GitHub Actions`
- [ ] Verificare che l'ultimo run in **Actions** sia verde
