# VØX — Модель 3 / Model 3 / Modelo 3 — City

Статический сайт-магазин. Языки: русский, English, español (переключатель в шапке, язык запоминается).
Ничего устанавливать не нужно: откройте `index.html` или выложите папку на любой хостинг.

## Структура

```
vox-store/
├── index.html          страница
├── css/style.css       оформление (скруглённый, плавный стиль)
├── js/
│   ├── config.js       НАСТРОЙКИ: WhatsApp, доставка, скидки, оплата
│   ├── i18n.js         все тексты на ru / en / es и описания товаров
│   ├── products.js     каталог: цены, фото, категории
│   └── app.js          логика: корзина, заказ, язык
└── assets/
    ├── favicon.svg
    └── img/            фото товаров и деталей (jpg)
```

## Что поменять перед запуском

1. **`js/config.js`** → `whatsapp`: ваш номер в формате `34XXXXXXXXX`. Пока там заглушка `34600000000`.
2. **`js/products.js`** → `price`: цены в примере ориентировочные.
3. **`js/config.js`** → доставка (`freeShipping`, `shipping`) и скидка на комплект. Тексты про «2–4 дня» и «возврат 14 дней» лежат в `js/i18n.js` (ключи `strip.*`, `p.a2`). Проверьте, что они совпадают с вашими условиями.
4. **Настоящий логотип.** Сейчас VØX набран шрифтом. Замените на SVG бренда в `index.html` (класс `.logo`, `.wordmark`).
5. **Фото.** Сейчас это кадры из лукбука, увеличенные в 2 раза. Положите свои фото в `assets/img/` под теми же именами, и качество станет заметно выше.

## Оплата

Сайт показывает способы оплаты (Visa, Mastercard, Apple Pay, Google Pay, PayPal, Bizum, банковский перевод), покупатель выбирает способ при оформлении, и выбор попадает в сообщение WhatsApp.

Деньги сайт сам не принимает: нужны ваши аккаунты. Подключается в `js/config.js`, блок `payments`:

| Поле | Что вписать | Что увидит покупатель |
|---|---|---|
| `cardLink` | ссылка Stripe Payment Link (карта, Apple Pay, Google Pay) | кнопка «Оплатить картой» |
| `paypalLink` | ссылка PayPal.me или PayPal Checkout | кнопка «Оплатить через PayPal» |
| `bizum` | номер для Bizum | инструкция с номером |
| `iban`, `accountHolder` | реквизиты | инструкция с реквизитами |

Пустое поле = покупателю придёт сообщение, что ссылку на оплату пришлёте в WhatsApp.

Ограничение: одна ссылка Stripe Payment Link имеет фиксированную сумму. Для автоматической оплаты корзины на любую сумму нужен небольшой серверный код (Stripe Checkout Session). Пока заказ подтверждается в WhatsApp, а ссылку на нужную сумму вы создаёте вручную.

## Публикация

Подойдёт любой статический хостинг: Netlify, Vercel, Cloudflare Pages, GitHub Pages. Перетащите папку `vox-store` целиком. Шрифты подгружаются с Google Fonts, поэтому при открытии файла без интернета будут запасные.

---

## English

Static store, 3 languages (RU / EN / ES). Edit `js/config.js` (WhatsApp number, shipping, payment links), `js/products.js` (prices) and `js/i18n.js` (texts). Payment methods are displayed and chosen at checkout; real card payments need your Stripe/PayPal account (put the links into `payments` in `config.js`). Deploy the folder to any static host.

## Español

Tienda estática en 3 idiomas (RU / EN / ES). Edita `js/config.js` (número de WhatsApp, envío, enlaces de pago), `js/products.js` (precios) y `js/i18n.js` (textos). Los métodos de pago se muestran y se eligen al finalizar el pedido; los pagos reales con tarjeta requieren tu cuenta de Stripe/PayPal (pon los enlaces en `payments` dentro de `config.js`). Sube la carpeta a cualquier hosting estático.
