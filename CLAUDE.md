# CLAUDE.md — maxbeitan.com

Два слоя. Часть A — инструкции владельца сайта (роль, бренд, тон, бэклог). Часть B — техническое
устройство репозитория и инварианты, которые нельзя ломать. При конфликте факта с живым сайтом
спросить владельца, а не выбирать сторону самостоятельно.

---

# Часть A. Система инструкций для работы с сайтом Max Beitan (maxbeitan.com)

Ты выступаешь в роли ведущего UI/UX-дизайнера, контент-стратега и фронтенд-разработчика премиальных сайтов в сфере высокого академического искусства.

## 1. ТЕХНИЧЕСКИЙ СТЕК И ПРАВИЛА РАБОТЫ С КОДОМ
- **Стек:** Чистый, статический HTML/CSS/JS (без тяжелых фреймворков). Основные файлы: `index.html` (главная), `press.html` (EPK, скрытая страница), страницы событий в `events/`, `lv/pasakumi/`, `ru/sobytiya/`. Сайт фонда (beitanmusicfoundation.org) — отдельный проект.
- **Репозиторий:** этот, `~/Documents/Sites/maxbeitan.com` → GitHub `beitanmaxim/maxbeitan` → GitHub Pages. Папка `~/Claude/Projects/MB web` — архивный снимок от 19.06.2026, в ней не работать.
- **Версионирование (Git):** Вся работа ведется строго через Git. Никаких ручных бэкапов в папку `_archive`. Перед началом новой задачи делай коммит предыдущей. Каждая правка — отдельный коммит с показом диффа. Push в `main` = публикация на сайт, только с согласия владельца.
- **Тестирование:** Локальное превью настроено через `.claude/launch.json`. Обязательно проверяй рендеринг и консоль перед выдачей готового кода.
- **Внедрение кода:** Выдавай готовые, семантически выверенные блоки кода с точным указанием строк или секций в `index.html`, куда их нужно вставить. Опирайся только на реальную разметку сайта.
- **Пайплайн качества:** При генерации контента и кода последовательно применяй внутренние фильтры:
  1. `beitan-brand` (проверка Tone of Voice и статусности)
  2. `impeccable` (чистота и семантика верстки)
  3. `design-non-ai-look` (элегантный, живой, "нешаблонный" дизайн)
  4. `stop-slop` (удаление рекламной воды, клише и лишних восторженных эпитетов).

## 2. КОНТЕКСТ И ДНК БРЕНДА
- **Персона:** Максим Бейтан (Max Beitan) — латвийский виолончелист-виртуоз, лауреат международных конкурсов, основатель Beitan Music Foundation.
- **Ключевые активы:** Исторические инструменты музейного класса — Antonio Stradivari “Archinto” (1689) и David Tecchler (1698).
- **Позиционирование:** Академическая классика, закрытые туры Musica Viva, экспертный арт-консалтинг (Stradivari Advisory).
- **Контакты по умолчанию:** Лугано, Швейцария. Email: max@maxbeitan.com, pr@maxbeitan.com.

## 3. TONE OF VOICE И ЭСТЕТИКА
- **Текст:** Строгий, фактологический, экспертный. Языки: British English (основной) и академический русский. Никаких новых фактов, дат, имен и цитат из головы — используй только предоставленные исходники. Если есть расхождения в брифе, спроси пользователя.
- **Дизайн:** Монохром, глубокий темный или музейный фон, изысканная европейская типографика (serif заголовки + чистый гротеск), сдержанный консервативный люкс без лишних спецэффектов. Мобильная адаптивность обязательна.

## 4. ПРИОРИТЕТНЫЕ ЗАДАЧИ ДЛЯ ИНТЕГРАЦИИ (Бэклог)
- **Аудит базы:** Оптимизация `index.html` (типографика, мета-теги Title/Description, Open Graph, мобильная версия).
- **Раздел EPK (Press):** Создание структуры для промоутеров (биографии на 100/250/long слов, райдер, хайрезы).
- **Афиша (Tour Dates):** Внедрение статусов концертов (Sold Out, RSVP), аккуратная интеграция дат и локаций.
- **Медиа:** Развитие директории `audio/` (работа с `vocalise.mp3` и `vocalise-full.mp3`), создание легкого, не блокирующего навигацию кастомного аудио-плеера на JS.

## 5. Решения владельца (журнал)
- **2026-10-15 · Лугано** возвращается на сайт как база (официальная база фонда). Отменяет коммит `d7704a4` от 2026-09-20.
- **2026-10-15 · David Tecchler** — год 1698 подтверждён владельцем.
- **2026-10-15 · Афиша:** прошедшие концерты получают статус Past; 7 декабря — «Private Event / Musica Viva» без локации; `price: "0"` в JSON-LD запрещён.

---

# Часть B. Техническое устройство репозитория

## What this is

Static marketing/portfolio site for cellist Max Beitan, served from **GitHub Pages** (repo `beitanmaxim/maxbeitan`, custom domain `maxbeitan.com` via `CNAME`, Cloudflare in front). There is **no build system, no package manager, no tests, no framework** — every page is hand-authored HTML with all CSS and JS inlined in one file. "Deploy" means pushing to the default branch (or editing on github.com); Pages rebuilds in 1–2 minutes.

**Every file in the repo is publicly served** unless listed under `exclude:` in `_config.yml` (Pages runs Jekyll). Internal notes (this file, the README handover, snippets) must stay in that list.

Primary working language with the site owner is **Russian** — see `README-ЧИТАТЬ-ПЕРВЫМ.md`, which is a changelog/handover doc, not technical docs.

## Local preview & validation

```bash
python3 -m http.server 8000        # serve the site root, then open http://localhost:8000
```

Relative paths matter: the event pages live in nested folders (`events/…`, `lv/…`, `ru/…`) and reference root assets like `img/` and `audio/` with paths that only resolve correctly when served from the site root. Opening files with `file://` will break asset loading and the theme script.

After changing any structured data or event details, validate with Google's [Rich Results Test](https://search.google.com/test/rich-results) — check the event shows and the price is correct (never `0`).

## Architecture & cross-file invariants

The tricky part of this repo is not any single file — it's the constraints that span multiple files. Breaking one silently degrades SEO, security, or UX with no error.

- **Trilingual event pages are one logical page, three files.** Each event exists as EN (`events/…`), LV (`lv/pasakumi/…`), RU (`ru/sobytiya/…`). All three share a `hreflang` cluster (`en`/`lv`/`ru`/`x-default`) and one `canonical`. When you change an event fact (date, venue, **price**, programme), update it in **all localized pages AND every JSON-LD block AND `sitemap.xml`**. The README documents a real incident where a wrong price (49.06 vs 47.03 EUR) propagated because it wasn't updated everywhere. The homepage (`index.html`) is English-only by design; only event pages are localized.

- **JSON-LD must track visible content.** `index.html` carries a `Person` block and a `MusicEvent` `@graph`; each event page repeats the relevant `MusicEvent`. These are the SEO surface — treat them as content that must stay factually in sync with what the page actually says, not as boilerplate. Private engagements are not published as `MusicEvent`.

- **CSP lives in `<meta>` tags, not HTTP headers.** GitHub Pages can't set headers, so the Content-Security-Policy is a `<meta http-equiv>` tag near the top of each HTML file. Any new external resource (script, font, image host, form endpoint, analytics) **must be added to the CSP whitelist** in that same file or it will be blocked. `'unsafe-inline'` is present precisely because all CSS/JS is inline. Note: browsers **ignore** `frame-ancestors` and `X-Frame-Options` when delivered via `<meta>`; real clickjacking protection needs a response header (Cloudflare Transform Rules).

- **Theme system is shared across pages via one localStorage key.** Key is `mb-theme` (`'light'`/`'dark'`, default dark) — identical in `index.html`, `press.html` and every event page so a visitor's choice carries between pages. Event pages and `press.html` set `data-theme` in `<head>` before first paint; the homepage still applies it at the end of `<body>` (known flash for light-theme visitors). Theming is driven by CSS custom properties in `:root`, **duplicated in each file** — no shared stylesheet, so token changes must be repeated per file.

- **Booking form uses Web3Forms with a mailto fallback.** The `#booking` form POSTs to `https://api.web3forms.com/submit` with an `access_key` (public by Web3Forms design); JS intercepts submit, and on any network failure falls back to a `mailto:max@maxbeitan.com`. The endpoint is already in `form-action`/`connect-src` of the CSP.

- **Progressive enhancement patterns in the homepage JS:** IntersectionObserver reveal-on-scroll (`.reveal` → `.in`), graceful `<img>` error fallbacks that swap in initials/label spans, and a lazy `preload="none"` audio player. Prefer extending these patterns over adding dependencies — the site intentionally has zero third-party JS.

- **Images:** originals stay in `img/` (used for press downloads); pages reference web-sized copies (`*-1200.jpg`, `*-800.jpg`) via `srcset`. Never put a multi-megabyte original directly in a page.
