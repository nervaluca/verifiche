# Verifiche Impianti — Ten Solutions

PWA per la compilazione da smartphone del rapporto di verifica/collaudo impianti
elettrici (CEI 64-8, DPR 462/01), con esportazione in PDF firmato e archivio
locale delle verifiche compilate.

## Struttura

- `www/index.html` — l'intera app (HTML + CSS + JS), stesso stile del
  Rapportino giornaliero.
- `www/jspdf.umd.min.js`, `www/jspdf.autotable.min.js` — librerie vendorizzate
  per generare il PDF offline (nessuna dipendenza da CDN esterni).
- `www/manifest.webmanifest`, `www/sw.js` — PWA installabile, funziona offline.
- `capacitor.config.json`, `package.json`, `.github/workflows/` — build APK
  Android identico al flusso del Rapportino (GitHub Actions, firma con gli
  stessi secrets `KEYSTORE_BASE64` / `KEY_ALIAS` / `KEYSTORE_PASSWORD` /
  `KEY_PASSWORD` se vuoi l'APK firmato).

## Funzioni principali

1. Dati identificativi, dati generali impianto, misura di terra
2. Continuità PE/EQP, resistenza di isolamento, prove differenziali,
   illuminazione di emergenza — tutte a righe aggiungibili/eliminabili
3. Esito verifica e prescrizioni
4. Firma su schermo (tecnico e committente) con canvas touch
5. Salvataggio automatico della bozza in corso (localStorage)
6. Archivio locale delle verifiche salvate, con possibilità di riaprirle
7. Esportazione PDF (autopaginato, con intestazione, tabelle e firme) e
   condivisione nativa su Android (Capacitor Share) o download da browser

## Deploy

Stesso procedimento già usato per il Rapportino:
- **Netlify**: collega questa repo, build command vuoto, publish directory `www`.
- **GitHub Pages**: workflow Actions con source "GitHub Actions" (se preferisci
  repo pubblica).
- **APK Android**: tab Actions → workflow "Build APK" → Run workflow.

## Note

- Le icone PWA sono nella root di `www/` (non in una sottocartella): su
  Android/Chrome le icone in sottocartella a volte non venivano risolte
  correttamente, per cui qui sono già posizionate nel modo che funziona.
- Nessuna dipendenza da rete a runtime: jsPDF e ExcelJS-equivalenti sono
  vendorizzati nella cartella `www/`, quindi l'app genera i PDF anche offline
  in cantiere.
