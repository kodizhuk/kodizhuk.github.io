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

![github-blog-1.png](/assets/resources/github-blog-1.png)

вставити імя репозиторію, і обовязково зробити репозиторій "Public", та поставити галочку "Add a README file"

![github-blog-2.png](/assets/resources/github-blog-2.png)

Далі ідемо відкриваємо на компютері папку де будемо створювати наш блог, і скачуємо наш репозиторій

```bash
git clone https://github.com/kodizhuk/kodizhuk.github.io.git
```

![github-blog-3.png](/assets/resources/github-blog-3.png)

Я все робитиму через Linux, а точніше WSL (Windows Subsystem for Linux). Так простіше.

## 2\. Jekyll

**Jekyll** — це генератор статичних сайтів, створений спеціально для блогів та персональних сайтів. Він перетворює прості текстові файли (Markdown, HTML, шаблони) у повноцінний вебсайт.

- Ти пишеш контент у Markdown-файлах, наприклад:  
    `_posts/2025-06-04-pryvit.md`
    
- Jekyll читає ці файли та твої шаблони (`_layouts`, `_includes`) і генерує HTML.
    
- Отриманий статичний сайт можна опублікувати де завгодно — найзручніше на GitHub Pages, бо він офіційно підтримує Jekyll.
    

&nbsp;

```
.
├── _config.yml         # Налаштування сайту
├── _posts/             # Пости (Markdown-файли з датами)
├── _layouts/           # Шаблони сторінок
├── _includes/          # Вставки в шаблони (наприклад, шапка/футер)
├── index.md            # Головна сторінка

```

Заходимо в нашу папку яку ми скачали з git:

```bash
cd .\kodizhuk.github.io\
```

і створюємо нову папочку docs, і заходимо в неї

```bash
mkdir docs
cd docs
```

Встановлюємо jekyll

```bash
gem install bundler jekyll
```

створюємо Jekyll сайт

```bash
jekyll new --skip-bundle .
```

відкриваємо файл Gemfile і коментуємо рядок і розкоментовуємо github-pages

```bash
#gem "jekyll", "~> 4.4.1"
gem "github-pages", group: :jekyll_plugins

```

відкриваємо файл .gitignore і добавляємо туди

```bash
Gemfile.lock
```

Щоб перевірити сайт локально можна запустити команду нижче та переглянути сайт по адресі http://127.0.0.1:4000.

```bash
bundle exec jekyll serve
```

<img src="/assets/resources/github-blog-4.png" alt="github-blog-4.png" width="712" height="235" class="jop-noMdConv">

Вітаємо, сайт працює.

Комітимо та пушимо зміни на гітхаб

```bash
git add .
git commit -m "init jekyll site"
git push
```

## 3. Публікація сайту

Сайт опублікується автоматично із гілки main, але при потребі можна глянути на github як він це робить. Відкриваємо Actions

![github-blog-5.png](/assets/resources/github-blog-5.png)



відкриваємо останній pages-build-deployment

![github-blog-6.png](/assets/resources/github-blog-6.png)

тут при потребі можна перезапустити деплой вручну

## 4. Як добавити новий пост?

В нас є папка названа \_posts. В неї і будемо закидати нові статті.

Кожна нова стаття повинна мати назву у форматі `YEAR-MONTH-DAY-title.md`. Там вже лежить приклад, копіюємо його, редагуємо. Я його назву 2025-06-04-test.md, і закину туди текст:

```bash
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

<img src="/assets/resources/github-blog-7.png" alt="github-blog-7.png" width="253" height="339" class="jop-noMdConv">  <img src="/assets/resources/github-blog-8.png" alt="github-blog-8.png" width="245" height="334" class="jop-noMdConv">

&nbsp;

## Корисні посилання

- [docs.github.com](https://docs.github.com/en/pages/quickstart)
- [thinhdanggroup.github.io](https://thinhdanggroup.github.io/github-blog/#introduction)
- [jekyllrb.com](https://jekyllrb.com/docs/pages/)
- [aleksandrhovhannisyan.com](https://www.aleksandrhovhannisyan.com/blog/getting-started-with-jekyll-and-github-pages/)
- [pages.github.com](https://pages.github.com/)

