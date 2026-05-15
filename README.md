# Vyhledávač obědů

Webová aplikace pro vyhledávání jídel školní jídelny podle názvu s ukázkou fotky. Vznikla jako řešení problému — při objednávání obědů jsou dostupné pouze názvy jídel bez fotek, takže je těžké odhadnout, co dítě dostane.

## Jak to funguje

### Sběr dat
Každý všední den ráno Make automaticky navštíví web školní jídelny, stáhne jídelní lístek pro daný den a pošle e-mail s názvy jídel a fotkami na rodinné e-maily.

### Automatické budování databáze
Google Apps Script se každý den v 7:25 podívá do Gmailu, najde dnešní e-mail s jídelníčkem a zpracuje ho:
- Vytáhne názvy jídel a URL fotek
- Zkontroluje, zda jídlo už v databázi není
- Pokud ne, stáhne fotku na Google Drive a přidá záznam do Google Sheets

### Vyhledávání
Statická HTML stránka na GitHub Pages umožňuje vyhledávat v databázi jídel. Frontend volá Google Apps Script jako REST API, které prohledá Google Sheets a vrátí výsledky.

## Technologie

- **Frontend** — statická HTML stránka na GitHub Pages
- **Backend** — Google Apps Script (REST API nad Google Sheets)
- **Databáze** — Google Sheets (název jídla, typ, URL fotky)
- **Úložiště fotek** — Google Drive
- **Automatizace e-mailu** — Make (dříve Integromat)

## Funkce vyhledávače

- Vyhledávání bez diakritiky (špagety = spagety)
- Zvýraznění hledaného řetězce v názvu jídla
- Mobilní layout — fotka přes celou šířku
- Zavření klávesnice po zadání dotazu
- Animovaný loader během čekání na výsledky

## Struktura projektu

```
Google Drive/
└── Obědy projekt/
    ├── Obědy databáze 3      ← Google Sheets s databází jídel
    ├── Obědy fotky/          ← složka se staženými fotkami
    └── Apps Script projekt   ← backend + automatizace

GitHub/
└── obed-vyhledavac/
    └── index.html            ← frontend
```

## Apps Script funkce

| Funkce | Popis |
|---|---|
| `zpracujDnesniEmail()` | Spouští se denně v 7:25, zpracuje dnešní e-mail |
| `hledejJidla(dotaz)` | REST endpoint pro vyhledávání |
| `importObedy()` | Jednorázový import historických e-mailů |
| `stahniFotky()` | Jednorázové stažení fotek na Drive |
| `odstranDuplikaty()` | Jednorázové čištění duplikátů |
| `odstranBezFotky()` | Jednorázové odstranění řádků bez fotky |
