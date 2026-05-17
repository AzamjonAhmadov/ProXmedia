# mobilography-web

> Powered by **MKM777**

Bu **mobilography** Flutter ilovasining tayyor web build'i. GitHub Pages uchun
sozlangan — push qilsangiz, sayt bevosita ishlaydi.

---

## GitHub'ga yuklash (3 qadam)

### 1. GitHub'da yangi repository yarating

[github.com/new](https://github.com/new) — nomi: **`mobilography-web`**
(boshqa nom tanlasangiz, `base-href`'ni qayta build qilish kerak bo'ladi)

### 2. Lokal repo'ni push qiling

```bash
cd ~/Desktop/mobilography-web
git remote add origin https://github.com/<sizning-username>/mobilography-web.git
git branch -M main
git push -u origin main
```

### 3. GitHub Pages'ni yoqing

Repository → **Settings** → **Pages** → *Build and deployment*:

- **Source:** `Deploy from a branch`
- **Branch:** `main` / `/ (root)` → **Save**

Bir necha daqiqadan so'ng saytingiz ushbu manzilda ochiladi:

```
https://<sizning-username>.github.io/mobilography-web/
```

---

## Lokal ko'rish (test uchun)

Flutter web faylini to'g'ridan-to'g'ri brauzerda ochib bo'lmaydi (CORS sababli).
Lokal server kerak:

```bash
cd ~/Desktop/mobilography-web
python3 -m http.server 8000
# brauzerda: http://localhost:8000/
```

> ℹ️ `index.html` `/mobilography-web/` base-path'ga sozlangan. Lokal test uchun
> URL `http://localhost:8000/mobilography-web/` bo'lishi shart **emas** —
> Flutter avtomatik moslashadi.

---

## Tuzilishi

```
mobilography-web/
├── index.html                # Asosiy kirish nuqtasi
├── 404.html                  # SPA routing uchun (index.html nusxasi)
├── main.dart.js              # Flutter web bundle (~3 MB)
├── flutter.js                # Flutter loader
├── flutter_bootstrap.js      # Flutter init
├── flutter_service_worker.js # PWA service worker
├── manifest.json             # PWA manifest
├── favicon.png               # Favicon
├── version.json              # Build versiyasi
├── .nojekyll                 # GitHub Pages — Jekyll'ni o'chiradi
├── assets/                   # Rasmlar, fontlar, fontTree-shake
├── canvaskit/                # Flutter renderer (WebAssembly)
├── icons/                    # PWA app iconlar
└── .github/workflows/        # Auto-deploy GitHub Action
```

---

## Qayta build qilish

Source kod boshqa repo'da (`mobilography`). U yerda:

```bash
flutter build web --release --base-href "/mobilography-web/"
cp -R build/web/. ~/Desktop/mobilography-web/
cd ~/Desktop/mobilography-web && git add . && git commit -m "rebuild" && git push
```

---

## Xavfsizlik eslatmasi

- API kalitlari (Supabase / Firebase) `main.dart.js` ichiga embed bo'lgan.
- Supabase **anon key** va Firebase **public web key** mijoz tomonda
  bo'lishi normal — ammo Supabase Row Level Security (RLS) qoidalari
  yoqilganligiga ishonch hosil qiling.
- Admin parol (`ADMIN_PASSWORD`) ham bundle ichida — kuchli parol qo'ying
  va kerak bo'lsa rotate qiling.

---

© 2026 MKM777. All rights reserved.
