# Ziyofat — premium restoran landing (bitta HTML fayl)

Zamonaviy **o‘zbek–xalqaro fusion** restoran uchun yagona `index.html`: **Tailwind CSS (CDN)**, **Font Awesome 6**, minimal **vanilla JavaScript**. Dizayn — iliq qizil (#9F1239), boy oltin (#D4AF37), kulrang charcoal (#111827) va krem fon.

## Tezkor boshlash

1. `index.html`ni ikki marta oching yoki oddiy HTTP server orqali ko‘ring (masalan, VS Code **Live Server**).
2. Internet kerak: Tailwind CDN, shriftlar, rasmlar (Unsplash) va xarita embed tashqi manbadan yuklanadi.

---

## Shriftlar (Google Fonts)

Saytda ulangan juftlik:

| Rol | Shrift | Qayerda |
|-----|--------|---------|
| Sarlavhalar (`font-display`) | **Playfair Display** | Hero, bo‘lim sarlavhalari, taom nomlari |
| Matn va tugmalar (`font-sans`) | **Outfit** | Navbar, paragraflar, forma |

Ulanish `<head>` ichida — `fonts.googleapis.com` link orqali; `:root` da `--font-display` va `--font-sans` CSS o‘zgaruvchilari Tailwind `fontFamily` bilan bog‘langan.

**Almashtirish:** Google Fonts dan boshqa shrift tanlang → yangi `<link href="https://fonts.googleapis.com/css2?family=...">` qo‘ying → `:root` dagi `--font-display` / `--font-sans` nomlarini yangilang.

---

## Restoran nomi va logo

| Nima | Qayerda |
|------|---------|
| Brauzer tab sarlavhasi | `<title>...</title>` va `<meta name="description">` |
| Navbar va footer’dagi nom | Matn `Ziyofat` — qidiruv (Ctrl+F): `Ziyofat` |
| Logo harfi `Z` | `<header>` ichidagi dumaloq gradient — ichidagi `Z` harfini SVG yoki boshqa belgi bilan almashtiring |
| Placeholder | Nomni `[Restaurant Name]` qilib qoldirmoqchi bo‘lsangiz, barcha “Ziyofat” joylarini shu bilan almashtiring |

**Maslahat:** Logo rasmini qo‘shish uchun navbar ichidagi `<span class="flex h-10 w-10...">Z</span>` blokini `<img src="logo.svg" alt="..." class="h-10 w-auto" />` bilan almashtiring (rasmni `index.html` yoniga qo‘yganingizda yo‘lni to‘g‘ri yozing).

---

## Ranglar palitrasi

Ranglar Tailwind konfiguratsiyasida — `index.html` ichidagi:

```html
<script src="https://cdn.tailwindcss.com"></script>
<script>
  tailwind.config = {
    darkMode: "class",
    theme: {
      extend: {
        colors: {
          wine: { DEFAULT: "#9F1239", ... },
          gold: { DEFAULT: "#D4AF37", ... },
          charcoal: "#111827",
          cream: { DEFAULT: "#FDF8F3", ... },
```

- **Asosiy qizil:** `wine` (`#9F1239`)
- **Oltin:** `gold` (`#D4AF37`)
- **Matn fon:** `cream` / qorong‘i rejimda `charcoal`

O‘zgartirish: yuqoridagi hex kodlarni almashtiring, kerak bo‘lsa `tailwind.config` ichiga yangi nom qo‘shing (masalan `wine.light`).

---

## Matnlarni tahrirlash

Faylda **`EDIT:`** yoki **`═══ EDIT:`** bilan belgilangan izohlarga yaqin bloklarda:

- Hero sarlavha va subtitle
- “Biz haqimizda” bo‘limi
- Menyu kartalari (nom, tavsif, narx)
- Shef tavsiyasi (maxsus taklif)
- Aloqa (manzil, telefon, email)
- Footer ijtimoiy havolalar (`href="#"`)
- O‘ngdagi suzuvchi **Telegram** — `href="https://t.me/..."` (`@username` ni o‘z kanalingiz/botingizga mos qiling)

Matnlar o‘zbek tilida; boshqa til uchun shu bloklarni almashtiring.

---

## Rasmlar (Unsplash / Pexels)

Barcha rasmlar **to‘g‘ridan-to‘g‘ri URL** orqali:

- **Hero fon:** `#heroBg` inline `background-image` yoki style ichidagi `url('...')`
- **About, menyu kartalari, galereya:** har bir `<img src="...">`
- **Sharhlardagi avatarlar:** kichik portret URLlari

Yangi rasm: mos `<img>` ning `src` va `alt` atributlarini yangilang (`alt` — SEO va accessibility uchun).

---

## Yangi menyu bandini qo‘shish

1. Kerakli turkumni toping: **Sovuq starterlar**, **Issiq taomlar**, **Desertlar**, **Ichimliklar**.
2. Mavjud kartani **to‘liq nusxa** qiling — `<article class="menu-card group reveal ...">...</article>` blokini.
3. Ichida almashtiring:
   - `src` — taom surati
   - `alt` — qisqa tavsif
   - Narx — `<span class="absolute bottom-3 left-3 ...">` ichida
   - `<h4>` — taom nomi
   - `<p>` — tavsif

Yangi turkum qo‘shish: yangi `<h3>` + `<div class="grid ...">` blokini oldingi turkum kabi yozing.

---

## Dark / Light rejim

- **Qanday ishlaydi:** `html` elementiga `dark` klassi qo‘shiladi/olib tashlanadi; Tailwind `dark:` prefiksi bilan qorong‘i stillar qo‘llanadi.
- **Saqlash:** `localStorage` kaliti — `ziyofat-theme`, qiymat `dark` yoki `light`.
- **Birinchi kirish:** agar saqlangan qiymat bo‘lmasa, tizim **prefers-color-scheme** ga qarab dark yoqishi mumkin.

### Faqat yorug‘ rejim (dark o‘chirish)

**Variant A — kod:** `<script>` ichidagi tema qismida har doim:

```javascript
html.classList.remove("dark");
localStorage.setItem(themeKey, "light");
```

va `themeToggle` tugmasini HTML dan olib tashlang.

**Variant B — mijoz uchun:** brauzerda bir marta yorug‘ rejimni tanlash yetarli; keyingi safar `localStorage` eslab qoladi.

### Dark rejimni majburiy qilish

Sahifa yuklanganda:

```javascript
html.classList.add("dark");
localStorage.setItem(themeKey, "dark");
```

---

## Hisoblagichlar (stats strip)

`<span class="counter" data-target="18">` — `data-target` raqamini o‘zgartiring. Kasr uchun masalan `data-target="4.9"` (yulduzcha bahosi).

---

## Google Maps

`<!-- EDIT: Google Maps -->` yaqinidagi `<iframe src="...">`. O‘z manzilingiz:

1. [Google Maps](https://maps.google.com) da joyni toping → **Share** → **Embed a map** → HTML ni nusxalang → faqat `src="..."` ichidagi URL ni iframe ga qo‘ying.

---

## Bron formasi — Telegram Bot

1. **HTML forma** (`<form id="reserveForm">`) — ism, telefon, sana, mehmonlar soni, izoh.

2. **Konfiguratsiya:** skriptda placeholderlar — `__BOT_TOKEN__` va `__CHAT_ID__` matnlari o‘rniga haqiqiy token va chat ID qo‘yiladi (`let BOT_TOKEN = "..."`). Batafsil — `index.html` **oxiridagi HTML komment**.

3. **Ixtiyoriy xavfsiz usul:** asosiy faylga tegmagan holda, undan **oldin** yuklanadigan skriptda:
   `window.__ZIYOFAT_TELEGRAM__ = { botToken: "...", chatId: "..." };`
   (shu faylni `.gitignore` ga qo‘shing).

4. **Frontend validatsiya:** telefon — O‘zbekiston `+998` va 9 raqam; sana — bugun yoki kelajak; mehmonlar — 1–20.

5. Yuborish **Telegram Bot API** (`/sendMessage`). Muvaffaqiyatda yashil blok + forma tozalanadi, **`#reserve` bo‘limiga silliq scroll**.

6. Xatolikda qizil blok avtomatik ko‘rinadi va unga scroll qilinadi.

7. Token ochiq statik saytda har doim xavf — production uchun ideal **server/proksi**.

8. “Internet / ulanish” xatosi — tarmoq, VPN yoki brauzerni tekshirish kerak bo‘lishi mumkin.

---

## Texnik eslatmalar

| Komponent | Texnologiya |
|-----------|----------------|
| Stillar | Tailwind CDN + `tailwind.config` |
| Ikonlar | Font Awesome 6 (CDN) |
| Shriftlar | Playfair Display + Outfit (Google Fonts) |
| Scroll animatsiya | CSS `.reveal` + `IntersectionObserver` |
| Parallax | Hero fon `translateY` scroll bilan |
| Galereya | Oddiy lightbox (modal + Escape) |
| Sharhlar | CSS `transform` carousel + avtomatik aylanish (~7 s) |
| Kursor | Katta ekranda (`lg`) glow nuqta + hover da `utensils` |

---

## Papka tuzilishi (tavsiya)

Loyiha kengayganda:

```
project/
├── index.html          # Hozirgi bitta fayl — ishlab chiqarish uchun yetarli
├── assets/
│   ├── logo.svg
│   ├── favicon.ico
│   └── images/         # Mahalliy rasmlar (ixtiyoriy)
└── README.md           # Ushbu qo‘llanma
```

CDN rasmlar tez ishlaydi; production uchun rasmlarni siqib (`webp`), `assets/images/` ga qo‘yish va URL larni yangilash yaxshi amaliyot.

---

## Muammo bartarafi

- **Dark rejim “tutilib” qolsa:** brauzerda sayt ma’lumotlarini tozalang yoki `localStorage.removeItem('ziyofat-theme')`.
- **Kursor yo‘qolsa:** kichik ekranda (`<1024px`) mo‘ljallangan — planshet/telefon uchun standart kursor ishlatiladi.
- **Tailwind klasslari ishlamasa:** internet va CDN ga ulanishni tekshiring.

---

© Qo‘llanma `index.html` bilan birga yangilanishi mumkin — versiya: 2026.
