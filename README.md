# tp_lab_5

Изучение систем непрерывной интеграции на примере сервиса Travis CI

## Tasks

- [ ] 1. Ознакомиться со ссылками учебного материала
- [ ] 2. Выполнить инструкцию учебного материала
- [ ] 3. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```bash
$ export GITHUB_USERNAME=<имя_пользователя> // Создание переменной с именем пользователя на GitHub
$ export GIST_TOKEN=<сохраненный_токен> // Создание перменной, которая хранит токен
$ alias edit=vim // Открытие текстового редактора
```

```ShellSession
$ mkdir -p ${GITHUB_USERNAME}/workspace // Создание директория workspace
$ cd ${GITHUB_USERNAME}/workspace // Переход в нужную директорию
$ pushd . // Сохранение адреса текущего каталога
```
```ShellSession
$ \curl -sSL https://get.rvm.io | bash -s -- --ignore-dotfiles
$ echo "source $HOME/.rvm/scripts/rvm" >> scripts/activate
$ rvm autolibs disable
$ rvm install ruby-2.4.2

Searching for binary rubies, this might take some time.
No binary rubies available for: osx/10.13/x86_64/ruby-2.4.2.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Installing Ruby from source to: /Users/elshan/.rvm/rubies/ruby-2.4.2, this may take a while depending on your cpu(s)...
ruby-2.4.2 - #downloading ruby-2.4.2, this may take a while depending on your connection...
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
Dload  Upload   Total   Spent    Left  Speed
100 12.0M  100 12.0M    0     0  5534k      0  0:00:02  0:00:02 --:--:-- 5533k
ruby-2.4.2 - #extracting ruby-2.4.2 to /Users/elshan/.rvm/src/ruby-2.4.2.....
ruby-2.4.2 - #configuring......................................................-
ruby-2.4.2 - #post-configuration.
ruby-2.4.2 - #compiling........................................................-
ruby-2.4.2 - #installing.......
ruby-2.4.2 - #making binaries executable..
ruby-2.4.2 - #downloading rubygems-2.7.7
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
Dload  Upload   Total   Spent    Left  Speed
100  894k  100  894k    0     0  1627k      0 --:--:-- --:--:-- --:--:-- 1629k
No checksum for downloaded archive, recording checksum in user configuration.
ruby-2.4.2 - #extracting rubygems-2.7.7.....
ruby-2.4.2 - #removing old rubygems........
$LANG was empty, setting up LANG=en_US.US-ASCII, if it fails again try setting LANG to something sane and try again.
ruby-2.4.2 - #installing rubygems-2.7.7................................
ruby-2.4.2 - #gemset created /Users/elshan/.rvm/gems/ruby-2.4.2@global
ruby-2.4.2 - #importing gemset /Users/elshan/.rvm/gemsets/global.gems..........there was an error installing gem rubygems-bundler
....................
ruby-2.4.2 - #generating global wrappers.......
ruby-2.4.2 - #gemset created /Users/elshan/.rvm/gems/ruby-2.4.2
ruby-2.4.2 - #importing gemsetfile /Users/elshan/.rvm/gemsets/default.gems evaluated to empty gem list
ruby-2.4.2 - #generating default wrappers.......
ruby-2.4.2 - #adjusting #shebangs for (gem irb erb ri rdoc testrb rake).
Install of ruby-2.4.2 - #complete
Ruby was built without documentation, to build it run: rvm docs generate-ri

$ rvm use 2.4.2 --default
$ gem install travis
```

```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab04 projects/lab05 // Клонирование репозитория
$ cd projects/lab05 // Переход
$ git remote remove origin // Удаление старого origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab05 // Указание нового origin-репозитория
```

```ShellSession
$ cat > .travis.yml <<EOF // Установка языка программирования
language: cpp
EOF
```

```ShellSession
$ cat >> .travis.yml <<EOF

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
```

```ShellSession
$ cat >> .travis.yml <<EOF

addons:
apt:
sources:
- george-edison55-precise-backports
packages:
- cmake
- cmake-data
EOF
```

```ShellSession
$ travis login --github-token ${GITHUB_TOKEN} // Настраиваиваем системы Travis с помощью персонального токена
```

```ShellSession
$ travis lint // Cчитывание файлов и вывод предупреждений и ошибок при их наличии
/*Warnings for .travis.yml:
[x] value for addons section is empty, dropping
[x] in addons section: unexpected key apt, dropping*/
```

```ShellSession
$ ex -sc '1i|<фрагмент_вставки_значка>' -cx README.md // Добавляем виджет Travis
```

```ShellSession
$ git add .travis.yml // Добавляем файлы
$ git add README.md
$ git commit -m"added CI" // Добавление комменатрия к коммиту
$ git push origin master // Пуш
```

```ShellSession
$ travis lint // Проверяем на наличие ошибок
/*Warnings for .travis.yml:
[x] value for addons section is empty, dropping
[x] in addons section: unexpected key apt, dropping*/
$ travis accounts // Информация об учётных записях
/* (elpidifor): subscribed, 11 repositories
bmstu-iu8-11-cpp-2017 (): subscribed, 4 repositories*/
$ travis sync // Синхронизация
*/synchronizing: ........ done*/
$ travis repos // Отображение списка репозиториев
/*elpidifor/ColorDefence (active: no, admin: yes, push: yes, pull: yes)
Description: Homework №2


elpidifor/bmstu-programming-languages (active: yes, admin: yes, push: yes, pull: yes)
Description: Лабораторные работы по курсу АЯ. 1 семестр

elpidifor/lab02 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

elpidifor/lab03 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

elpidifor/lab05 (active: yes, admin: yes, push: yes, pull: yes)
Description: ???

elpidifor/lab1 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

elpidifor/lab2 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

elpidifor/lab4 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

elpidifor/lb (active: no, admin: yes, push: yes, pull: yes)
Description: ???

elpidifor/rk2 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

elpidifor/tgbot (active: no, admin: yes, push: yes, pull: yes)
Description: homework-telegram-bot

bmstu-iu8-11-cpp-2017/lab03-elpidifor (active: yes, admin: no, push: yes, pull: yes)
Description: lab03-elpidifor created by GitHub Classroom

bmstu-iu8-11-cpp-2017/lab05-elpidifor (active: yes, admin: no, push: yes, pull: yes)
Description: lab05-elpidifor created by GitHub Classroom

bmstu-iu8-11-cpp-2017/lab06-elpidifor (active: yes, admin: no, push: yes, pull: yes)
Description: lab06-elpidifor created by GitHub Classroom

bmstu-iu8-11-cpp-2017/test-m2-remake-elpidifor (active: no, admin: no, push: yes, pull: yes)
Description: test-m2-remake-elpidifor created by GitHub Classroom*/
$ travis enable // Активация проектов
/*Detected repository as elpidifor/lab05, is this correct? |yes|
elpidifor/lab05: enabled :)*/
$ travis whatsup // Суммарное количество сборок
/*bmstu-iu8-11-cpp-2017/lab06-elpidifor passed: #6
bmstu-iu8-11-cpp-2017/lab05-elpidifor passed: #58
bmstu-iu8-11-cpp-2017/lab03-elpidifor passed: #8*/
$ travis branches // Вывод последней сборки
/*master:  #2    failed     Delete CMakeLists.txt*/
$ travis history // История
/*#2 failed:       master Delete CMakeLists.txt
#1 canceled:     master Delete README.md*/
$ travis show // Общая информация
/*Job #2.1:  Delete CMakeLists.txt
State:         failed
Type:          push
Branch:        master
Compare URL:   https://github.com/elpidifor/lab05/compare/e599870c503c...39a7e0ccd151
Duration:      23 sec
Started:       2018-09-18 14:17:27
Finished:      2018-09-18 14:16:04
Allow Failure: false
Config:        os: linux*/
```

## Report

```ShellSession
$ popd
$ export LAB_NUMBER=05
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [Travis Client](https://github.com/travis-ci/travis.rb)
- [AppVeyour](https://www.appveyor.com/)
- [GitLab CI](https://about.gitlab.com/gitlab-ci/)

```
Copyright (c) 2017 Братья Вершинины
```
