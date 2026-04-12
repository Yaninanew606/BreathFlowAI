# Деплой BreathFlow как Telegram Mini App

## Шаг 1 — Создать бота

1. Открыть @BotFather в Telegram
2. Написать `/newbot`
3. Дать имя и username (например `breathflow_bot`)
4. Сохранить токен

---

## Шаг 2 — Задеплоить HTML файл

Нужен публичный HTTPS-хостинг. Варианты:

### Вариант A — GitHub Pages (бесплатно, быстро)
```bash
# 1. Создать репозиторий на github.com
# 2. Загрузить breathflow.html как index.html
# 3. Settings → Pages → Deploy from branch → main
# URL: https://USERNAME.github.io/REPO/
```

### Вариант B — Vercel (бесплатно, автодеплой)
```bash
npm i -g vercel
# Положить breathflow.html в папку как index.html
vercel --prod
# Vercel даст URL типа https://breathflow.vercel.app
```

### Вариант C — Netlify Drop
```
Зайти на app.netlify.com/drop
Перетащить папку с index.html
Получить URL типа https://random-name.netlify.app
```

### Вариант D — VPS/сервер
```nginx
# nginx config
server {
    listen 443 ssl;
    server_name breathflow.example.com;
    root /var/www/breathflow;
    index index.html;
}
```

---

## Шаг 3 — Подключить Mini App к боту

В @BotFather:
```
/newapp
→ выбрать своего бота
→ Title: BreathFlow
→ Description: Дыхательные упражнения
→ Photo: загрузить иконку 640x360
→ Web App URL: https://ВАШ-ДОМЕН/
```

Или через `/mybots` → выбрать бота → Bot Settings → Menu Button → настроить URL.

---

## Шаг 4 — Добавить кнопку меню (опционально)

```
/mybots → [ваш бот] → Bot Settings → Menu Button
→ Edit menu button URL → вставить ваш URL
→ Edit menu button text → "Дышать"
```

---

## Шаг 5 — Тест

Открыть бота → нажать кнопку Menu или написать `/start`.

Для локального теста использовать [ngrok](https://ngrok.com):
```bash
npx ngrok http 5500
# Взять https URL и вставить в BotFather
```

---

## Что уже реализовано в файле

| Фича | Статус |
|------|--------|
| `tg.ready()` + `tg.expand()` | ✅ |
| `tg.disableVerticalSwipes()` | ✅ |
| Адаптация к теме Telegram (dark/light) | ✅ |
| `HapticFeedback.impactOccurred()` | ✅ |
| `HapticFeedback.notificationOccurred()` | ✅ |
| `CloudStorage` — сохранение настроек | ✅ |
| `CloudStorage` — история сессий | ✅ |
| `BackButton` — кнопка назад в шапке TG | ✅ |
| Web Audio API — звуковые тоны | ✅ |
| Fallback вибрация через `navigator.vibrate` | ✅ |

---

## Структура файлов для деплоя

```
/
└── index.html   ← это и есть breathflow.html, переименовать
```

Всё в одном файле, никаких зависимостей и npm install не нужно.
