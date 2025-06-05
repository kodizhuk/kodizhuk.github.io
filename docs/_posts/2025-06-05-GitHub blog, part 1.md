---
title:  "Блог на GitHub"
last_modified_at: 2025-05-05T16:00:58-04:00
categories: 
  - blog
tags:
  - learning
toc: true
toc_label: "Posts"
---

GitHub Pages — це безкоштовний сервіс від GitHub, який дозволяє тобі публікувати статичні веб-сайти прямо з репозиторію. Статичний  - це сайт, який складається з готових HTML, CSS, JS файлів (без бекенду або бази даних). Такий сайт швидко відкривається і не вимагає окремого сервера.

- можна створити персональний сайт або блог;
    
- зробити документацію для проєкту;
    
- хостити портфоліо, резюме або лендинг;
    
- розміщувати демо-версії сайтів або шаблонів;
    
- використовувати Jekyll (вбудований генератор сайтів) для зручного ведення блогу.
    

## 1\. Створюємо новий github репозиторій для блогу

![b134bd1d29864c87f9aea89b8e682826.png](/assets/resources/b134bd1d29864c87f9aea89b8e682826.png)

вставити імя репозиторію, і обовязково зробити репозиторій "Public", та поставити галочку "Add a README file"

![5fbd9c26624e902475f71da508e8719c.png](/assets/resources/5fbd9c26624e902475f71da508e8719c.png)

Далі ідемо відкриваємо на компютері папку де будемо створювати наш блог, і скачуємо наш репозиторій

```bash
git clone https://github.com/kodizhuk/kodizhuk.github.io.git
```

![b72e7d20e89b6e1b5890d1ac483e66e4.png](/assets/resources/b72e7d20e89b6e1b5890d1ac483e66e4.png)

Я все робитиму через Linux, а точніше WSL (Windows Subsystem for Linux). Так простіше.

## 2\. Jekyll

**Jekyll** — це генератор статичних сайтів, створений спеціально для блогів та персональних сайтів. Він перетворює прості текстові файли (Markdown, HTML, шаблони) у повноцінний вебсайт.

- Ти пишеш контент у Markdown-файлах, наприклад:  
    `_posts/2025-06-04-pryvit.md`
    
- Jekyll читає ці файли та твої шаблони (`_layouts`, `_includes`) і генерує HTML.
    
- Отриманий статичний сайт можна опублікувати де завгодно — найзручніше на GitHub Pages, бо він офіційно підтримує Jekyll.
    

&nbsp;

```bash
.
├── _config.yml         # Налаштування сайту
├── _posts/             # Пости (Markdown-файли з датами)
├── _layouts/           # Шаблони сторінок
├── _includes/          # Вставки в шаблони (наприклад, шапка/футер)
├── index.md            # Головна сторінка

```

Заходимо в нашу папку яку ми скачали з git:

```shell
cd .\kodizhuk.github.io\
```

і створюємо нову папочку docs, і заходимо в неї

```shell
mkdir docs
cd docs
```

Встановлюємо jekyll

```bash
gem install bundler jekyll
```

створюємо Jekyll сайт

```shell
jekyll new --skip-bundle .
```

відкриваємо файл Gemfile і коментуємо рядок і розкоментовуємо github-pages

```shell
#gem "jekyll", "~> 4.4.1"
gem "github-pages", group: :jekyll_plugins

```

відкриваємо файл .gitignore і добавляємо туди

```shell
Gemfile.lock
```

Щоб перевірити сайт локально можна запустити команду нижче та переглянути сайт по адресі http://127.0.0.1:4000.

```shell
bundle exec jekyll serve
```

<img src="/assets/resources/7b2e986c643832116631fb69ab139c5f.png" alt="7b2e986c643832116631fb69ab139c5f.png" width="712" height="235" class="jop-noMdConv">

Вітаємо, сайт працює.

Комітимо та пушимо зміни на гітхаб

```bash
git add .
git commit -m "init jekyll site"
git push
```

## 3. Публікація сайту

Сайт опублікується автоматично із гілки main, але при потребі можна глянути на github як він це робить. Відкриваємо Actions

![284af78b001930394bba10185d878a65.png](/assets/resources/284af78b001930394bba10185d878a65.png)



відкриваємо останній pages-build-deployment

![6cc169ba63b816a7b501cafa1ef3dd77.png](/assets/resources/6cc169ba63b816a7b501cafa1ef3dd77.png)

тут при потребі можна перезапустити деплой вручну

## 4. Як добавити новий пост?

В нас є папка названа \_posts. В неї і будемо закидати нові статті.

Кожна нова стаття повинна мати назву у форматі `YEAR-MONTH-DAY-title.md`. Там вже лежить приклад, копіюємо його, редагуємо. Я його назву 2025-06-04-test.md, і закину туди текст:

```
---
layout: post
title:  "Firts Post"
date:   2025-06-04 11:00:00 +0200
categories: jekyll update
---
Hello World, this is my first post.

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/

```

Далі комітимо наші зміни на гітхаб.

Після деплою можемо переглянути зміни - на головній сторінці появився наш пост.

<img src="/assets/resources/24fe765b6f1ae1e1eaeaec9d6200cbf0.png" alt="24fe765b6f1ae1e1eaeaec9d6200cbf0.png" width="253" height="339" class="jop-noMdConv">  <img src="/assets/resources/76362d6b970bfcaad36aec3b177545ad.png" alt="76362d6b970bfcaad36aec3b177545ad.png" width="245" height="334" class="jop-noMdConv">

&nbsp;

## Корисні посилання

- https://docs.github.com/en/pages/quickstart
- https://thinhdanggroup.github.io/github-blog/#introduction
- https://jekyllrb.com/docs/pages/
- дууже довга стаття https://www.aleksandrhovhannisyan.com/blog/getting-started-with-jekyll-and-github-pages/
- https://pages.github.com/

