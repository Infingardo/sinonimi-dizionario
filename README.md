# 📚 Dizionario dei Sinonimi - Edizione Vintage Restaurata

**Un dizionario interattivo e ricercabile dei sinonimi italiani con interface vintage moderna**

---

## 📖 Descrizione

Questo è uno **strumento web-based** per la ricerca interattiva di sinonimi e contrari in italiano. Combina i dati di un dizionario tradizionale restaurato digitalmente con un'interfaccia moderna, responsive e intuitiva.

Caratteristiche principali:
- ✅ **14.000+** lemmi italiani con sinonimi e contrari
- ✅ **Ricerca avanzata** con wildcard support
- ✅ **Caching intelligente** (localStorage con versioning)
- ✅ **PWA installabile** come app nativa
- ✅ **Zero dipendenze** - React + Tailwind inline
- ✅ **Mobile-first** design completamente responsive

---

## 🚀 Come Usare

### Accesso Online
```
https://infingardo.github.io/sinonimi-dizionario/
```

### Primo Accesso: Caricare il Dizionario

Il dizionario NON è pre-caricato. Al primo accesso, hai due opzioni:

#### Opzione A: Carica JSON da GitHub (CONSIGLIATO - Veloce)
```
1. Clicca su "Carica JSON (veloce)"
2. Scarica automaticamente da GitHub il file sinonimi-master.json
3. Si carica in ~2-3 secondi
4. Salvato in cache locale per accessi futuri
```

**Vantaggi:**
- Velocissimo
- Aggiornamenti automatici se disponibili
- Una sola azione

#### Opzione B: Carica da File HTML (Manuale)
```
1. Clicca su "Carica file HTML (parsing completo)"
2. Seleziona uno o più file .html con tabelle di sinonimi
3. Il tool parsa automaticamente le tabelle
4. Converte in JSON e salva in cache
```

**Quando usare:**
- Hai file HTML locali legacy
- Vuoi customizzare il dizionario
- Offline non hai accesso a GitHub

---

## 🔍 Funzionalità di Ricerca

### Ricerca Base
```
Digita una parola: "mare"
↓
Mostra tutti i lemmi che INIZIANO con "mare"
Esempio: mare, mareggiata, mare-nostrum
```

### Ricerca con Wildcard (Pattern Matching)

#### 1. **Inizio Parola** (`*end`)
```
Inserisci: *ato
Trova: stato, prato, gatto, atto, fatto
Logica: qualsiasi parola che TERMINA con "ato"
```

#### 2. **Fine Parola** (`iniz*`)
```
Inserisci: mar*
Trova: mare, marcia, marmo, martedì, marito
Logica: qualsiasi parola che INIZIA con "mar"
```

#### 3. **Ovunque** (`*nel*`)
```
Inserisci: *nel*
Trova: canello, cenere, connessione, fenello
Logica: qualsiasi parola che CONTIENE "nel"
```

#### 4. **Ricerca Esatta** (nessun asterisco)
```
Inserisci: amore
Trova: SOLO "amore" (nessuna variante)
```

### Ricerca nei Sinonimi (Toggle)
```
Checkbox: "Cerca anche nei sinonimi e contrari"

DISABILITATO (default):
- Cerca solo nei lemmi principali

ABILITATO:
- Cerca nei sinonimi
- Cerca nei contrari
- Molto più potente ma lento su dataset grandi
```

**Esempio:**
```
Ricerca: "felice" senza toggle
Risultato: "felice" (lemma principale)

Ricerca: "felice" CON toggle
Risultati: 
- felice (lemma)
- contento (sinonimo di felice)
- allegro (sinonimo di felice)
- triste (contrario di felice)
- infelice (contrario di felice)
```

---

## 💾 Caching e Storage

### Come Funziona

```
Primo accesso:
1. Scarica JSON da GitHub (~2MB)
2. Controlla se localStorage ha spazio (<4MB)
3. Se sì: salva in cache locale
4. Se no: usa solo da GitHub (più lento)

Accessi successivi:
1. Legge da cache locale (instantaneo)
2. Controlla versione (VERSION_KEY)
3. Se versione è aggiornata: riusa cache
4. Se versione è vecchia: scarica nuovo
```

### Gestione Manuale Cache

#### Visualizzare Storage Usato
```
Barra info in alto a destra:
"Versione 1.0.0"
↓
Mostra spazio usato dal dizionario nel tuo browser
```

#### Cancellare Cache
```
Pulsante rosso "X" nella barra di ricerca
↓
Cancella dizionario salvato
↓
Prossimo accesso: ricarica da GitHub
```

### Limiti e Quote

| Storage | Limite | Dizionario |
|---------|--------|-----------|
| localStorage | 5-10 MB | ~2 MB (sempre ok) |
| sessionStorage | 5-10 MB | ~2 MB (sempre ok) |
| IndexedDB | 50 MB+ | Non usato (più complesso) |

**Se il dizionario è >4MB:**
```
❌ NON salva in cache automaticamente
✓ Carica sempre da GitHub (più lento)
ℹ️ Avviso nella UI: "Troppo grande per cache"
```

---

## 🌐 Struttura Dati JSON

### Formato del Dizionario

```json
[
  {
    "lemma": "amore",
    "sinonimi": ["affetto", "ardore", "amore", "caro", "carizia"],
    "contrari": ["odio", "disprezzo", "avversione"]
  },
  {
    "lemma": "mare",
    "sinonimi": ["oceano", "pelagico", "talasso", "tirreno"],
    "contrari": ["terra", "continente", "terraferma"]
  }
]
```

### Campi

| Campo | Tipo | Descrizione |
|-------|------|------------|
| **lemma** | string | Parola principale (headword) |
| **sinonimi** | array | Lista di sinonimi (1-50 termini) |
| **contrari** | array | Lista di contrari/antonimi (0-20 termini) |

### Normalizzazione Automatica

Se il JSON ha formato misto:

```json
// ❌ Formato misto (non ideale)
{
  "lemma": "bella",
  "sinonimi": "gradevole, affascinante, avvenente"  // string!
}

// ✅ Viene convertito automaticamente a:
{
  "lemma": "bella",
  "sinonimi": ["gradevole", "affascinante", "avvenente"]  // array!
}
```

---

## 📤 Export Dati

### Scarica JSON Completo

```
Pulsante: "Export" → "Scarica JSON"
↓
File: sinonimi-master.json
↓
Contiene: Tutti i lemmi nel tuo dispositivo
↓
Formato: UTF-8 con indentazione (leggibile)
```

### Copia negli Appunti

```
Pulsante: "Export" → "Copia negli appunti"
↓
Tutto il JSON copiato
↓
Incolla dove vuoi: text editor, email, database
```

### Casi d'Uso

**Backup Personale:**
```
Scarica JSON periodicamente per backup
Conservalo localmente in caso di problemi
```

**Integrazione in Progetti:**
```
Scarica JSON
Usalo nel tuo progetto/app
Processalo con Python/Node/etc.
```

**Condivisione:**
```
Copia negli appunti
Condividi con collaboratori
Colla in un file shared
```

---

## ⚙️ Configurazione Tecnica

### Tecnologie

| Componente | Dettagli |
|-----------|----------|
| **Frontend** | React 18 (CDN, no build) |
| **Styling** | Tailwind CSS (CDN) |
| **Storage** | localStorage + sessionStorage |
| **Data** | JSON statico (GitHub raw) |
| **UI** | Vanilla HTML5 |
| **Icons** | Emoji + SVG inline |

### Browser Supportati

```
✅ Chrome/Chromium 90+
✅ Firefox 88+
✅ Safari 14+
✅ Edge 90+
✅ Opera 76+
✅ Mobile (iOS Safari, Chrome mobile)
```

### Performance

| Operazione | Tempo | Note |
|-----------|-------|------|
| Caricamento HTML | <500ms | Velocissimo |
| Fetch JSON (primo) | 1-3s | Da GitHub, dipende da ISP |
| Ricerca 1 termine | <50ms | Locale, instantaneo |
| Ricerca wildcard | 50-200ms | Dipende da pattern |
| Ricerca nei sinonimi | 200-1000ms | Più lenta su dataset grande |
| Export JSON | <100ms | Generazione locale |

### Requisiti Minimi

```
RAM: 50 MB (app + dizionario)
Storage: 10 MB (per cache)
Connessione: 2 Mbps (primo caricamento)
CPU: Qualsiasi (JavaScript moderno, niente GPU)
```

---

## 📱 PWA - Installa come App

### Cos'è una PWA?

Una **Progressive Web App** è un'app web che puoi installare come nativa sul tuo dispositivo.

### Come Installare

#### Desktop (Chrome/Edge)

```
1. Visita https://infingardo.github.io/sinonimi-dizionario/
2. Guarda in alto a destra nella barra dell'indirizzo
3. Clicca sull'icona "Installa" (computer con freccia) oppure menu ⋮
4. Clicca "Installa"
5. L'app compare nel menu Start/Applications
```

#### Mobile iOS (iPhone/iPad)

```
1. Apri Safari
2. Vai a https://infingardo.github.io/sinonimi-dizionario/
3. Clicca il pulsante "Condividi" (freccia verso l'alto in basso)
4. Scorri e seleziona "Aggiungi a Home"
5. Clicca "Aggiungi"
6. L'app compare nella home screen
```

#### Mobile Android (Chrome)

```
1. Apri Chrome
2. Vai a https://infingardo.github.io/sinonimi-dizionario/
3. Clicca il menu ⋮ (tre puntini)
4. Clicca "Installa app"
5. Clicca "Installa"
6. L'app compare nel drawer delle app
```

### Vantaggi PWA

```
✓ Launch rapido (scorciatoia dalla home)
✓ Funziona offline (con cache precondizionata)
✓ Niente app store
✓ Aggiornamenti automatici
✓ Full screen (senza barra del browser)
✓ Stesso codice web (no compilazione)
```

---

## 🎯 Casi d'Uso

### Scrittori e Copywriter
```
Cerca sinonimi mentre scrivi per evitare ripetizioni
Es: "Bella" → sinonimi: gradevole, affascinante, incantevole, attraente
```

### Studenti di Italiano
```
Impara sinonimi e contrari
Comprendi sfumature semantiche tra parole simili
```

### Insegnanti
```
Risorse didattiche
Esercizi di vocabolario
```

### Sviluppatori
```
Integra il dizionario nei tuoi progetti
Scarica JSON e processalo
```

### Programmatori Generazione Testo
```
Usa il dizionario per parafrasi
Evita ripetizioni in testi automatici
```

---

## 🔧 Troubleshooting

### Problema: Dizionario non carica
**Causa:** Connessione internet assente
**Soluzione:** 
- Controlla la connessione
- Se è la prima volta, devi online per scaricare da GitHub
- Successivamente: usa cache locale (offline ok)

### Problema: "Carica JSON (veloce)" non funziona
**Causa:** GitHub non raggiungibile o CORS bloccato
**Soluzione:**
- Scarica manualmente da: `https://raw.githubusercontent.com/Infingardo/sinonimi-dizionario/main/sinonimi-master.json`
- Carica il file con "Carica file HTML"

### Problema: Ricerca è lentissima
**Causa:** Toggle "Cerca nei sinonimi" è acceso su dataset grande
**Soluzione:**
- Disabilita il toggle se non lo usi
- Usa wildcard specifici (es: `mar*` invece di `*ar*`)

### Problema: Cache non salva
**Causa:** localStorage pieno o disabilitato
**Soluzione:**
- Cancella cache di altri siti
- Abilita localStorage nelle impostazioni browser
- Se >4MB: il tool usa GitHub (normale)

### Problema: Risultati di ricerca inaspettati
**Causa:** Wildcard mal interpretato
**Soluzione:**
```
⚠️ Ricorda:
- "mare*" = inizia con "mare"
- "*mare" = termina con "mare"
- "*mare*" = contiene "mare"
- "mare" = esattamente "mare"
```

### Problema: Emoji non visualizzati
**Causa:** Font vecchio o compatibilità browser
**Soluzione:**
- Aggiorna browser
- Non è critico - sono solo icone decorative

---

## 📊 Statistiche Dizionario

| Metrica | Valore | Note |
|---------|--------|------|
| **Lemmi Totali** | 14,000+ | Parole principali |
| **Sinonimi Medi** | 5-8 per lemma | Range variabile |
| **Contrari Medi** | 2-4 per lemma | Quando presenti |
| **Dimensione File** | ~2 MB | JSON non compresso |
| **Linguaggio** | Italiano | Standard italiano moderno |
| **Copertura** | Sostantivi, Aggettivi, Verbi, Avverbi | Principali categorie |

---

## 🔄 Aggiornamenti

### Versionamento

```
Versione 1.0.0: Release iniziale
VERSION_KEY: salva versione in localStorage

Quando GitHub viene aggiornato:
1. Nuova versione (es. 1.0.1)
2. Al prossimo accesso: detect versione vecchia
3. Scarica nuovo JSON
4. Aggiorna cache
5. Zero downtime
```

### Come Forzare Aggiornamento

```
1. Clicca il pulsante rosso "X" (cancella cache)
2. Ricarica la pagina (F5)
3. Clicca "Carica JSON" per scaricare versione fresca
```

---

## 🔐 Privacy e Dati

### Politica Dati

```
✅ ZERO tracciamento
✅ ZERO cookie di terze parti
✅ ZERO dati caricati su server
✅ ZERO analytics
✅ Tutto locale (localStorage)
✅ Codice open-source (GitHub)
```

### Storage Locale

```
I tuoi dati rimangono nel tuo dispositivo:
- localStorage: dizionario in cache
- sessionStorage: state temporaneo sessione
- IndexedDB: non usato

Cancellazione:
- Clicca "X" → cancella dizionario
- Clear browser data → cancella localStorage
```

### Connessione a GitHub

```
⚠️ PRIMO CARICAMENTO ONLY:
- Connessione HTTP a raw.githubusercontent.com
- IP tuo visibile a GitHub
- File JSON trasferito (no tracking)

SUCCESSIVAMENTE:
- Usa cache locale
- Nessuna connessione esterna
- Completamente offline
```

---

## 📚 Fonte Dati

### Origine Dizionario

```
Fonte: Dizionario vintage restaurato digitalmente
Anno originale: Inizio 1900s (Larousse italiano)
Restauro digitale: 2024
Formattazione: JSON moderno

Qualità: Affidabile e completato
Copertura: Lessico italiano standard
```

### Contributi Miglioramenti

Se trovi errori o vuoi suggerimenti:

1. **Fork** il repository GitHub
2. **Modifica** il file JSON
3. **Commit** con descrizione
4. **Pull Request** con i miglioramenti

Repository: `https://github.com/Infingardo/sinonimi-dizionario`

---

## 🛠️ Manutenzione

### Backup Dati

```
Scarica regolarmente il JSON:
1. Clicca Export → Scarica JSON
2. Salva il file nel tuo backup
3. Data: inclusa nel nome file (sinonimi-master.json)
```

### Monitoraggio

```
Se noti lentezza:
1. Controlla console browser (F12)
2. Vedi se ci sono errori
3. Segnala su GitHub Issues
```

### Supporto

```
❓ Domande: apri Issue su GitHub
🐛 Bug: descrivi con screenshot
💡 Suggerimenti: proponi feature
```

---

## 📄 Licenza

**Creative Commons Attribution 4.0 International (CC BY 4.0)**

```
✅ Puoi: usare, modificare, distribuire, commercializzare
❌ Devi: dar credito (menzione autore + fonte)
⚠️ Warranty: NESSUNA - usi a tuo rischio
```

---

## 👨‍💻 Autore e Ringraziamenti

### Sviluppatore

**Filippo**
- Direttore, Sezione Anatomia Patologica
- ASST Fatebenefratelli-Sacco, Milano
- GitHub: [@Infingardo](https://github.com/Infingardo)

### Tech Stack Ringraziamenti

- **React 18** - UI library
- **Tailwind CSS** - Styling
- **GitHub Pages** - Hosting gratuito
- **Larousse** - Dizionario vintage originale

---

## 📞 Contatti e Link Utili

| Link | Descrizione |
|------|------------|
| [Live App](https://infingardo.github.io/sinonimi-dizionario/) | Accedi al dizionario online |
| [GitHub Repository](https://github.com/Infingardo/sinonimi-dizionario) | Codice sorgente |
| [JSON Download](https://raw.githubusercontent.com/Infingardo/sinonimi-dizionario/main/sinonimi-master.json) | Scarica dati direttamente |
| [Dashboard](https://infingardo.github.io/) | Home di tutti i progetti |
| [Issues](https://github.com/Infingardo/sinonimi-dizionario/issues) | Segnala bug |

---

**Versione**: 1.0.0
**Data**: Novembre 2025
**Status**: Production-ready
**Last Updated**: 2025-11-16

---

*"Le parole sono il vestito dei pensieri"* - Samuel Johnson

Buona ricerca! 📚✨
