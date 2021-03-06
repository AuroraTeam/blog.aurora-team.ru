---
title: "Закрытие проекта MC Mirrors и краткие итоги"
date: 2021-10-10T21:12:01+03:00
tags: ["Minecraft", "Зеркала"]
cover:
  image: "closed.png"
  caption: 'Вот и подошёл к концу мой небольшой "эксперимент". В принципе результат ожидаем :)'
  relative: true
summary: "Ожидания и реальность, краткие итоги и дальнейшая судьба проекта"
---

# TL;DR

> За 3 месяца работы, проектом интересовалось около 4-5 человек. Из них было три "клиента", из которых один действительно развивал своё зеркало.

# Ожидания == Реальность

Как я и ожидал проект мало кого заинтересует, ибо мало кто хочет ковыряться в файлах игры. В основном все любят потреблять уже готовое.

Конечно, я думал, что от части проблема состоит в том, что у людей есть сложности с поднятием своего зеркала, поиска площадки для хранения всего своего добра (помню кто-то свои сборки даже на GitLab грузил). Но на самом деле ситуация такова, что сборками просто занимаются единицы. И для них, в принципе, нет проблем поднять своё зеркало (если бы они конечно же хотели это делать).

Хотя более вероятная причина в том, что не все знают и понимают как собирать клиенты, либо им просто лень))

По большей части я ожидал подобных результатов, особенно учитывая что я практически никак не рекламировал проект (только на старте и то по парочке гилдов в Discord) и зная какого вообще заниматься сборками, с учётом всей возни с имеющимися на данных момент лаунчерами.

На самом деле я мог накинуть немного рекламы и попытаться как-то развивать идею, но честно не вижу в этом смысла))  
Да, и в принципе, я посчитал что я себе только добавляю лишнего гемора.  
_(К слову, на случай если проект выстрелит, я собирался написать панель управления, но как видите - не получилось, не фартануло XD)_

## А что тут вообще было? Я всё пропустил.

> ![Прошлый сайт проекта MC Mirrors](mc-mirrors.ru.png "Прошлый сайт проекта MC Mirrors") _Прошлый сайт проекта MC Mirrors_

Можно сказать, что это был статичный хостинг файлов, на котором вы могли разместить свои сборки без возни с настройкой сервера, подключением доменов и прочей мелочи.

> Хотели заняться созданием сборок для Minecraft, но не знали где их публиковать?
> Наш сервис позволит Вам создать собственный файловый сервер с минимальными вложениями и без надобности в изучении различных технологий.
> _--- Говорилось на сайте проекта_

Первые пару месяцев был доступен бесплатный "тариф", на котором вы могли протестировать систему. Позже я это убрал, сделав минимальный вариант в 10 рублей в месяц.

По сути это был обычный сервер на облаке Hetzner с настроенным nginx и sftp доступом. Рассчитывалось, что всё это будет работать на основе блочных хранилищ, потому и цена в итоге получилась очень низкой. В расчёт была включена только плата за хранилище, ну а машинку я уже тянул за свой)

Забавно в итоге то, что до блочных хранилищ дело не дошло, но я всё-таки успел немножечко их поковырять.

# А что дальше то?

Сейчас я думаю вести здесь небольшой бложик на тему майна, работы со сборками и зеркалами и чем-нибудь ещё. Возможно когда-нибудь я снова подниму этот проект, если вдруг появится интерес, ну а пока как-то так)
