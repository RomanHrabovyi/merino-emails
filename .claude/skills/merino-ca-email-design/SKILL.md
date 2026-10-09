---
name: "merino-ca-email-design"
description: Email design system для Merino.tech CA (merinotech.ca). Використовуй щоразу, коли треба зверстати email-шаблон для Merino CA — кампанію, флоу (welcome, abandoned cart, browse abandonment, post-purchase, win-back) або транзакційний лист. Тригериться на запити "зверстай лист", "email для Merino CA", "welcome
---

# Merino CA — Email Design System

Коли верстаєш будь-який лист для Merino.tech CA — бери токени й компоненти звідси. Не вигадуй кольори, відступи й кнопки заново. Склей лист із готових блоків нижче.

## Правила доставки (обовʼязково)
- Віддавати **готовий HTML-файл у чаті**. Нічого не створювати в Klaviyo напряму — Roma сам вставляє код.
- Email-safe: табличний лейаут (`<table role="presentation">`), **інлайн-стилі**, mobile-first, рендер в Outlook/Gmail/Apple Mail. Не веб-дизайн-система, не flex/grid.
- Klaviyo-теги лишати як є: `{{ first_name|default:'there' }}`, `{{ coupon_code|default:'...' }}`, `{% unsubscribe %}`, `{{ organization.name }}`, `{{ organization.full_address }}`.
- Зображення — плейсхолдери з alt-текстом, чітко позначені `<!-- ЗАМІНИТИ: ... -->`. Roma вантажить реальні в Klaviyo.
- Брендові кольори — завжди, в потрібних блоках (hero, CTA, акценти, фони секцій, дивайдери, бейджі/зірки). Не нейтральні дефолти.
- Один лист — одна мета — один головний CTA.
- **БЕЗ хедера і футера.** Roma додає свій логотип-хедер і футер (unsubscribe/адреса) сам у Klaviyo. Верстай **лише тіло листа** — від hero до останнього контентного блоку/CTA. Не додавай логотип зверху і футер знизу, якщо Roma прямо не попросив. Каркас документа лишай (DOCTYPE, head, контейнер) — усередину тільки контентні секції.

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
font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
H1 (hero):   28–32px / bold / line-height 1.2 / color #1A1917
H2 (секція): 20–22px / bold / line-height 1.3 / color #1A1917
Body:        16px / normal / line-height 1.6 / color #5C5C5C
Small/cap:   13px / color #9A948A
Контейнер:   600px, канва ззовні #EFEAE0
```

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
    .container{width:100%!important}
    .px{padding-left:20px!important;padding-right:20px!important}
    .py{padding-top:24px!important;padding-bottom:24px!important}
    .stack{display:block!important;width:100%!important}
    .h1{font-size:26px!important}
  }
  a{color:#C16452;text-decoration:underline}
</style>
</head>
<body style="margin:0;padding:0;background:#EFEAE0;">
<!-- PREHEADER -->
<div style="display:none;max-height:0;overflow:hidden;opacity:0;">PREHEADER 40–90 символів, доповнює сабджект.</div>
<table role="presentation" width="100%" cellpadding="0" cellspacing="0" style="background:#EFEAE0;">
  <tr><td align="center" style="padding:24px 12px;">
    <table role="presentation" class="container" width="600" cellpadding="0" cellspacing="0" style="width:600px;max-width:600px;background:#FFFFFF;">
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
  <img src="https://placehold.co/552x320/EFEAE0/9A948A?text=HERO" width="552" alt="опис" style="display:block;width:100%;max-width:552px;border:0;border-radius:8px;margin-bottom:24px;">
  <h1 class="h1" style="margin:0 0 12px;font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;font-size:30px;line-height:1.2;color:#1A1917;font-weight:700;">Hero-заголовок</h1>
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

## Чекліст перед віддачею
- [ ] 600px контейнер, канва #EFEAE0 ззовні
- [ ] Всі стилі інлайн; media-query лише для моб-правок
- [ ] Один головний CTA (повторити у довгому листі)
- [ ] Preheader заповнений, не дублює сабджект
- [ ] Всі зображення мають alt і позначку `ЗАМІНИТИ`
- [ ] Klaviyo-теги на місці (`{% unsubscribe %}` — лише якщо футер запитаний явно)
- [ ] Хедер і футер відсутні (за замовчуванням), якщо Roma не попросив їх окремо
- [ ] Брендові кольори застосовані (rust CTA / bone фони / терракота лінки)
- [ ] Перевір рендер подумки в Outlook (VML-кнопка) і Gmail (без зовнішнього CSS)

## Формат відповіді до листа
Разом з HTML давати: **3 сабджекти** (цікавість / вигода / прямий), **preheader**, короткі нотатки (сегмент, час відправки, A/B-ідея).
