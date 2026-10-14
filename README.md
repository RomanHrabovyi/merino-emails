# Merino CA — Email Templates

Репозиторій для верстки email-шаблонів **Merino.tech CA** ([merinotech.ca](https://merinotech.ca)).
Листи верстаються за єдиним дизайн-системним скілом і вставляються в Klaviyo вручну.

## Структура

```
.
├── AGENTS.md                   # Інструкції для AI-агентів (Codex та ін.): копі-персона + дизайн-система
├── .claude/
│   └── skills/
│       └── merino-ca-email-design/
│           └── SKILL.md        # Дизайн-система: токени, компоненти, правила доставки
├── templates/                  # Готові HTML-шаблони, згруповані в підтеки за флоу
│   ├── welcome-flow/           #   welcome + returning (welcome-back) серії
│   ├── post-purchase/          #   post-purchase флоу
│   └── campaigns/              #   разові кампанії (Black Friday тощо)
├── references/                 # Референс-скріни листів — беремо лише структуру, не стиль
├── exports/                    # Фінальні версії, готові до вставки в Klaviyo
└── README.md
```

### `AGENTS.md`
Конфіг-файл інструкцій для AI-агентів, що читають `AGENTS.md` у корені репо (OpenAI **Codex**
та ін.). Дублює два скіли в одному файлі — **копірайт-персону** (голос бренду, структура листа,
сабджекти) і **дизайн-систему** (палітра, email-safe HTML-компоненти, правила доставки). Агент
читає його перед версткою, тож кожен лист виходить у єдиному стилі з наявними в `templates/`.
Для Claude Code це не обов'язкове (він підхоплює скіл з `.claude/skills/` сам) — файл потрібен
насамперед, щоб та сама поведінка працювала в Codex.

### `.claude/skills/merino-ca-email-design/`
Email-дизайн-система Merino CA. Містить брендові токени (кольори, типографіка, spacing),
email-safe компоненти (hero, CTA, product card, соцдоказ тощо), правила доставки та чекліст.
Claude Code автоматично підхоплює скіл і використовує його щоразу, коли треба зверстати лист.

### `templates/`
Готові HTML email-шаблони. Один файл — один лист. Email-safe: табличний лейаут, інлайн-стилі,
mobile-first, Klaviyo-теги на місці.

**Структура — кожен флоу у своїй підтеці:**
- `templates/welcome-flow/` — welcome-серія (нові клієнти) + returning-серія (welcome-back).
- `templates/post-purchase/` — post-purchase флоу.
- `templates/campaigns/` — разові кампанії (Black Friday тощо).

**Неймінг файлів** — щоб порядок було видно одразу:
- **Флоу**: `<flow>-NN-<назва>.html` з двозначним номером кроку, напр. `welcome-01-intro.html`.
- **Кампанії**: `campaign-<назва>.html`, напр. `campaign-black-friday.html`.
- **Транзакційні**: `transactional-<назва>.html`.

Поточні шаблони:

| Файл | Що це |
|---|---|
| `welcome-flow/welcome-01-intro.html` | Welcome #1 — вітання + промокод 20% |
| `welcome-flow/welcome-02-brand-story.html` | Welcome #2 — brand story / why merino |
| `welcome-flow/welcome-02-shop-by-weight.html` | Welcome #2 (alt) — explore by weight / GSM |
| `welcome-flow/welcome-03-bestsellers.html` | Welcome #3 — social proof + bestsellers |
| `welcome-flow/welcome-04-build-your-set.html` | Welcome #4 — build your set |
| `welcome-flow/welcome-05-objections-faq.html` | Welcome #5 — objections / FAQ |
| `welcome-flow/welcome-06-last-chance.html` | Welcome #6 — last chance (код діє) |
| `welcome-flow/returning-01-welcome-back.html` | Returning #1 — welcome back + rewards |
| `welcome-flow/returning-02-next-layer.html` | Returning #2 — your next layer |
| `welcome-flow/returning-03-community-accessories.html` | Returning #3 — community + accessories |
| `post-purchase/post-purchase-01-thank-you-what-happens-next.html` | Post-purchase #1 (first-time buyer) — thank you / what happens next (Day 0) |
| `post-purchase/post-purchase-01-welcome-back.html` | Post-purchase #1 (returning buyer) — welcome back (Day 0) |
| `campaigns/campaign-black-friday.html` | Кампанія — Black Friday 30% |

### `references/`
Референс-скріни або фото інших листів. З них беремо **лише структуру й композицію**
(порядок блоків, кількість елементів, ієрархію) — стиль завжди зі скіла.

### `exports/`
Фінальні/експортовані версії листів, готові до вставки в Klaviyo.

## Робочий процес

1. Описати лист (мета, сегмент, CTA) — опційно прикріпити референс у `references/`.
2. Claude верстає тіло листа за скілом `merino-ca-email-design` → HTML у `templates/`.
3. Разом з HTML: 3 сабджекти, preheader, нотатки (сегмент, час відправки, A/B-ідея).
4. Фінал — у `exports/`, звідки Roma вставляє код у Klaviyo.

> **БЕЗ хедера і футера** за замовчуванням — Roma додає логотип-хедер і футер
> (unsubscribe/адреса) сам у Klaviyo. Верстаємо лише тіло листа.
