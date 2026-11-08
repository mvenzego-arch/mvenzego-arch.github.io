# StaticSite

Статический сайт: семантический HTML5, чистый CSS3, vanilla JS. Без npm,
фреймворков и сборщиков. Живой адрес: `https://videoboost.duckdns.org`
(GitHub Pages, репо `mvenzego-arch/mvenzego-arch.github.io`, ветка `main`).

## Быстрый старт (локально)

```
python -m http.server 8000
```

Открой `http://127.0.0.1:8000/` в браузере. Остановка сервера: Ctrl+C.

## Структура

| Путь | Что там |
|---|---|
| `index.html` | главная: hero, 8 возможностей, «старая RX 570», CTA |
| `kak-rabotaet.html` | как работает: 5 шагов + FAQ |
| `skachat.html` | скачивание: сборки, чейнджлог, требования |
| `css/style.css` | все стили + дизайн-токены в `:root` |
| `js/main.js` | поведение (страница работает и без него) |
| `content/` | финальные тексты страниц (исходник копирайтера) |
| `assets/favicon/` | favicon (SVG) |
| `CNAME` | имя кастомного домена для GitHub Pages (`videoboost.duckdns.org`) |
| `tools/` | скрипты проверок (Python 3.10, только stdlib) |

## Проверки

```
python tools/check_html.py
python tools/check_links.py
python tools/check_weights.py
python tools/check_contrast.py
```

Каждый скрипт: отчёт «файл:строка → что не так», выход 0 = чисто, 1 = есть ошибки.

## Публикация

1. Правки делаются в ветке `master`, гейты зелёные, коммит `site: …`.
2. Сборка публикационной ветки `main` (сиротская, независимая история):
   `git checkout --orphan main` → `git rm -r --cached .` → добавить только публичные файлы:
   `index.html kak-rabotaet.html skachat.html robots.txt sitemap.xml CNAME README.md AGENTS.md css js assets tools content`
   → коммит → `git switch -f master`.
3. Пуш: `git push usersite main` (remote `usersite` → `github.com/mvenzego-arch/mvenzego-arch.github.io`).
   GitHub Pages отдаёт сайт на `https://videoboost.duckdns.org/`.
4. Старый адрес `https://mvenzego-arch.github.io/videoboost/` (репо `videoboost`, ветка `site`)
   работает до отключения владельцем.
