# Добро пожаловать!

Жёстких правил тут нет, потому что нет особых ограничений у данного проекта - типа горящих сроков, маленьких бюджетов и неугомонных заказчиков. 

Просто уважайте других и критикуйте информацию, а не людей. 

Кодекс поведения [доступен по ссылке](https://www.contributor-covenant.org/ru/version/1/4/code-of-conduct).

## Хочу исправить некорректную информацию

Лучше всего [создать issue](https://github.com/xo-russian-community/xo-russian-community.github.io/issues/new?title=Исправить+%3Ctopic%3E) и описать там желаемый результат. После обсуждения с другими людьми может получиться текст ещё лучше и полезнее. К тому же, там иногда можно получить официальный ответ.

## Хочу добавить что-то совсем новое

Опять же, лучше [создать issue](https://github.com/xo-russian-community/xo-russian-community.github.io/issues/new?title=Добавить+%3Ctopic%3E). Нужно обсудить, куда вставить этот кусок информации и как правильно его вставить. 

## Хочу написать пару абзацев вместо токена TODO

Супер! Пишите сразу!

#### Простой способ

Находите [нужный файлик в репозитории](https://github.com/xo-russian-community/xo-russian-community.github.io/tree/master/_pages), и прям там его редактируете [по шагам, как описано](https://help.github.com/articles/editing-files-in-another-user-s-repository/). 
Результат реально можно сразу посмотреть, нажав на вкладочку "Preview changes".

В конце процесса GitHub предложит закоммитить, выберите опцию "создать fork и pull request в master".

#### Посложнее, но можно хорошо протестировать

Можно создать fork, забрать всё локально, дописать текст, [протестировать](#Тестирование-изменений), а потом сделать PR в master основного репозитория. 

# Техническая проблема с сайтом

Есть несколько уже известных технических проблем с сайтом. 
Проверьте, нет ли [среди них](https://github.com/xo-russian-community/xo-russian-community.github.io/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen++label%3Atechnical) вашей.
Если нет - создавайте новую, стирайте текст шаблона (так как он написан для проблем с контентом), пишите детали.
Если есть - лайкайте, подписывайтесь на ~канал~ комментарии в проблеме (там внизу справа есть кнопочка ":loud_sound: Subscribe"), если считаете нужным - оставляйте комментарий.

## Технические подробности

Сайт сделан с помощью генератора статики [Jekyll](https://jekyllrb.com/) с темой [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/docs/configuration/) и хостится на [GitHub Pages](https://pages.github.com/).

Этот репозиторий содержит исходные файлы для сборки сайта. 
Файлы с контентом, который в конечном итоге увидят пользователи, лежат в каталоге [_pages](https://github.com/xo-russian-community/xo-russian-community.github.io/tree/master/_pages) в формате markdown.

В файле [navigation.yml](https://github.com/xo-russian-community/xo-russian-community.github.io/blob/master/_data/navigation.yml) содержится структура верхнего и бокового меню. 
Боковое меню может содержать только два уровня - это ограничение темы. 
Остальные уровни вложенности содержимого необходимо делать с помощью заголовков #, ##, ### внутри статей.

Чтобы добавить новую страницу с контентом, необходимо:
 * добавить новый файл UTF-8 (без BOM!) в формате markdown c [заголовком](https://jekyllrb.com/docs/frontmatter):
    ```
    ---
    title: Заголовок страницы
    toc: true
    ---
    далее идёт содержимое файла в формате markdown
    ```
 * в файл [navigation.yml](https://github.com/xo-russian-community/xo-russian-community.github.io/blob/master/_data/navigation.yml) добавить ссылку на эту страницу по примеру уже имеющихся.
 
## Тестирование изменений

Можно локально запустить сайт и проверить, как будут работать ваши изменения.

Проще всего - с помощью docker. 
Из корневого каталога репозитория запускаете:
```bash
docker run --name jekyll-xo -d -v "${PWD}:/srv/jekyll/" -p 4000:4000 jekyll/jekyll:stable /bin/bash -c "bundle update; jekyll serve --incremental --force_polling"
```

Он сначала поставит все зависимости, потом сгенерирует статический контент для сайта из исходников и [запустит web-сервер на порту 4000](http://localhost:4000). 
Это займёт около 4 минут времени и 55Мб трафика.

Посмотреть, что там происходит, можно с помощью команды
```bash
docker logs --follow jekyll-xo
```

