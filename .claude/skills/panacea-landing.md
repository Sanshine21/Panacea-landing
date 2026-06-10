# Skill: Создание лендинга в стиле «Панацея»

## Описание
Генерирует production-ready лендинг (одностраничный сайт) на чистом HTML+CSS по проверенной структуре проекта «Панацея». Использует тёмную премиальную тему с золотым акцентом.

## Триггер
Используй, когда пользователь просит:
- «сделай лендинг» / «создай сайт-визитку» / «landing page"
- «новая страница в стиле Панацеи"
- «сайт для друга/проекта/услуги"
- «добавь секцию [X] в стиле текущего сайта"

## Технический стек
- HTML5 семантическая вёрстка
- CSS3 с CSS-переменными (кастомные свойства)
- Google Fonts (Playfair Display + Manrope)
- Font Awesome 6 (иконки)
- Без фреймворков (Bootstrap/Tailwind не использовать)

## Дизайн-система

### Цвета (CSS-переменные)
```css
:root {
  --color-bg: #0B0D10;
  --color-surface: #12151C;
  --color-surface-raised: #181C26;
  --color-border: #2A2F3A;
  --color-border-hover: #3D4452;
  --color-accent: #D4A853;
  --color-accent-light: #E8C989;
  --color-accent-glow: rgba(212,168,83,0.25);
  --color-text: #F0EBE3;
  --color-text-muted: #8A8F99;
  --color-white: #FFFFFF;
  --font-display: 'Playfair Display', serif;
  --font-body: 'Manrope', sans-serif;
}
```

### Шрифты (Google Fonts)
```html
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=Manrope:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

### Обязательные секции (порядок)
1. **`<header>`** — фиксированная шапка с логотипом и навигацией. Смена фона при скролле через класс `.scrolled`.
2. **`.hero`** — главный экран с фоновым изображением, градиентным затемнением, заголовком, подзаголовком и 2 кнопками (основная + обводка).
3. **О проекте / Описание** — текстовый блок + карточки команды. Может содержать **карусель фотографий** (слайдер с точками, кнопками и автопроигрыванием).
4. **Видео** — секция с встроенными YouTube-видео через `<iframe>`.
5. **Услуги / Продукты** — сетка карточек `.service-card` (grid). Карточки кликабельные, ведут к форме.
6. **Форма заявки** — `<form>` с полями name, phone (с маской +7), email, select, textarea. Подключать через formsubmit.co с `_captcha=false` и страницей `_next` (thanks.html).
7. **Бесплатная помощь / Преимущества** — иконки + текст в сетке.
8. **Контакты** — email, телефон, соцсети (Telegram, YouTube и т.д.).
9. **`<footer>`** — копирайт.

### Дополнительные страницы
- **thanks.html** — страница подтверждения после отправки формы.

### Компоненты

#### Кнопки
```css
.btn {
  display: inline-block;
  padding: 16px 36px;
  border-radius: 6px;
  font-weight: 600;
  transition: all 0.35s ease;
  cursor: pointer;
}
.btn-primary { /* градиент золотой */ }
.btn-outline { /* прозрачная с золотой рамкой */ }
```

#### Карточки
```css
.service-card {
  background: var(--color-surface);
  border-radius: 14px;
  padding: 36px 28px;
  border: 1px solid var(--color-border);
  transition: transform 0.35s ease, border-color 0.35s ease, box-shadow 0.35s ease;
  cursor: pointer;
  display: flex;
  flex-direction: column;
}
.service-card:hover {
  transform: translateY(-6px);
  border-color: var(--color-accent);
}
```

#### Формы
```css
form {
  background: var(--color-surface);
  padding: 40px;
  border-radius: 16px;
  border: 1px solid var(--color-border);
}
input, select, textarea {
  background: var(--color-bg);
  border: 1px solid var(--color-border);
  border-radius: 8px;
  padding: 14px 16px;
  color: var(--color-text);
}
input:focus, select:focus, textarea:focus {
  border-color: var(--color-accent);
  box-shadow: 0 0 0 3px var(--color-accent-glow);
}
```

#### Карусель
- Элемент `.carousel` с `.carousel-track`, `.carousel-slide`, кнопками `.carousel-prev` / `.carousel-next` и точками `.carousel-dots`.
- Автопроигрывание с паузой при наведении мыши.
- Поддержка свайпа на мобильных устройствах.

### Анимации
- **Появление при скролле:** `.reveal` с `IntersectionObserver`, добавляет класс `.visible`.
- **Hero-анимация:** `.animate-fade-up` с задержками `.delay-1`, `.delay-2`, `.delay-3`.
- **Плавный скролл:** `html { scroll-behavior: smooth; }`.

### Маска телефона
Поле `<input type="tel">` автоматически форматируется в формат `+7 (XXX) XXX-XX-XX` через JavaScript.

### Адаптив
```css
@media (max-width: 768px) {
  /* Бургер-меню */
  /* Grid → 1 колонка */
  /* Уменьшение отступов */
}
```

## SEO-шаблон (в `<head>`)
```html
<meta name="description" content="[описание проекта]">
<meta name="keywords" content="[ключевые слова через запятую]">
<meta name="robots" content="index, follow">
<link rel="canonical" href="[домен]">
<meta property="og:title" content="[заголовок]">
<meta property="og:description" content="[описание]">
<meta property="og:type" content="website">
<meta property="og:url" content="[домен]">
<meta property="og:image" content="[домен]/favicon.png">
<meta property="og:locale" content="ru_RU">
<meta name="twitter:card" content="summary_large_image">
<!-- Schema.org JSON-LD Organization -->
```

## Файловая структура
```
/
├── index.html
├── thanks.html
├── css/
│   └── style.css
├── js/
│   └── main.js
├── assets/
│   └── images/
│       ├── logo.png (→ favicon.png)
│       └── ...
└── favicon.png
```

## Правила
- Все изображения в `assets/images/`.
- CSS-переменные обязательны — не хардкодить цвета.
- Шрифты только Playfair Display (заголовки) и Manrope (текст).
- Формы отправлять через formsubmit.co с `_captcha=false`.
- Карточки услуг всегда кликабельны и скроллят к `#consultation`.
- Кнопки всегда `<a>` или `<button>` с классом `.btn`.
- Favicon всегда `.png`, скопирован из логотипа проекта.
- Не использовать Bootstrap, Tailwind, jQuery.
- Не генерировать `README.md` или документацию без явной просьбы.
