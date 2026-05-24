# Nauczyciel — Aplikacja do nauki

Autonomiczna aplikacja edukacyjna oparta na Claude API. Prowadzi ucznia przez 5 etapów lekcji i generuje ściągę PDF do wydruku.

## Struktura projektu

```
nauczyciel-app/
├── public/
│   └── index.html          # Frontend (cała aplikacja)
├── netlify/
│   └── functions/
│       └── chat.js         # Backend serverless (proxy API)
├── netlify.toml            # Konfiguracja Netlify
└── README.md
```

## Wdrożenie na Netlify (darmowe)

### Krok 1 — Wgraj projekt na GitHub

```bash
cd nauczyciel-app
git init
git add .
git commit -m "Nauczyciel app"
git remote add origin https://github.com/TWOJ_LOGIN/nauczyciel-app.git
git push -u origin main
```

### Krok 2 — Połącz z Netlify

1. Wejdź na https://netlify.com i zaloguj się (lub zarejestruj — bezpłatnie)
2. Kliknij **"Add new site" → "Import an existing project"**
3. Wybierz GitHub i autoryzuj dostęp
4. Wybierz repozytorium `nauczyciel-app`
5. Ustawienia budowania zostaw domyślne (netlify.toml zadba o resztę)
6. Kliknij **"Deploy site"**

### Krok 3 — Dodaj klucz API

1. W Netlify wejdź w **Site settings → Environment variables**
2. Dodaj zmienną:
   - Klucz: `ANTHROPIC_API_KEY`
   - Wartość: Twój klucz z https://console.anthropic.com
3. Kliknij **"Save"**
4. Wróć do **Deploys** i kliknij **"Trigger deploy"**

### Krok 4 — Gotowe!

Netlify wygeneruje link np. `https://nauczyciel-xyz.netlify.app` — udostępnij go komukolwiek.

---

## Alternatywa: Vercel

```bash
npm i -g vercel
cd nauczyciel-app
vercel
```

Potem w Vercel Dashboard dodaj `ANTHROPIC_API_KEY` w **Settings → Environment Variables**.

Uwaga: przy Vercel funkcja serverless musi być w folderze `/api/` — przenieś `chat.js` do `api/chat.js` i dostosuj `API_URL` w `index.html` na `/api/chat`.

---

## Lokalne uruchomienie (bez serwera)

Wymaga Netlify CLI:

```bash
npm install -g netlify-cli
cd nauczyciel-app
echo "ANTHROPIC_API_KEY=twoj_klucz" > .env
netlify dev
```

Otwórz http://localhost:8888

---

## Funkcjonalności

- **5 etapów lekcji**: profil ucznia → analogia → pytania sokratejskie → quiz → tekst z lukami
- **Interaktywne wybory**: klikalne przyciski A/B i A/B/C/D (nie trzeba nic pisać)
- **Personalizacja**: analogie oparte na opisie doświadczeń ucznia
- **Dynamiczny poziom trudności**: dostosowuje się do jakości odpowiedzi
- **Ściąga PDF**: generowana po lekcji, gotowa do wydruku z lukami do uzupełnienia
- **Responsywna**: działa na telefonie i komputerze
- **Bezpieczna**: klucz API nigdy nie trafia do przeglądarki
