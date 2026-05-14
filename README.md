# Vyhledávač obědů

Jednoduchá webová aplikace pro vyhledávání jídel školní jídelny podle názvu s ukázkou fotky.

## Jak to funguje

Každý den ráno Make automaticky stáhne jídelní lístek ze školní jídelny a uloží názvy jídel a fotky do Google Sheets. Tato stránka umožňuje vyhledávat v historii jídel podle názvu — užitečné při objednávání obědů, kdy jsou dostupné pouze názvy bez fotek.

## Technologie

- **Frontend** — statická HTML stránka hostovaná na GitHub Pages
- **Backend** — Google Apps Script (REST API nad Google Sheets)
- **Automatizace** — Make (dříve Integromat)
- **Úložiště fotek** — Google Drive

## Funkce

- Vyhledávání bez diakritiky (špagety = spagety)
- Mobilní zobrazení
- Fotky jídel z archivu školní jídelny
