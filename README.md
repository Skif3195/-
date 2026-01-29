# Репозиторий для хранения изображений (image hosting via GitHub)

Этот репозиторий предназначен для удобного хранения и публикации изображений, чтобы можно было вставлять на другие сайты прямые ссылки на файлы (например, в Markdown, HTML, форумы и т.п.).

Ниже — готовые инструкции, примеры ссылок и рекомендации по настройке.

---

## Быстрый старт

1. Создайте публичный репозиторий на GitHub (например, `images`).
   - Через веб-интерфейс: New repository → имя `images` → Public → Create repository.
   - Через GitHub CLI:
   ```bash
   gh auth login
   gh repo create images --public --description "Repo for hosting images to link from other sites" --confirm
   ```

2. Клонируйте репозиторий локально и добавьте файлы:
```bash
git clone https://github.com/Skif3195/images.git
cd images
# Скопируйте сюда ваши картинки (например в папки avatars/, banners/, thumbs/)
git add .
git commit -m "Add images"
git push origin main
```

> Примечание: здесь и далее предполагается, что ваш аккаунт — `Skif3195`, репозиторий — `images`, ветка — `main`. Замените при необходимости.

---

## Рекомендуемая структура папок
Организуйте файлы для удобства:
```
avatars/
banners/
thumbnails/
screens/
README.md
.gitattributes  # если используете Git LFS
```

Имена файлов — без пробелов, в нижнем регистре, через дефис или underscore:
`user-123-avatar.png`, `landing-banner-2026.jpg`

---

## Если у вас большие файлы (>100 MB) или много больших изображений

GitHub не позволяет файлы >100 MB в обычный git. Рекомендуется Git LFS:

Установка и использование:
```bash
# установить git-lfs (один раз)
git lfs install

# отслеживать форматы
git lfs track "*.png"
git lfs track "*.jpg"
git lfs track "*.webp"

# добавьте .gitattributes (git lfs track добавит его автоматически)
git add .gitattributes
git add path/to/large-image.png
git commit -m "Add images with LFS"
git push origin main
```

Пример содержимого `.gitattributes`:
```gitattributes
*.png filter=lfs diff=lfs merge=lfs -text
*.jpg filter=lfs diff=lfs merge=lfs -text
*.webp filter=lfs diff=lfs merge=lfs -text
```

---

## Прямые ссылки на изображения — варианты

1. raw.githubusercontent.com (прямая ссылка на файл)
```
https://raw.githubusercontent.com/<username>/<repo>/<branch>/<path-to-file>
```
Пример:
```
https://raw.githubusercontent.com/Skif3195/images/main/avatars/user-123-avatar.png
```

2. jsDelivr (CDN, кэшируемая, предпочтительна для публичного использования)
```
https://cdn.jsdelivr.net/gh/<username>/<repo>@<branch>/<path-to-file>
```
Пример:
```
https://cdn.jsdelivr.net/gh/Skif3195/images@main/avatars/user-123-avatar.png
```
- Можно использовать `@main` или `@latest`. CDN более производителен и лучше кэширует, чем raw.

3. GitHub Pages
- Включите Pages в Settings → Pages → выберите ветку (например `main`, root или /docs).
- После публикации изображение доступно по:
```
https://<username>.github.io/<repo>/<path-to-file>
```
Пример:
```
https://Skif3195.github.io/images/avatars/user-123-avatar.png
```
GitHub Pages даёт фиксированный домен и удобен для публичных сайтов.

---

## Примеры встраивания

Markdown:
```markdown
![Аватар](https://cdn.jsdelivr.net/gh/Skif3195/images@main/avatars/user-123-avatar.png)
```

HTML:
```html
<img src="https://cdn.jsdelivr.net/gh/Skif3195/images@main/avatars/user-123-avatar.png" alt="Аватар" width="200">
```

Прямая ссылка (raw):
```
https://raw.githubusercontent.com/Skif3195/images/main/banners/landing-banner.jpg
```

---

## Ограничения и рекомендации

- ��епозиторий должен быть публичным, чтобы ссылки работали без авторизации.
- Максимальный размер отдельного файла в обычном git — 100 MB.
- Для публичного встраивания лучше использовать jsDelivr (CDN) вместо raw.githubusercontent.com.
- Не храните в репозитории приватные или чувствительные изображения.
- Чтобы лучше кэшировать и уменьшить трафик, используйте оптимизацию изображений (WebP, сжатие).
- Укажите лицензию (LICENSE) если хотите разрешить/запретить повторное использование изображений (напр., CC0, CC BY, или собственная).

---

## Полезные команды / чек-лист

- Создать репозиторий (CLI):
```bash
gh repo create images --public --description "Repo for hosting images to link from other sites" --confirm
```

- Клонировать и загрузить:
```bash
git clone https://github.com/Skif3195/images.git
cd images
# добавить файлы
git add .
git commit -m "Add images"
git push origin main
```

- Установить и включить LFS (если нужно):
```bash
git lfs install
git lfs track "*.png"
git lfs track "*.jpg"
git add .gitattributes
git add large-image.png
git commit -m "Add large images with LFS"
git push origin main
```

---

Если хотите, могу:
- Сгенерировать готовый `.gitattributes` и поместить его в отдельный файл (вставлю содержимое здесь — скопируете и создадите файл).
- Подготовить пример структуры с несколькими демонстрационными картинками (шаблонный коммит), чтобы вы могли быстро протестировать ссылки.
- Подготовить инструкции по автоматической оптимизации изображений перед пушем (GitHub Actions).

Какая опция вам нужна дальше?
