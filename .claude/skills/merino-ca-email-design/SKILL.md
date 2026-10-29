---
name: "merino-ca-email-design"
description: Email design system для Merino.tech CA (merinotech.ca). Використовуй щоразу, коли треба зверстати email-шаблон для Merino CA — кампанію, флоу (welcome, abandoned cart, browse abandonment, post-purchase, win-back) або транзакційний лист. Тригериться на запити "зверстай лист", "email для Merino CA", "welcome
---

# Merino CA — Email Design System

Коли верстаєш будь-який лист для Merino.tech CA — бери токени й компоненти звідси. Не вигадуй кольори, відступи й кнопки заново. Склей лист із готових блоків нижче.

## Ринок і мова (обовʼязково)
- Merino CA — ринок **Канади** (merinotech.ca). Увесь копірайт у листах (заголовки, body, CTA, плейсхолдери, alt-текст, умови) — **англійською**, у стилі **Canadian English** (fibre, colour, odour, favourite, neighbourhood). Не українською і не US-spelling.
- Якщо Roma дав готові рядки (сабджект, preheader, код) — лишай їх **дослівно**, навіть якщо спелінг US.
- Писати Roma можна українською (пояснення, нотатки, сабджект-ідеї), але **вміст листа — завжди англійською**, якщо Roma прямо не попросив іншу мову.

## Аудиторія: і чоловіче, і жіноче (обовʼязково)
- За замовчуванням кожен лист показує **і чоловічі, і жіночі** товари — Merino CA продає на обидві статі. Не роби лист односторонньо «чоловічим» чи «жіночим» без прямого прохання.
- У продуктових блоках давай **обидві статі**: або парні CTA «Shop women's / Shop men's» на відповідні колекції, або окремі секції «For her» / «For him» (як у кампаніях). Аксесуари (шкарпетки, шапки) — unisex, спільний CTA.
- Відповідні колекції: жіночі — `women-sets`, `women-long-sleeves`, `womens-hoodies`, `all-women`; чоловічі — `men-merino-wool-base-layer-sets`, `men-long-sleeves`, `mens-hoodies`, `all-men`; unisex — `merino-wool-socks`, `beanies`, `accessories`.
- Виняток: Roma прямо просить односторонній лист (напр. сегмент тільки «him» / тільки «her») або транзакційний лист під конкретне замовлення.

## Правила доставки (обовʼязково)
- Віддавати **готовий HTML-файл у чаті**. Нічого не створювати в Klaviyo напряму — Roma сам вставляє код.
- **Завжди давати лінк на скачування коду** (прикріплений файл у відповіді) — щоразу, не лише за запитом.
- **Темплейт листа завжди пушити в git** (гілка задачі, у `templates/`) — коміт + push, і давати лінк на файл у репозиторії.
- **Неймінг файлів — щоб було видно порядок.** Флоу: `<flow>-NN-<назва>.html` з двозначним кроком (`welcome-01-intro.html`, `welcome-02-brand-story.html`, `welcome-03-bestsellers.html`). Разові кампанії: `campaign-<назва>.html` (`campaign-black-friday.html`). Транзакційні: `transactional-<назва>.html`. Номер — двозначний, щоб сортувалось правильно.
- **Усі зображення мають бути клікабельними** — обгортай `<img>` у `<a href="...">` (не лише кнопки). Картинка веде на ту саму сторінку/колекцію, що й сусідня кнопка/блок.
- **Лінки бери з Shopify (merinotech.ca)** через MCP (`search_collections` / `search_products`) — реальні handle колекцій/продуктів, щоб кожне зображення й кнопка вели на відповідну сторінку. Не вигадуй handle напам'ять. Evergreen-колекції: `all-men`, `all-women`, `men-merino-wool-base-layer-sets`, `men-bottoms`, `accessories`, `beanies`, `clearance`, `/collections/all`. Сезонні/промо-колекції для флоу не використовуй.
- **Код знижки має бути робочим.** Якщо лист статичний і код жорстко вшитий — створити реальний код у Shopify (`create-discount`) або погодити з Roma. Для welcome/флоу зазвичай динамічний `{{ coupon_code|default:'...' }}` від Klaviyo — лишати як є (Klaviyo генерує робочий код), default — лише запасний.
- **Якщо в листі є код знижки — застосовуй його ДО ВСІХ лінків.** Щоб клієнт переходив по будь-якому посиланню/зображенню/кнопці й код спрацьовував автоматично, обгортай КОЖЕН storefront-лінк у Shopify discount-лінк: `https://merinotech.ca/discount/{{ coupon_code|default:'...' }}?redirect=/collections/<handle>` (і в `<a href>`, і у VML-`href`). Код-чип у блоці-акценті лишай додатково (щоб можна було й скопіювати). Якщо знижка **автоматична, без коду** (напр. Black Friday) — лінки лишаються звичайні, без discount-обгортки.
- **Знижка/оффер — завжди окремим блоком-акцентом, не рядком у тексті.** Якщо в листі є знижка чи промокод — виділяй її в самостійну секцію, що привертає увагу: темний фон (`#232323`), eyebrow (uppercase, `#E8965A`), велике число (`20% OFF`, ~34px, біле), а якщо є код — пунктирний чип (`border:2px dashed #E8965A`) з `{{ coupon_code|default:'...' }}`, і rust-CTA під ним. Не ховай оффер у звичайний абзац. (Приклад — компонент 9 нижче.)
- Email-safe: табличний лейаут (`<table role="presentation">`), **інлайн-стилі**, mobile-first, рендер в Outlook/Gmail/Apple Mail. Не веб-дизайн-система, не flex/grid.
- Klaviyo-теги лишати як є: `{{ first_name|default:'there' }}`, `{{ coupon_code|default:'...' }}`, `{% unsubscribe %}`, `{{ organization.name }}`, `{{ organization.full_address }}`.
- Зображення — плейсхолдери з alt-текстом, чітко позначені `<!-- ЗАМІНИТИ: ... -->`. Roma вантажить реальні в Klaviyo.
- **НЕ лишати видимих плейсхолдерів у тексті листа.** Жодних `[Placeholder]`, `[Review placeholder]`, `[Product name]`, `$[00.00]`, `[4.8/5]`, `[region]` тощо у видимому копірайті — Roma може їх проґавити й відправити. Увесь видимий текст пиши **готовим, зв'язним** (реальні семпл-назви товарів, правдоподібні ціни, справжні за стилем відгуки, чисті умови). Нагадування «замінити на реальні дані» став **лише в HTML-коментарях** (`<!-- replace in Klaviyo: ... -->`), які не рендеряться. Точні цифри (рейтинг, к-сть відгуків, ціни) — або семпл без квадратних дужок, або формулювання без точного числа («thousands of reviews»), а точні — в коментарі.
- Брендові кольори — завжди, в потрібних блоках (hero, CTA, акценти, фони секцій, дивайдери, бейджі/зірки). Не нейтральні дефолти.
- Один лист — одна мета — один головний CTA.
- **БЕЗ хедера і футера.** Roma додає свій логотип-хедер і футер (unsubscribe/адреса) сам у Klaviyo. Верстай **лише тіло листа** — від hero до останнього контентного блоку/CTA. Не додавай логотип зверху і футер знизу, якщо Roma прямо не попросив. Каркас документа лишай (DOCTYPE, head, контейнер) — усередину тільки контентні секції.
- **Klaviyo HTML-блок вирізає `<head>` і `<style>`.** Тому лист має коректно виглядати **лише на інлайн-стилях**, без залежності від media-query:
  - Контейнер — «гумовий»: `style="width:100%;max-width:600px"` (не фіксований `width:600px`), атрибут `width="600"` лишати для Outlook.
  - Жодних фіксованих піксельних ширин, що можуть вилізти на моб.: багатоколонкові ряди роби на **відсоткових комірках** (`width:50%`/`33.33%`), зображення — `width:100%;max-width:…`.
  - Парні кнопки (women/men, socks/beanies) — **fluid**: комірка `width:50%`, сам `<a>` з `display:block` (заповнює комірку), VML-ширину лишати лише для Outlook. Так вони стискаються на моб. без overflow, навіть коли media-query вирізано.
  - `<style>`-блок з media-query лишати можна (працює в Apple Mail / Gmail app як покращення), але **верстка не повинна від нього залежати**.
  - ⚠️ **Елементи з Klaviyo-тегом — завжди `word-break:break-word;overflow-wrap:break-word`** (інлайн). Тег `{{ first_name|default:'there' }}`, `{{ coupon_code|default:'...' }}` тощо — це суцільний рядок без пробілів; у прев'ю Klaviyo (і при довгому реальному значенні) він НЕ переноситься й розпирає лист за межі екрана на мобільному. Став перенос на H1/H2 із тегом, на чип коду купона, на будь-який текст із тегом. Перевірено рендером: без цього лист ~388px замість 375px і дає горизонтальний скрол.
- **Без зовнішньої «канви» — блоки на всю ширину.** Не роби бежеву рамку навколо листа: `body` і зовнішню таблицю-обгортку — `background:#FFFFFF`, у зовнішній комірці `padding:0` (не `24px 12px`). Контейнер лишається `width:100%;max-width:600px`. Так у Klaviyo немає сірих/бежевих смуг з боків. Кольорові фони (bone, dark, акценти) застосовуй **всередині секцій** (повноширинні смуги), а не як зовнішню рамку.
- **Заголовки — по центру.** Усі `H1`/`H2` центруй **інлайн**: `text-align:center` прямо в `style` заголовка (не покладайся лише на `align="center"` комірки, бо Klaviyo ріже частину). Стосується всіх секцій і на світлому, і на темному фоні.
- **Останній блок — не чорний.** Фінальну секцію листа (closing / повтор CTA — те, чим лист закінчується) **не роби на темному фоні** (`#232323`/`#000000`). Завершуй на світлому — `#FFFFFF` або bone `#F4F1EA` — з ink/body-текстом (`#1A1917`/`#5C5C5C`). Темні смуги використовуй лише для **проміжних** секцій (offer-акцент, grid-хедер), а не як кінцівку листа. Rust-CTA лишається rust на світлому фоні.

## Якщо дано референс-фото / скрін листа
Коли Roma прикріпив скрін або фото іншого листа як референс:
1. **Розклади референс на блоки** зверху вниз: що за секції, їх порядок, скільки продуктів, де CTA, де соцдоказ, де дивайдери.
2. **Бери зі скріна ЛИШЕ структуру й композицію** — порядок і склад блоків, кількість елементів, ієрархію. Повтори *логіку* макета.
3. **Стиль — завжди з цього скіла**, не з референсу: кольори, шрифти, кнопки, відступи. Чужу палітру/лого/шрифти не копіюй.
4. Якщо на референсі чужий бренд — явно ігноруй його кольори й лого, адаптуй під Merino (rust CTA, bone фони, терракота лінки).
5. Якщо якогось блоку з референсу немає серед компонентів — збери його в тому ж табличному email-safe стилі з наявних токенів.
6. Тексти — плейсхолдери під тему листа (не переписуй дослівно з референсу), Roma замінить.
> Коротко: **структура — зі скріна, стиль — зі скіла.**

## Design tokens

### Кольори
```
/* Текст */
--ink:        #1A1917   /* заголовки, основний текст */
--body:       #5C5C5C   /* body-текст */
--sub:        #6B675F   /* приглушений */
--faint:      #9A948A   /* найсвітліший, caption */

/* CTA */
--btn-dark-bg:    #232323   (hover #000000)   текст #FFFFFF
--btn-brand-bg:   #BF570A   (hover #A64A08)   текст #FFFFFF

/* Акценти */
--rust:       #BF570A   /* основний акцент */
--rust-light: #E8965A
--terra:      #C16452   /* лінки, бейдж "new", зірки */
--sale:       #C20000   /* розпродаж/знижка */
--stars:      #F2D300   /* зірки Judge.me */

/* Фони */
--white:      #FFFFFF
--bone:       #F4F1EA   /* теплий бренд-фон */
--alt:        #F7F7F8   /* світла секція */
--canvas:     #EFEAE0   /* за межами 600px (теплий) */
--dark:       #232323   /* темна секція/футер */  (або #000000)

/* Бордери/дивайдери */
--border:     #E3DED4
--soft:       #EFEAE0
--chip:       #D8D2C4

/* Текст на темному */
--on-dark:        #FFFFFF
--on-dark-muted:  #CFCFCF
```

### Типографіка (email-safe stack)
```
Заголовки (H1/H2): SERIF — font-family: Georgia, 'Times New Roman', Times, serif;
Решта (body, eyebrow, labels, кнопки, числа, ціни): SANS — 'Helvetica Neue', Helvetica, Arial, sans-serif;

H1 (hero):   28–32px / bold / line-height 1.2 / color #1A1917 / SERIF
H2 (секція): 20–22px / bold / line-height 1.3 / color #1A1917 / SERIF
Body:        16px / normal / line-height 1.6 / color #5C5C5C / SANS
Small/cap:   13px / color #9A948A / SANS
Контейнер:   width:100%;max-width:600px (без зовнішньої канви — див. правила доставки)
```
> **Serif лише для H1/H2** (елегантний editorial-контраст). Eyebrow-мітки (uppercase),
> промо-числа (`20% OFF`), CTA, ціни, стат-плитки — лишаються **sans**. Georgia — email-safe,
> рендериться скрізь, фолбек Times.

### Spacing
```
Секція padding: 32px 24px (моб. 24px 20px)
Між блоками:     24px
CTA padding:     14px 32px
```

## Компоненти (копіюй і наповнюй)

### 0. Каркас документа
```html
<!DOCTYPE html>
<html lang="en" xmlns="http://www.w3.org/1999/xhtml" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:o="urn:schemas-microsoft-com:office:office">
<head>
<meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="x-apple-disable-message-reformatting">
<title>{{ organization.name }}</title>
<!--[if mso]><noscript><xml><o:OfficeDocumentSettings><o:PixelsPerInch>96</o:PixelsPerInch></o:OfficeDocumentSettings></xml></noscript><![endif]-->
<style>
  @media only screen and (max-width:600px){
    .container{width:100%!important;max-width:100%!important}
    .px{padding-left:20px!important;padding-right:20px!important}
    .py{padding-top:24px!important;padding-bottom:24px!important}
    .stack{display:block!important;width:100%!important}
    .h1{font-size:26px!important}
    img{max-width:100%!important;height:auto!important}
  }
  a{color:#C16452;text-decoration:underline}
</style>
</head>
<body style="margin:0;padding:0;background:#FFFFFF;">
<!-- PREHEADER -->
<div style="display:none;max-height:0;overflow:hidden;opacity:0;">PREHEADER 40–90 символів, доповнює сабджект.</div>
<!-- БЕЗ зовнішньої канви: outer bg #FFFFFF, padding:0 (жодних бежевих смуг з боків у Klaviyo) -->
<table role="presentation" width="100%" cellpadding="0" cellspacing="0" style="background:#FFFFFF;">
  <tr><td align="center" style="padding:0;">
    <!-- контейнер гумовий: width:100%;max-width:600px (НЕ фіксований 600px) — інакше вилазить за межі колонки Klaviyo на мобільному -->
    <table role="presentation" class="container" width="600" cellpadding="0" cellspacing="0" style="width:100%;max-width:600px;background:#FFFFFF;">
      <!-- СЮДИ БЛОКИ -->
    </table>
  </td></tr>
</table>
</body></html>
```

### 1. Логотип-хедер — ⚠️ ТІЛЬКИ ЗА ПРЯМИМ ЗАПИТОМ (за замовчуванням не додавати, Roma робить сам)
```html
<tr><td align="center" class="px" style="padding:24px 24px 8px;background:#FFFFFF;">
  <!-- ЗАМІНИТИ: логотип Merino.tech CA, ~150px -->
  <img src="https://placehold.co/150x40/FFFFFF/1A1917?text=MERINO.TECH" width="150" alt="Merino.tech" style="display:block;border:0;">
</td></tr>
```

### 2. Hero
```html
<tr><td class="px py" style="padding:40px 24px;background:#F4F1EA;" align="center">
  <!-- ЗАМІНИТИ: hero-зображення продукту 552px wide -->
  <img src="https://placehold.co/552x320/EFEAE0/9A948A?text=HERO" width="552" alt="опис" style="display:block;width:100%;max-width:100%;height:auto;border:0;border-radius:8px;margin-bottom:24px;">
  <!-- word-break обовʼязково, якщо в заголовку є Klaviyo-тег ({{ first_name }}) -->
  <h1 class="h1" style="margin:0 0 12px;font-family:Georgia,'Times New Roman',Times,serif;font-size:30px;line-height:1.2;color:#1A1917;font-weight:700;text-align:center;word-break:break-word;overflow-wrap:break-word;">Hero-заголовок</h1>
  <p style="margin:0 0 24px;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:16px;line-height:1.6;color:#5C5C5C;">Підзаголовок — головна вигода в один-два рядки.</p>
  <!-- CTA-кнопку встав сюди (компонент 4) -->
</td></tr>
```

### 3. Текстова секція
```html
<tr><td class="px py" style="padding:32px 24px;background:#FFFFFF;">
  <h2 style="margin:0 0 12px;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:22px;line-height:1.3;color:#1A1917;font-weight:700;">Підзаголовок</h2>
  <p style="margin:0;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:16px;line-height:1.6;color:#5C5C5C;">Текст. Короткі абзаци, скануваність, одна ідея.</p>
</td></tr>
```

### 4. CTA — bulletproof button (працює в Outlook)
```html
<table role="presentation" cellpadding="0" cellspacing="0" style="margin:0 auto;"><tr><td align="center" bgcolor="#BF570A" style="border-radius:4px;">
  <!--[if mso]><v:roundrect xmlns:v="urn:schemas-microsoft-com:vml" xmlns:w="urn:schemas-microsoft-com:office:word" href="{{ CTA_URL }}" style="height:48px;v-text-anchor:middle;width:240px;" arcsize="8%" strokecolor="#BF570A" fillcolor="#BF570A"><w:anchorlock/><center style="color:#FFFFFF;font-family:Arial,sans-serif;font-size:16px;font-weight:bold;"><![endif]-->
  <a href="{{ CTA_URL }}" style="background:#BF570A;border-radius:4px;color:#FFFFFF;display:inline-block;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:16px;font-weight:700;line-height:48px;text-align:center;text-decoration:none;width:240px;">Текст кнопки →</a>
  <!--[if mso]></center></v:roundrect><![endif]-->
</td></tr></table>
```
> Для темної кнопки замінити `#BF570A` → `#232323`.

### 5. Product card
```html
<tr><td class="px" style="padding:16px 24px;background:#FFFFFF;">
  <table role="presentation" width="100%" cellpadding="0" cellspacing="0" style="border:1px solid #E3DED4;border-radius:8px;">
    <tr><td style="padding:16px;" align="center">
      <!-- ЗАМІНИТИ: фото продукту -->
      <img src="https://placehold.co/260x260/F7F7F8/9A948A?text=PRODUCT" width="260" alt="продукт" style="display:block;width:100%;max-width:260px;border:0;border-radius:6px;margin-bottom:12px;">
      <p style="margin:0 0 4px;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:16px;color:#1A1917;font-weight:700;">Назва продукту</p>
      <p style="margin:0 0 12px;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:15px;color:#5C5C5C;">$00.00 <span style="color:#C20000;">$00.00</span></p>
    </td></tr>
  </table>
</td></tr>
```

### 6. Соцдоказ / зірки (Judge.me)
```html
<tr><td class="px py" style="padding:28px 24px;background:#F4F1EA;" align="center">
  <div style="font-size:18px;color:#F2D300;letter-spacing:2px;margin-bottom:8px;">★★★★★</div>
  <p style="margin:0 0 6px;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:16px;line-height:1.5;color:#1A1917;font-style:italic;">«Короткий відгук клієнта — до точки сумніву.»</p>
  <p style="margin:0;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:13px;color:#9A948A;">— Імʼя K., verified buyer</p>
</td></tr>
```

### 7. Divider
```html
<tr><td style="padding:0 24px;background:#FFFFFF;"><div style="border-top:1px solid #E3DED4;height:1px;line-height:1px;font-size:1px;">&nbsp;</div></td></tr>
```

### 8. Футер — ⚠️ ТІЛЬКИ ЗА ПРЯМИМ ЗАПИТОМ (за замовчуванням не додавати, Roma робить сам)
```html
<tr><td class="px" style="padding:32px 24px;background:#232323;" align="center">
  <p style="margin:0 0 8px;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:13px;color:#CFCFCF;line-height:1.5;">{{ organization.name }}<br>{{ organization.full_address }}</p>
  <p style="margin:0;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:13px;color:#CFCFCF;">
    <a href="{% unsubscribe %}" style="color:#CFCFCF;text-decoration:underline;">Unsubscribe</a>
  </p>
</td></tr>
```

### 9. Offer / discount — окремий блок-акцент (копіюй для будь-якої знижки/коду)
```html
<tr><td class="px py" style="padding:40px 24px;background:#232323;" align="center">
  <p style="margin:0 0 6px;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:13px;letter-spacing:3px;text-transform:uppercase;color:#E8965A;font-weight:700;">Your welcome gift</p>
  <p style="margin:0 0 4px;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:34px;line-height:1.1;color:#FFFFFF;font-weight:700;">20% OFF</p>
  <p style="margin:0 0 18px;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:15px;line-height:1.6;color:#CFCFCF;">your first order. Apply the code at checkout:</p>
  <!-- CODE CHIP (прибрати, якщо знижка без коду / автоматична) -->
  <table role="presentation" cellpadding="0" cellspacing="0" style="margin:0 auto 22px;"><tr><td style="border:2px dashed #E8965A;border-radius:6px;padding:12px 28px;" align="center">
    <span style="font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:22px;letter-spacing:3px;color:#FFFFFF;font-weight:700;word-break:break-word;overflow-wrap:break-word;">{{ coupon_code|default:'WELCOME20' }}</span>
  </td></tr></table>
  <!-- CTA (rust, bulletproof — компонент 4) -->
  <table role="presentation" cellpadding="0" cellspacing="0" style="margin:0 auto;"><tr><td align="center" bgcolor="#BF570A" style="border-radius:4px;">
    <!--[if mso]><v:roundrect xmlns:v="urn:schemas-microsoft-com:vml" xmlns:w="urn:schemas-microsoft-com:office:word" href="{{ CTA_URL }}" style="height:48px;v-text-anchor:middle;width:240px;" arcsize="8%" strokecolor="#BF570A" fillcolor="#BF570A"><w:anchorlock/><center style="color:#FFFFFF;font-family:Arial,sans-serif;font-size:16px;font-weight:bold;">Shop now &rarr;</center><![endif]-->
    <!--[if !mso]><!-- -->
    <a href="{{ CTA_URL }}" style="background:#BF570A;border-radius:4px;color:#FFFFFF;display:inline-block;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:16px;font-weight:700;line-height:48px;text-align:center;text-decoration:none;padding:0 32px;">Shop now &rarr;</a>
    <!--<![endif]-->
  </td></tr></table>
</td></tr>
```

## Чекліст перед віддачею
- [ ] Контейнер гумовий: `width:100%;max-width:600px` (НЕ фіксований `600px`); outer bg `#FFFFFF`, `padding:0` (без зовнішньої канви)
- [ ] ⚠️ Кожен елемент із Klaviyo-тегом (H1 `{{ first_name }}`, чип `{{ coupon_code }}`, будь-який текст із тегом) має `word-break:break-word;overflow-wrap:break-word` — інакше тег розпирає лист за межі на мобільному (перевірено: ~388px замість 375px)
- [ ] Зображення гумові: `width:100%;max-width:…;height:auto` — ніколи голий фіксований px
- [ ] Всі стилі інлайн; верстка не залежить від media-query (Klaviyo ріже `<head>`)
- [ ] Один головний CTA (повторити у довгому листі)
- [ ] Preheader заповнений, не дублює сабджект
- [ ] Всі зображення мають alt і позначку `ЗАМІНИТИ`
- [ ] Klaviyo-теги на місці (`{% unsubscribe %}` — лише якщо футер запитаний явно)
- [ ] Хедер і футер відсутні (за замовчуванням), якщо Roma не попросив їх окремо
- [ ] Брендові кольори застосовані (rust CTA / bone фони / терракота лінки)
- [ ] Перевір рендер подумки в Outlook (VML-кнопка) і Gmail (без зовнішнього CSS)

## Формат відповіді до листа
Разом з HTML давати: **3 сабджекти** (цікавість / вигода / прямий), **preheader**, короткі нотатки (сегмент, час відправки, A/B-ідея).
