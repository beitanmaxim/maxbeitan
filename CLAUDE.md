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
- **Исторические инструменты (опыт выступлений, не владение):** Antonio Stradivari “Archinto” (1689), Antonio Stradivari “Magg” (1698), David Tecchler (1698). Писать только как опыт или в прошедшем времени, никогда «plays / his instruments». Образец: *“Throughout his career, Max Beitan has performed on several historic instruments of museum calibre, including the Stradivari ‘Archinto’, the Stradivari ‘Magg’, and a David Tecchler (1698).”* В фактбоксах заголовок «Instruments performed».
- **Позиционирование:** Академическая классика, закрытые туры Musica Viva, экспертный арт-консалтинг (Stradivari Advisory).
- **Контакты по умолчанию:** Email: max@maxbeitan.com, pr@maxbeitan.com. Город базы не указывается (см. §5).

## 3. TONE OF VOICE И ЭСТЕТИКА
- **Текст:** Строгий, фактологический, экспертный. Языки: British English (основной) и академический русский. Никаких новых фактов, дат, имен и цитат из головы — используй только предоставленные исходники. Если есть расхождения в брифе, спроси пользователя.
- **Дизайн:** Монохром, глубокий темный или музейный фон, изысканная европейская типографика (serif заголовки + чистый гротеск), сдержанный консервативный люкс без лишних спецэффектов. Мобильная адаптивность обязательна.

## 4. ПРИОРИТЕТНЫЕ ЗАДАЧИ ДЛЯ ИНТЕГРАЦИИ (Бэклог)
- **Аудит базы:** Оптимизация `index.html` (типографика, мета-теги Title/Description, Open Graph, мобильная версия).
- **Раздел EPK (Press):** Создание структуры для промоутеров (биографии на 100/250/long слов, райдер, хайрезы).
- **Афиша (Tour Dates):** Внедрение статусов концертов (Sold Out, RSVP), аккуратная интеграция дат и локаций.
- **Медиа:** Развитие директории `audio/` (работа с `vocalise.mp3` и `vocalise-full.mp3`), создание легкого, не блокирующего навигацию кастомного аудио-плеера на JS.

## 5. Решения владельца (журнал)
- **2026-10-15 · Лугано (окончательно):** не указывать Лугано в качестве базы артиста на главной странице и в промо-материалах (title, og, hero, био, футер, schema.org, press.html, страницы событий). Временный возврат в `2b0c9c9` отменён в тот же день. Лугано как площадка (LAC Lugano, Musica Viva, фестивали, консерватория) упоминается как факт, не как база.
- **2026-10-15 · David Tecchler** — год 1698 подтверждён владельцем.
- **2026-10-15 · Инструменты:** формулировки только в статусе опыта (см. §2); добавлен Stradivari “Magg” (1698); вариант “De Munck” отменён владельцем в тот же день.
- **2026-10-15 · Афиша:** прошедшие концерты получают статус Past; `price: "0"` в JSON-LD запрещён. 6 декабря 2026 (один вечер; ранее «5–6 декабря», уточнено владельцем) — 40th Anniversary Gala, Grand Ballroom, Grand Hotel Kempinski Riga, статус Announced, полоса «Next concert» под hero, RSVP через pr@maxbeitan.com (заменяет заглушку «7 декабря · Private Event»). 31 декабря 2026 — New Year’s Eve Celebration, Palazzo Lanza, Palermo (исправлено владельцем; ранее ошибочно Kempinski Riga), статус Announced, RSVP через pr@maxbeitan.com. Цены и организатора в JSON-LD не указывать, пока их не подтвердит владелец.

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

- **CSP lives in `<meta>` tags, not HTTP headers.** GitHub Pages can't set headers, so the Content-Security-Policy is a `<meta http-equiv>` tag near the top of each HTML file. Any new external resource (script, font, image host, form endpoint, analytics) **must be added to the CSP whitelist** in that same file or it will be blocked. `'unsafe-inline'` is present precisely because all CSS/JS is inline. Cloudflare injects its Web Analytics beacon into every page: keep `https://static.cloudflareinsights.com` in `script-src` and `https://cloudflareinsights.com` in `connect-src` on every page, including new ones. Note: browsers **ignore** `frame-ancestors` and `X-Frame-Options` when delivered via `<meta>`; real clickjacking protection needs a response header (Cloudflare Transform Rules).

- **Theme system is shared across pages via one localStorage key.** Key is `mb-theme` (`'light'`/`'dark'`, default dark) — identical in `index.html`, `press.html` and every event page so a visitor's choice carries between pages. Event pages and `press.html` set `data-theme` in `<head>` before first paint; the homepage still applies it at the end of `<body>` (known flash for light-theme visitors). Theming is driven by CSS custom properties in `:root`, **duplicated in each file** — no shared stylesheet, so token changes must be repeated per file.

- **Booking form uses Web3Forms with a mailto fallback.** The `#booking` form POSTs to `https://api.web3forms.com/submit` with an `access_key` (public by Web3Forms design); JS intercepts submit, and on any network failure falls back to a `mailto:max@maxbeitan.com`. The endpoint is already in `form-action`/`connect-src` of the CSP.

- **Progressive enhancement patterns in the homepage JS:** IntersectionObserver reveal-on-scroll (`.reveal` → `.in`), graceful `<img>` error fallbacks that swap in initials/label spans, and a lazy `preload="none"` audio player. Prefer extending these patterns over adding dependencies. The only third-party JS is vendored in `vendor/` (see below); Cloudflare's analytics beacon is injected at the edge, cookieless.

- **Motion layer (homepage only): Lenis + GSAP ScrollTrigger.** Self-hosted, pinned, no CDN: `vendor/gsap.min.js` and `vendor/ScrollTrigger.min.js` (3.15.0, GSAP Standard License), `vendor/lenis.min.js` (1.3.26, MIT); versions, hashes and licences in `vendor/README.txt` and `vendor/LICENSE-*.txt`. `initMotion()` in `index.html` does three things: Lenis smooth scroll (lerp 0.075, touch stays native, anchor links glide 1.8 s ease-out-quart, menu pauses it), a slow reveal of every outermost `.reveal` (children rise 24 px, 1.2 s, `power3.out`, once), and the hero title letter reveal (~1.1 s, masked, `aria-label` on the `<h1>`, letters `aria-hidden`). House rule: slow, eased out, **no bounce, back or elastic easing**.
- **Level 2 (desktop with a mouse only, `gsap.matchMedia`, query `(min-width: 921px) and (hover: hover) and (pointer: fine) and (min-height: 640px)`):** soft hero parallax (the photo layer drifts 48 px while the hero scrolls away; written to the CSS `translate` property on `.photo-img` because `transform` belongs to the `heroDrift` animation and to the mouse parallax, and an animation overrides anything GSAP puts in `transform`), and the **pinned practices** (`.pillars` holds for 120% of the viewport while focus moves Cellist → Foundation → Advisory, then all three at full strength). Anchors `#cellist`, `#foundation`, `#advisory` scroll to the matching step of the pin (see `pinStep` in the click handler). On phones and touch screens there is no pin and no parallax: native scrolling.
- **Practices reactions.** Desktop: each column shows `max(scroll focus, cursor focus)` as opacity 0.35 to 1; hovering or tabbing into a column brings it forward (0.6 s `sine.out`, heading lifts 6 px), leaving releases it (0.9 s). Values are written straight to `style` (no per-frame tweens). Touch screens and narrow windows: no pin; each practice comes forward (1.0, else 0.55) while it crosses the middle of the screen.
- **Smoothness rules.** Photos used in animated frames are served as web-sized copies (`*-900.jpg`, `*-1440.jpg`; originals stay in `img/`) and are decoded in an idle callback after load, so the curtain does not stall on a big JPEG decode. The page grain has no `mix-blend-mode` (a full-screen blend layer re-blends every scroll frame). `html.hero-off` pauses the hero zoom once the hero is off screen. ScrollTrigger runs with `ignoreMobileResize: true` so the mobile address bar does not trigger a re-measure mid-scroll.
- **Photo curtain:** put `data-mask` on a direct child of a `.reveal` container and it reveals with a left-to-right wipe with a soft edge (a gradient mask, edge 22% of the width, class `wiping` while it plays; browsers without `mask-image` get a hard `clip-path` wipe) (1.5 s, `power3.inOut`) while the inner `img` or `.img` settles from scale 1.16 to 1 (2.2 s, `power2.out`). Used on the biography photo, the four Selected plates and the video frame; everything else keeps the fade.
- **ScrollTrigger auto-refresh** is limited to `DOMContentLoaded,load,resize` (no `visibilitychange`): a refresh in the middle of a Lenis glide resets the scroll position.
- **Reduced motion = static.** With `prefers-reduced-motion: reduce` (or if any vendor script fails) `initMotion()` does not run: no Lenis, no GSAP, native scroll, everything visible; the CSS rule in the reduced-motion block also stops the hero drift and the scroll cue. The class `js-motion` on `<html>` marks the active layer. New sections: add `.reveal` to the container and its children animate automatically; do not add CSS transitions on `.reveal > *`.
- **Updating vendor files:** download the new pinned versions, replace them, update `vendor/README.txt`, re-check reduced motion and the mobile menu.

- **Images:** originals stay in `img/` (used for press downloads); pages reference web-sized copies (`*-1200.jpg`, `*-800.jpg`) via `srcset`. Never put a multi-megabyte original directly in a page.
