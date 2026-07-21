# Rebuilding Creativity

Статический сайт: HTML + CSS + JS, без сборки и зависимостей.

## Структура

```
index.html         — лента выпусков (главная)
interview.html      — страница одного интервью (?slug=...)
about.html           — «О проекте»
css/style.css        — все стили и цвета/шрифты (design tokens вверху файла)
js/data.js            — ВЕСЬ контент: выпуски, теги, категории, манифест
js/main.js             — рендер (трогать не обязательно)
assets/images/          — картинки (обложки, лого)
assets/fonts/             — сюда положить файлы шрифта Buira, если есть
```

## Как добавить новое интервью

Открой `js/data.js`, скопируй один объект внутри массива `INTERVIEWS`,
поменяй `slug`, `title`, `excerpt`, `tags`, `category`, `content`.
Больше ничего менять не нужно — карточка появится в ленте и в меню сама.

## Как запустить локально

Любой способ поднять статичный сервер подойдёт, например:

```bash
cd rebuilding-creativity
python3 -m http.server 8000
```

и открыть http://localhost:8000

## Деплой на GitHub Pages

1. Создай репозиторий на GitHub (например `rebuilding-creativity`).
2. Залей туда содержимое этой папки (можно перетащить файлы в вебе,
   либо через git):
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/<твой-юзернейм>/rebuilding-creativity.git
   git push -u origin main
   ```
3. В репозитории: **Settings → Pages → Source** → выбери ветку `main`
   и папку `/root`, нажми Save.
4. Через пару минут сайт будет доступен на
   `https://<твой-юзернейм>.github.io/rebuilding-creativity/`

## Подключение своего домена

1. В файл `CNAME` (в корне репозитория, уже создан) впиши свой домен,
   например `rebuildingcreativity.com` — без `https://` и без `www`.
2. У регистратора домена добавь DNS-записи:
   - Если домен корневой (`rebuildingcreativity.com`):
     4 записи типа **A** на IP GitHub Pages:
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - Если используешь поддомен (`www.rebuildingcreativity.com`):
     запись **CNAME** → `<твой-юзернейм>.github.io`
3. В GitHub: **Settings → Pages** → впиши домен в поле Custom domain,
   подожди проверки DNS, включи **Enforce HTTPS**.

DNS обновляется от нескольких минут до 24 часов.

## Что доделать

- [ ] Заменить шрифт-заглушку Fraunces на настоящий Buira
      (положить файлы в `assets/fonts/`, раскомментировать
      `@font-face` в начале `css/style.css`)
- [ ] Добавить реальные изображения обложек в `assets/images/`
      (сейчас показывается заглушка-паттерн, если файла нет)
- [ ] Добавить лого в `assets/images/logo.png`
- [ ] Досверстать под десктоп-макет (сейчас адаптив — экстраполяция
      мобильной версии; готовые Figma-фреймы для ПК ещё не присылались)
