---
title: "Как создать своё зеркало"
date: 2021-10-17T00:22:00+03:00
tags: ["Minecraft", "Зеркала"]
cover:
  image: "mirror.png"
  caption: "Пример того, как может выглядеть зеркало. На картинке шаблон [Apaxy](https://oupala.github.io/apaxy/) для Apache"
  relative: true
summary: "Инструкция о том, как создать своё зеркало"
showtoc: true
tocopen: true
---

Сегодня я расскажу и покажу вам как создать своё зеркало.

В данной статье я буду рассматривать создание зеркала на основе [своих шаблонов](https://github.com/JoCat/beautiful-listing). Без лишних предисловий сразу к делу.

# Apache

Данный вариант подойдет вам, если вы используете Shared Hosting (ибо в большинстве случаев там используется Apache, либо связка Apache + Nginx) и у вас нет доступа к настройкам сервера, кроме как к файлам `.htaccess`.

Для включения режима листинга файлов, нужно указать в `.htaccess` файле опцию `Indexes`  
Также следует включить некоторые опции модуля `mod_autoindex`, а также указать список игнорируемых файлов/папок и собственно те файлы, которые у нас будут выводиться вместо стандартного вывода.

Для примера мы можем создать в корне сайта папку и назвать её как угодно, например `tpl`. После чего добавить в неё 2 файла `header.html` и `footer.html` и в них переопределить наш шаблон (например, сделать меню сайта, вывести описание после таблицы со списком файлов и др.).

Пример конфига:

```apache
Options +Indexes
IndexOptions Charset=UTF-8 FancyIndexing FoldersFirst HTMLTable IconsAreLinks IgnoreCase SuppressRules VersionSort SuppressHTMLPreamble SuppressDescription SuppressColumnSorting
IndexIgnore .htaccess tpl
HeaderName /tpl/header.html
ReadmeName /tpl/footer.html

AddIcon /tpl/icons/folder.svg ^^DIRECTORY^^
AddIcon /tpl/icons/folder-home.svg ..
AddIcon /tpl/icons/zip.svg .zip
AddIcon /tpl/icons/java.svg .jar
AddIcon /tpl/icons/json.svg .json
AddIcon /tpl/icons/file-text.svg .cfg .txt
DefaultIcon /tpl/icons/file.svg
```

Описание свойств:

- `Options` – определяем, какие особенности сервера являются доступными в данном каталоге (в данном случае мы включаем режима листинга файлов используя директиву `Options +Indexes`)
- `IndexOptions` – определяем список используемых особенностей модуля `mod_autoindex`  
  в данном случае:
  - `Charset=UTF-8` – устанавливаем кодировку `UTF-8` для страниц
  - `FancyIndexing` – включаем режим FancyIndexing
  - `FoldersFirst` – сначала выводим директории, затем файлы
  - `HTMLTable` – выводим список файлов в виде таблицы
  - `IconsAreLinks` – выводим иконки рядом с названием файлов в ссылке
  - `IgnoreCase` – сортируем файлы без учета регистра
  - `SuppressRules` – убираем прочерки `<hr>` перед и после таблицы
  - `VersionSort` – корректно сортируем файлы содержащие указание версии
  - `SuppressHTMLPreamble` – отключаем вывод `<html>, <head>` и прочих не нужных нам тегов
  - `SuppressDescription` – отключаем вывод описания файла
  - `SuppressColumnSorting` – отключаем возможность сортировки файлов
- `IndexIgnore` – определяем список файлов, которые нужно скрыть при перечислении каталога (в данном случае файлы `.htaccess` и папку с нашим шаблоном - `tpl`)
- `HeaderName` – указываем путь до "шапки" шаблона
- `ReadmeName` – указываем путь до "подвала" шаблона
- `AddIcon` – устанавливаем значок, отображаемый для файлов с определённым расширением
- `DefaultIcon` – устанавливаем значок, отображаемый для файлов, у которых расширение не совпадает ни с одним из списка `AddIcon`

Подробнее обо всех настройках можно узнать [здесь](https://httpd.apache.org/docs/2.0/mod/mod_autoindex.html)

# Nginx

Аналогичную возможность имеет и Nginx. Для того чтобы её можно было использовать нужно в настройках сайта включить режим `autoindex`. А также указать `header.html` и `footer.html` в `add_before_body` и `add_after_body` соответственно.

Пример конфига:

```nginx
location / {
	autoindex on; # включаем режим просмотра файлов
	autoindex_localtime on; # выводим время в листинге каталога в локальной временной зоне
	autoindex_exact_size off; # округляем размеры файлов в листинге каталога до килобайт, мегабайт и гигабайт
	sub_filter '<html>' ''; # удаляем с помощью фильтров не нужные нам теги
	sub_filter '<head><title>Index of $uri</title></head>' '';
	sub_filter '<body>' '';
	sub_filter '<h1>Index of $uri</h1><hr>' '';
	sub_filter '<hr></body>' '';
	sub_filter '</html>' '';
	sub_filter_once on; # включаем одноразовое срабатывание фильтров
	add_before_body /.html/header.html; # определяем "шапку" сайта
	add_after_body /.html/footer.html; # определяем "подвал" сайта
}
```

Как видно из конфига выше, если вы хотите переопределить вывод шапки и футера своей вёрсткой, придётся воспользоваться фильтрами. Да костыльно, но зато работает)

# Nginx + модуль fancyindex

Более продвинутый вариант, отличается от предыдущего тем, что вам придётся собирать модуль для nginx. Для CentOS есть уже собранный модуль. Подробнее в [репозитории](https://github.com/aperezdc/ngx-fancyindex) модуля.

Пример конфига:

```nginx
location / {
	fancyindex on; # включаем режим просмотра файлов с использованием модуля fancyindex
	fancyindex_header "/.html/header.html"; # определяем "шапку" сайта
	fancyindex_footer "/.html/footer.html"; # определяем "подвал" сайта
	fancyindex_show_path off; # убираем вывод стандартного заголовка
	fancyindex_localtime on; # выводим время в листинге каталога в локальной временной зоне
	fancyindex_time_format "%d.%m.%Y %H:%M"; # определяем формат вывода времени
}
```

# Полезные сниппеты

Ниже будет приведён небольшой список полезных сниппетов, которые вы можете добавить себе на зеркало.

## Хлебные крошки

Данный сниппет позволит добавить вам на странице вывод хлебных крошек, для более удобного ориентирования по зеркалу. Данный пример сделан под фреймворк Bootstrap, но вы можете спокойно поменять его под себя.

**JS код:**

```js
const breadcrumbs_el = document.querySelector(".breadcrumb");
const breadcrumbs = location.pathname
  .split("/")
  .filter((word) => word.length > 0);

breadcrumbs_el.append(get_breadcrumbs_el("/", "Home", breadcrumbs.length == 0));
if (breadcrumbs.length > 0) {
  let tree = "";
  breadcrumbs.forEach((link, index) => {
    tree += "/" + link;
    breadcrumbs_el.append(
      get_breadcrumbs_el(tree, link, index == breadcrumbs.length - 1)
    );
  });
}

function get_breadcrumbs_el(link, text, last = false) {
  const el = document.createElement("li");
  el.classList.add("breadcrumb-item");
  if (last === true) {
    el.classList.add("active");
    el.innerHTML = text;
    return el;
  }
  const a = document.createElement("a");
  a.href = link;
  a.innerHTML = text;
  el.append(a);
  return el;
}
```

**HTML код:**

```html
<nav aria-label="breadcrumb">
  <ol class="breadcrumb"></ol>
</nav>
```

## Описание на страницах

Данный сниппет позволит добавить вам на зеркало вывод определённого контента для определённых страниц.

**JS код:**

```js
document.querySelectorAll(".js__toggle_content").forEach((el) => {
  if (el.dataset.pathname == location.pathname) el.style.display = "block";
});
```

**HTML код:**

```html
<div class="js__toggle_content" data-pathname="/">
  *Контент выводимый на главной*
</div>
<div class="js__toggle_content" data-pathname="/clients">
  *Контент выводимый на странице /clients*
</div>
```
