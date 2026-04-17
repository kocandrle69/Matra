# Mantra tracker

PWA pro sledování Mantra a Tantra Deeksha opakování.

## Nasazení — krok za krokem

### 1. Supabase — databáze

1. Otevři [supabase.com](https://supabase.com) a přihlas se do projektu
2. Vlevo: **SQL Editor** → **New query**
3. Zkopíruj obsah souboru `supabase-setup.sql` a klikni **Run**
4. Vlevo: **Authentication → URL Configuration**
   - Site URL: `https://kocandrle69.github.io/Matra/`
   - Redirect URLs: přidej `https://kocandrle69.github.io/Matra/`
5. Vlevo: **Settings → API**
   - Zkopíruj **Project URL** a **anon public** klíč

### 2. index.html — doplnit klíč

Otevři `index.html` a na řádku s `SUPABASE_ANON_KEY` nahraď
`'REPLACE_WITH_YOUR_ANON_KEY'` svým anon klíčem ze Supabase.

```js
const SUPABASE_ANON_KEY = 'eyJhbGci...'; // tvůj klíč
```

### 3. Ikony (volitelné, ale doporučené)

Přidej do složky soubory:
- `icon-192.png` (192×192 px)
- `icon-512.png` (512×512 px)

Stačí jednoduchá ikona s písmenem "M" na šafránovém pozadí.

### 4. GitHub Pages

```bash
git clone https://github.com/kocandrle69/Matra.git
# zkopíruj soubory z tohoto adresáře do klonované složky
git add .
git commit -m "Initial deploy"
git push
```

Pak v GitHub repozitáři:
- **Settings → Pages → Source: Deploy from a branch**
- Branch: `main` / `master`, složka: `/ (root)`
- Ulož → za ~1 minutu bude appka na `https://kocandrle69.github.io/Matra/`

## Soubory

| Soubor | Popis |
|--------|-------|
| `index.html` | Celá aplikace (single file PWA) |
| `manifest.json` | PWA manifest — název, barvy, ikony |
| `sw.js` | Service worker — offline podpora |
| `supabase-setup.sql` | SQL skript pro vytvoření tabulek |

## Levely

| Level | Opakování | Mály | Agiyari mály |
|-------|-----------|------|--------------|
| Mantra Deeksha 0 | 125 000 | 1 158 | 116 |
| Tantra Deeksha 1 | 250 000 | 2 315 | 232 |
| Tantra Deeksha 2 | 600 000 | 5 556 | 556 |
| Tantra Deeksha 3 | 600 000 | 5 556 | 556 |
| Tantra Deeksha 4 | 250 000 | 2 315 | 232 |
| Tantra Deeksha 5 | 500 000 | 4 630 | 463 |
