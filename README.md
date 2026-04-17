# Mantra tracker

Webová PWA aplikace pro sledování pokroku při Mantra a Tantra Deeksha. Každý uživatel má vlastní data rozdělená podle levelu. Funguje na mobilu, tabletu i počítači — přidej si ji na plochu jako klasickou appku.

**Live:** [kocandrle69.github.io/Matra](https://kocandrle69.github.io/Matra/)

---

## Co aplikace umí

- Sledování počtu mál a opakování pro každý level zvlášť
- Oddělené záznamy pro standardní sezení a sezení při agiyari
- Kontrola pravidla agiyari — počet mál při agiyari nesmí přesáhnout 10 % aktuálně provedeného počtu opakování
- Vizuální progress bar s červenou čárou aktuálního maxima agiyari
- Přepínání mezi levely bez ztráty dat — každý level má vlastní historii
- Přihlášení e-mailem a heslem (funguje na iOS PWA, Safari, Chrome i Android)
- Tři jazyky: čeština, angličtina, hindština

---

## Levely

| Level | Opakování | Mály | Agiyari mály |
|-------|-----------|------|--------------|
| Mantra Deeksha 0 | 125 000 | 1 158 | 116 |
| Tantra Deeksha 1 | 250 000 | 2 315 | 232 |
| Tantra Deeksha 2 | 600 000 | 5 556 | 556 |
| Tantra Deeksha 3 | 600 000 | 5 556 | 556 |
| Tantra Deeksha 4 | 250 000 | 2 315 | 232 |
| Tantra Deeksha 5 | 500 000 | 4 630 | 463 |

---

## Přidat aplikaci na plochu

**Android (Chrome):** tečky vpravo nahoře → Přidat na úvodní obrazovku

**iOS (Safari):** tlačítko sdílení → Přidat na plochu

**PC (Chrome):** ikona instalace v adresním řádku nebo Menu → Nainstalovat aplikaci

---

## Technický stack

| Vrstva | Technologie |
|--------|-------------|
| Frontend | Single-file HTML/CSS/JS, PWA |
| Hosting | GitHub Pages |
| Databáze | Supabase (PostgreSQL) |
| Auth | Supabase Auth — e-mail + heslo |
| Email | Resend (SMTP) |

---

## Struktura souborů

| Soubor | Popis |
|--------|-------|
| `index.html` | Celá aplikace |
| `manifest.json` | PWA manifest |
| `sw.js` | Service worker — HTML se nikdy necachuje |
| `supabase-setup.sql` | Počáteční SQL schéma |
| `supabase-migration-01.sql` | Migrace — přidání sloupce `level` do sessions |

---

## Nasazení od nuly

### 1. Supabase

1. Vytvoř projekt na [supabase.com](https://supabase.com)
2. **SQL Editor → New query** → spusť `supabase-setup.sql`
3. **Authentication → Sign In / Providers → Email** → vypni **Confirm email** → Save
4. **Authentication → Email** → nastav vlastní SMTP (doporučeno: [resend.com](https://resend.com))
5. **Settings → API** → zkopíruj Project URL a anon public klíč

### 2. index.html

Nahraď placeholder na dvou místech:

```js
const SUPABASE_URL = 'https://TVUJ-PROJEKT.supabase.co';
const SUPABASE_ANON_KEY = 'eyJhbGci...';
```

### 3. Ikony (volitelné)

Přidej `icon-192.png` a `icon-512.png` pro pěknou ikonku na ploše.

### 4. GitHub Pages

```bash
git add .
git commit -m "deploy"
git push
```

**Settings → Pages → Source: Deploy from a branch → main → / (root)**

Za ~1 minutu běží na `https://TVUJ-LOGIN.github.io/REPO/`

### 5. Migrace (pokud upgraduješ existující instalaci)

Pokud jsi měl aplikaci nasazenou před přidáním podpory více levelů, spusť v Supabase SQL Editor:

```sql
ALTER TABLE public.sessions ADD COLUMN IF NOT EXISTS level text NOT NULL DEFAULT '0';
UPDATE public.sessions s
SET level = (SELECT p.level FROM public.profiles p WHERE p.id = s.user_id);
```

---

## Pravidla agiyari

Mála odříkaná při zapáleném agiyari se evidují jako agiyari sezení. Platí:

> Celkový počet agiyari mál nesmí v žádném okamžiku přesáhnout **10 %** celkového počtu dosud provedených opakování.

Po dokončení cílového počtu opakování **i** agiyari části (10 % z cíle) lze požádat gurua o postup do dalšího levelu.
