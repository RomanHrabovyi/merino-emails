# Merino CA — Email Templates

Репозиторій для верстки email-шаблонів **Merino.tech CA** ([merinotech.ca](https://merinotech.ca)).
Листи верстаються за єдиним дизайн-системним скілом і вставляються в Klaviyo вручну.

## Структура

```
.
├── .claude/
│   └── skills/
│       └── merino-ca-email-design/
│           └── SKILL.md        # Дизайн-система: токени, компоненти, правила доставки
├── templates/                  # Готові HTML-шаблони (кампанії, флоу, транзакційні)
├── references/                 # Референс-скріни листів — беремо лише структуру, не стиль
├── exports/                    # Фінальні версії, готові до вставки в Klaviyo
└── README.md
```

### `.claude/skills/merino-ca-email-design/`
Email-дизайн-система Merino CA. Містить брендові токени (кольори, типографіка, spacing),
email-safe компоненти (hero, CTA, product card, соцдоказ тощо), правила доставки та чекліст.
Claude Code автоматично підхоплює скіл і використовує його щоразу, коли треба зверстати лист.

### `templates/`
Готові HTML email-шаблони. Один файл — один лист. Email-safe: табличний лейаут, інлайн-стилі,
mobile-first, Klaviyo-теги на місці.

**Неймінг** — щоб порядок було видно одразу:
- **Флоу** (послідовність листів): `<flow>-NN-<назва>.html` з двозначним номером кроку, напр.
  `welcome-01-intro.html`, `welcome-02-brand-story.html`, `welcome-03-bestsellers.html`.
- **Кампанії** (разові, поза флоу): `campaign-<назва>.html`, напр. `campaign-black-friday.html`.
- **Транзакційні**: `transactional-<назва>.html`.
- **Великий флоу можна винести в підтеку** `templates/<flow>/`, напр. `templates/post-purchase/`.

Поточні шаблони:

| Файл | Що це |
|---|---|
| `welcome-01-intro.html` | Welcome flow #1 — вітання + промокод 20% |
| `welcome-02-brand-story.html` | Welcome flow #2 — brand story / why merino |
| `welcome-02-shop-by-weight.html` | Welcome flow #2 (alt) — explore by weight / GSM |
| `welcome-03-bestsellers.html` | Welcome flow #3 — social proof + bestsellers |
| `welcome-04-build-your-set.html` | Welcome flow #4 — build your set |
| `welcome-05-objections-faq.html` | Welcome flow #5 — objections / FAQ |
| `welcome-06-last-chance.html` | Welcome flow #6 — last chance (код діє) |
| `returning-01-welcome-back.html` | Returning-customer flow #1 — welcome back + rewards |
| `returning-02-next-layer.html` | Returning-customer flow #2 — your next layer |
| `returning-03-community-accessories.html` | Returning-customer flow #3 — community + accessories |
| `post-purchase/post-purchase-01-welcome-back.html` | Post-purchase flow #1 — welcome back (Day 0) |
| `campaign-black-friday.html` | Кампанія — Black Friday 30% |

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
