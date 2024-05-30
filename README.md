# Тестовый проект - шпаргалка по работе с Git:

## Задание:
```
1) Создайте репозиторий
2) Добавьте в репозиторий файл README.md и запишите в него всё, что уже знаете. Это могут быть: список команд и понятий по каждой из пройденных тем; инструкции по инициализации проекта, работе с коммитами и регистрации на GitHub или просто поурочные конспекты в свободной форме.
3) Загрузите получившийся репозиторий на GitHub и убедитесь, что локальная и удалённая версии идентичны.
```

## Решение:
1) На Gitlab создал репозиторий с именем test1 (через интерфейсе gitlab)

2) Локально добавил папку test1. Далее чтобы папка стала репозиторием ее нужно инициализировать. Для этого нужно в нее перейти и инициализировать: <br>
__cd test1__ <br>
__git init__ <br>
__git status__ - проверка состояния репозитория <br>
Для справки. Создание файла команда touch (или просто через GUI) <br>

3) Далее добавляем все файлы папки для отслеживания: 
__git add .__ <br>
и коммитим: <br>
__git commit -m "Первый коммит файла"__ <br>
Далее вносим в файл изменения и опять добавляем и коммитим <br>
__git add README.md__ <br>
__git commit -m "Второй коммит файла"__ <br>

4) Чтобы просомотреть историю коммитов: <br>
__git log__ <br>
Получить сокращённый лог можно с помощью команды __git log --oneline__ <br>

5) Далее нужно связать удаленный (см п.1) и локальные репозитории (см. п.2). Для этого нужно выполнить команды, которые приведены в секции *"…or push an existing repository from the command line"* на первой странице репозитория на gitlab (Но нужно перейти в директорию репозитория!).  <br>

Перед связыванием репозиториев необходимо настроить SSH-ключи.Но прежде чем генерировать SSH-ключи, убедитесь, что у вас их ещё нет. По умолчанию директория с SSH-ключами находится в домашней директории пользователя. Перейдите в неё: <br>
```
$ cd ~ # перешли в домашнюю директорию
```

Обычно SSH-ключи находятся в директории .ssh/. Проверить наличие этой директории и файлов в ней можно с помощью следующей команды. <br>
```
$ ls -la .ssh/ # вывели список созданных ключей 
```

Если папка пустая или её нет, всё в порядке. <br>
Если есть файлы с похожими названиями, SSH-ключи уже создавались: id_dsa.pub; id_ecdsa.pub; id_ed25519.pub; id_rsa.pub. <br>
Если вы не создавали эти файлы, удалите их все.

----

### Инструкция по генерации SSH-ключа
1. Для генерации SSH-пары можно использовать программу ssh-keygen. Откройте терминал и введите следующую команду.
```
$ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" 
```
Используйте электронную почту, к которой привязан ваш GitHub-аккаунт.
Если вы видите сообщение об ошибке, то, скорее всего, ваша система не поддерживает алгоритм шифрования ed25519. Ничего страшного: используйте другой алгоритм.
```
$ ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
```
После ввода отобразится такое сообщение.
```
> Generating public/private rsa key pair. # сгенерированы публичный и приватный ключи 
```
2. Укажите место хранения ключей. Простой вариант — сделать домашний каталог пользователя путём по умолчанию. Для этого нажмите Enter.
(для Windows)
```
> Enter a file in which to save the key (C:\Users\<имя_пользователя>\.ssh\):[Press enter] 
```
Теперь в указанной директории появится пара ключей.

3. Программа запросит кодовую фразу (англ. passphrase) для доступа к SSH-ключу. Вы можете оставить поле пустым. Для этого нажмите Enter, а затем ещё раз Enter для подтверждения.
```
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again] 
```
4. Готово! Теперь осталось проверить, что ключи действительно сгенерировались. Для этого вызовите эту команду.
```
ls -a ~/.ssh 
```
На экране должны появиться два файла — один с расширением .pub, другой — без. Файл в .pub — публичный, им можно делиться с веб-сайтами или коллегами. Файл без расширения .pub — приватный. Ни в коем случае не передавайте его никому! <br>
 <br>

----

6) Убедимся, что репозитории связаны: <br>
__git remote -v__
В результате выполнения команды должны вывестить две строки:
```
git remote -v
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push)
```
7) Изменения из локального репозитория в удаленный отправляются командой: <br>
__git push__ <br>

В первый раз эту команду нужно вызвать с флагом -u и параметрами origin (имя удалённого репозитория) и main или master (название текущей ветки). Флаг -u свяжет локальную ветку с одноимённой удалённой. Как вы связывали локальный и удалённый репозитории в предыдущем уроке, так же и здесь нужно дополнительно связать ветки. <br>

```
$ git push -u origin main # Если команда приведёт к ошибке, попробуйте 
                          # заменить main на master. 
```

----

### Информацию из уроков о хеше, логе, HEAD,

#### Файл HEAD

Файл __HEAD__ — один из служебных файлов папки .git. Он указывает на коммит, который сделан последним (то есть на самый новый). <br>

Вместо хеша последнего коммита можно написать слово HEAD — Git вас поймёт.

#### Статусы файлов в Git

Одна из ключевых задач Git — отслеживать изменения файлов в репозитории. Для этого каждый файл помечается каким-либо статусом. Рассмотрим основные. <br>

__untracked (англ. «неотслеживаемый»)__ <br>

Новые файлы в Git-репозитории помечаются как untracked, то есть неотслеживаемые. Git «видит», что такой файл существует, но не следит за изменениями в нём. У untracked-файла нет предыдущих версий, зафиксированных в коммитах или через команду git add. <br>

__staged (англ. «подготовленный»)__ <br>
После выполнения команды git add файл попадает в staging area (от англ. stage — «сцена», «этап [процесса]» и area — «область»), то есть в список файлов, которые войдут в коммит. В этот момент файл находится в состоянии staged. <br>

Команда git add добавляет в staging area только текущее содержимое файла. Если вы, например, сделаете git add file.txt, а затем измените file.txt, то новое содержимое файла не будет находиться в staging. <br>

__tracked (англ. «отслеживаемый»)__ <br>
Состояние tracked — это противоположность untracked. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью git commit, а также файлы, которые были добавлены в staging area командой git add. То есть все файлы, в которых Git так или иначе отслеживает изменения. <br>

__modified (англ. «изменённый»)__ <br)
Состояние modified означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия. Например, файл был закоммичен и после этого изменён. <br>

Git сообщит об этом с помощью статуса modified: файл изменён относительно той версии, которая уже в staging. Чтобы добавить в staging последнюю версию, нужно выполнить git add file.txt ещё раз. <br>

#### Типичный жизненный цикл файла в Git
```mermaid
flowchart TD;
%%A[untracked ] --git add--> B[stage + tracked];
      A[untracked] --git add--> B[stage + tracked];
      С[modified] --git add--> B[stage + tracked];
      B[stage + tracked] --изменения--> С[modified];
      B[stage + tracked] --git commit--> D[tracked];
      D[tracked ] --Изменения--> С[modified];
```

----
### Как исправить коммит

Иногда в только что выполненном коммите нужно что-то поменять: например, добавить ещё пару файлов или заменить сообщение на более информативное. <br>
В таком случае можно внести правки в уже сделанный коммит с помощью опции --amend (от англ. amend — «исправить», «дополнить») у команды commit: __git commit --amend__. <br>
Опция --amend работает только с последним коммитом (HEAD). <br>
<br>
__Как это работает:__
- Если забыли файл к коммиту, то нужно его добавить через __git add <имя файла>__ <br>
- Далее добавить в коммит __git commit --amend --no-edit__ (если не нужно править комментарий) или __git commit --amend -m "Комментарий"__ (если нужно править комментарий) <br>

----
### Как откатиться назад, если «всё сломалось»

На разных этапах работы с Git могут происходить похожие ситуации: <br>
- В список на коммит попал лишний файл (например, временный). Нужно «вынуть» его из списка. <br>
- Последние несколько коммитов ошибочные: например, сделали не то, что было нужно, или нарушили логику. Хочется «откатить» сразу несколько коммитов, вернуть «как было вчера». <br>
- Случайно изменился файл, который вообще не должен был меняться. Например, вы открыли не тот файл в редакторе и начали его исправлять. <br>

#### Выполнить unstage изменений — git restore --staged <file>
Допустим, вы создали или изменили какой-то файл и добавили его в список «на коммит» (staging area) с помощью __git add__, но потом передумали включать его туда. Убрать файл из staging поможет команда __git restore --staged <file>__ <br>
<br>
Чтобы «сбросить» все файлы из staged обратно в untracked/modified, можно воспользоваться командой __git restore --staged .__ -  она сбросит всю текущую папку __(.)__.

#### «Откатить» коммит — git reset --hard <commit hash>
Иногда нужно «откатить» то, что уже было закоммичено, то есть вернуть состояние репозитория к более раннему. Для этого используют команду __git reset --hard <commit hash>__. Внимание! <commit hash> - это коммит, к которому нужно откатиться, а не который нужно откатить.

#### «Откатить» изменения, которые не попали ни в staging, ни в коммит, — git restore <file>
Может быть так, что вы случайно изменили файл, который не планировали. Теперь он отображается в Changes not staged for commit (modified). Чтобы вернуть всё «как было», можно выполнить команду __git restore <file>__.

----
### Просматриваем изменения в файлах
По умолчанию команда __git diff__ не показывает изменения в staged-файлах — только в modified. <br>
Чтобы просмотреть изменения в staged, нужно использовать флаг --staged: __git diff --staged__. <br>
Чтобы просмотрить изменения между коммитами нужно выподнить: __git diff <хеш наиболее старого коммита> <хэш наиболее свежего коммита>__ <br>

----
### Игнорирование файлов в Git
Часто бывает так, что в папке-репозитории есть файлы, для которых не нужно хранить историю изменений. Например: в Git не принято коммитить результаты компиляции исходного кода, то есть получившиеся исполняемые файлы; среды разработки (вроде IntelliJ IDEA) могут создавать папку с вашими личными настройками проекта. <br>

Чтобы Git игнорировал такие файлы и не пытался добавить их в репозиторий, нужно __создать файл .gitignore__ и записать в него названия игнорируемых файлов. В этом уроке разберём, как это сделать. <br>
Файл .gitignore добавляют в корень репозитория и тоже коммитят. <br>
Правила из .gitignore применяются только к новым (untracked) файлам. Если файл уже попал в staging area или в коммит, то правила на него не распространяются. <br>
<br>
Пример:
````
# игнорировать все файлы в каталоге build
build/

# игнорировать все файлы "tmp" во всех подпапках папки docs
docs/*/tmp 

# игнорировать todo.txt в корне репозитория
/todo.txt

# для сравнения: spam.txt будет игнорироваться во всех папках
spam.txt 

# игнорировать файлы file0.txt, file1.txt и file2.txt
# при этом не игнорировать file3.txt, file4.txt, ...
file[0-2].txt 

# игнорировать все .log файлы
*.log

# не игнорировать *.log файлы в examples
# потому что это пример для документации
!examples/**/*.log 

# игнорировать все JPEG-файлы
*.jpeg

# но только не мем с Doge
!doge.jpeg
````

Посмотреть, что игнорируется, можно с помощью команды __git status --ignored__.
<br>

----
### Клонируем репозиторий

На платформе GitHub хранится множество проектов. Часть из них находится в открытом доступе. Такие open source проекты можно скачать на свой компьютер, внести какие-то правки или просто разобраться, как всё устроено внутри. <br>
Процесс копирования удалённого репозитория на локальный компьютер называется клонированием. __Клонирование репозитория — обычно первое, что делает разработчик на новом месте работы__.

#### Клонировать репозиторий — git clone
Копируем SSH ссылку репозитория на GitHub, который хотим склонировать. <br>
Переходи в консли в нужную папку. <br>
Выполняем команду: __git clone <ссылка вида - git@github.com:yandex-praktikum/git-clone-lesson.git>__ <br>
<br>
Команда git clone автоматически связывает локальный и удалённый репозиторий. То есть если в GitHub-репозитории что-то поменяется (например, добавятся коммиты), вам не нужно будет заново клонировать его. Достаточно будет выполнить команду, которая обновит вашу копию. <br>
Убедитесь в том, что репозитории связаны, командой __git remote -v__ (предварительно перейдя в папку репозитория).

----
### Выполняем Fork

Допустим, вы хотите усовершенствовать чужой проект или как-то использовать его в своей работе, но у вас нет прав на изменение оригинального репозитория.<br>
Fork в отличие от клонирования, она не скачает репозиторий на локальный компьютер, но добавит его прямо в ваш аккаунт на 
сервере GitHub. Fork создаёт копию репозитория в аккаунте GitHub. Такая копия будет полностью независима. Изменения, которые вы внесёте, не будут синхронизированы с исходным репозиторием.<br>
В процессе «форка» создаётся копия всех файлов, истории коммитов и веток. Эта копия сохраняется в вашей учётной записи GitHub.<br>
<br>
Вот некоторые из распространённых причин использования «форков»:<br>
1) Вы хотите внести свой вклад в проект (например, open source), но не имеете прав на изменение исходного репозитория. Тогда вы можете сделать «форк», добавить нужные правки, а затем отправить запрос на включение этих изменений в оригинальный проект.<br>
2) Вы хотите развивать проект независимо от исходного. Допустим, создатели проекта решили, что не будут добавлять функциональность, которая вам необходима. В таком случае вы можете сделать «форк» и добавить её самостоятельно.<br>

----
### Ветки
#### Что такое ветка
Ветка — это последовательность независимых изменений. <br>
Благодаря веткам несколько человек могут работать над одним репозиторием и не мешать друг другу. А ещё ветки помогают декомпозировать большую и страшную задачу на маленькие и понятные. <br>
Основная версия проекта хранится в главной ветке main (или master). <br>
С помощью команды __git branch__ можно посмотреть, какие в проекте есть ветки и в какой из них вы сейчас находитесь (отмечена звездочкой).<br>
Команда git branch -a показывает все ветки.

#### Создаём ветку
Создать ветку можно с помощью команды __git branch <название_ветки>__

#### Шагаем с ветки на ветку
Переключиться на другую ветку — __git checkout <название_ветки>__ <br>
Создать ветку и сразу переключиться на неё — __git checkout -b <название_ветки>__<br>
Ветка указывает на коммит, который сделан в ней последним. При этом две ветки могут ссылаться на один и тот же коммит — например, если вы только что создали ветку, но ещё не успели внести в неё коммит.

#### Сравниваем ветки
Сравнить ветки — git diff <название_ветки1> <название_ветки2> <br>

#### Как это работает
1) Есть файл в репе, лежит в main
2) Сохраняем его версию в git - __git add . && git commit -m "комментарий".__
3) Делаем новую ветку __git branch <название_ветки>__
4) Переходим в новую ветку __git checkout <название_ветки>__
5) Вносим правки в файл 
6) Сохраняем новый файл в git через выполнение команд: __git add . && git commit -m "комментарий".__
7) Можем сравнивать файлы из разных веток __git diff <название_ветки1> <название_ветки2>__ <br>

#### Полезное
Git поддерживает суффикс навигации `~`. С его помощью можно сослаться на предыдущие коммиты. Например, если вы находитесь в ветке main и хотите вывести разницу между тем коммитом, который был три коммита назад, и текущим, нужно выполнить `git diff main~3 main`.

#### Объединение и удаление веток

----


----