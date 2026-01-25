# Dizionario dei Sinonimi

Interfaccia web per la consultazione di sinonimi e contrari italiani. Restauro digitale del dizionario [Homolaicus](https://www.homolaicus.com/linguaggi/sinonimi/).

**[→ Usa il dizionario](https://infingardo.github.io/sinonimi-dizionario/)**

---

## Cosa fa

- **14.000+ lemmi** italiani con sinonimi e contrari
- **Ricerca con wildcard**: `mare*` (inizia con), `*mare` (finisce con), `*mare*` (contiene)
- **Ricerca nei sinonimi/contrari** (toggle opzionale)
- **Normalizzazione accenti**: "perche" trova "perché"
- **Highlighting** dei termini matchati
- **Cache locale** con localStorage (funziona offline dopo il primo caricamento)
- **PWA installabile** su mobile e desktop
- **Funziona offline** dopo il primo accesso (service worker)

---

## Come usare

1. Vai su https://infingardo.github.io/sinonimi-dizionario/
2. Il dizionario si carica automaticamente da GitHub (~2MB)
3. Digita una parola e premi invio

### Wildcard

| Pattern | Significato | Esempio |
|---------|-------------|---------|
| `mare` | esattamente "mare" | mare |
| `mare*` | inizia con "mare" | mare, mareggiata, marea |
| `*mare` | finisce con "mare" | altamare |
| `*mare*` | contiene "mare" | amareggiato, maremoto |

### Cerca nei sinonimi

Attiva il checkbox "Cerca anche nei sinonimi e contrari" per trovare lemmi che contengono il termine cercato tra i loro sinonimi o contrari. Più lento, ma più potente.

---

## Tecnologie

- **React 18** (UMD, no build)
- **Tailwind CSS** (CDN)
- **localStorage** per caching
- **Zero dipendenze server** — tutto client-side

Single HTML file, deployabile ovunque.

---

## Struttura dati

```json
[
  {
    "lemma": "amore",
    "sinonimi": ["affetto", "ardore", "passione"],
    "contrari": ["odio", "avversione"]
  }
]
```

Il JSON completo è disponibile su: [`sinonimi-master.json`](https://raw.githubusercontent.com/Infingardo/sinonimi-dizionario/main/sinonimi-master.json)

---

## Limitazioni note

- **localStorage**: limite ~5MB, sincrono. Con 14k lemmi va bene. Se i dati crescessero molto, servirebbe IndexedDB.
- **Ricerca O(n)**: filtra tutti i lemmi ad ogni ricerca. Con debounce 300ms e 14k lemmi, non è un problema.

---

## Crediti

**Dati**: [Homolaicus - Dizionario dei Sinonimi](https://www.homolaicus.com/linguaggi/sinonimi/) di Enrico Galavotti

**Licenza dati**: [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/)

**Interfaccia web**: [Infingardo](https://github.com/Infingardo)

---

## Changelog

### v1.1.0
- Debounce 300ms sulla ricerca
- Normalizzazione accenti (NFD)
- Highlighting termini matchati nei sinonimi/contrari
- Crediti Homolaicus nel footer
- Icona cestino per clear cache con tooltip
- **Service worker per offline completo**

### v1.0.0
- Release iniziale

---

## Licenza

Interfaccia: MIT

Dati: CC-BY 4.0 (Homolaicus)
