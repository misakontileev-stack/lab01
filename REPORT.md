
## Laboratory work I

Данная лабораторная работа посвещена изучению утилит для разработки проектов

## Tasks

- [ ] 1. Ознакомиться со ссылками учебного материала
- [ ] 2. Выполнить инструкцию учебного материала
- [ ] 3. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Студент
Контилеев Михаил
Группа: ИУ8-21  
Дата: 17.02.2026

---

## Ход работы

### 1. Настройка окружения*
```bash
$ export GITHUB_USERNAME=<имя пользователя>
$ export GIST_TOKEN=<токен>
$ alias edit=nano

Результат: переменные окружения заданы, alias работает.

---

### 2. Создание структуры папок
```sh
$ mkdir -p ${GITHUB_USERNAME}/workspace
$ cd ${GITHUB_USERNAME}/workspace
$ pwd
$ cd ..
$ pwd
```

```sh
$ mkdir -p workspace/tasks/
$ mkdir -p workspace/projects/
$ mkdir -p workspace/reports/
$ cd workspace
```

Результат: создана структура папок tasks, projects, reports.


```sh
### 3. Установка Node.js
$ wget https://nodejs.org/dist/v6.11.5/node-v6.11.5-linux-x64.tar.xz

Вывод:
--2026-02-18 15:43:14--  https://nodejs.org/dist/v6.11.5/node-v6.11.5-linux-x64.tar.xz
Распознаётся nodejs.org (nodejs.org)… 104.20.1.252, 172.66.128.70, 2606:4700:10::6814:1fc, ...
Подключение к nodejs.org (nodejs.org)|104.20.1.252|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа… 200 OK
Длина: 9356460 (8,9M) [application/x-xz]
Сохранение в: ‘node-v6.11.5-linux-x64.tar.xz’
node-v6.11.5-linux-x64.tar.xz        100%[===================================================================>]   8,92M  6,90MB/s    за 1,3s    
2026-02-18 15:43:16 (6,90 MB/s) - ‘node-v6.11.5-linux-x64.tar.xz’ сохранён [9356460/9356460]

$ tar -xf node-v6.11.5-linux-x64.tar.xz
$ rm -rf node-v6.11.5-linux-x64.tar.xz
$ mv node-v6.11.5-linux-x64 node
```


```sh
$ ls node/bin
Вывод:
node  npm

$ echo ${PATH}
Вывод: 
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin

$ export PATH=${PATH}:`pwd`/node/bin
$ echo ${PATH}
Вывод: 
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin:/home/misha/misakontileev/workspace/reports/lab01/node/bin

$ mkdir scripts
$ cat > scripts/activate<<EOF
export PATH=\${PATH}:`pwd`/node/bin
EOF
$ source scripts/activate
```

Результат: Node.js установлен, путь обновлен.

### 4. Установка утилиты Gist

```sh
$ gem install gist
Вывод:
Successfully installed gist-6.0.0
Parsing documentation for gist-6.0.0
Done installing documentation for gist after 0 seconds
1 gem installed

```

```sh
$ (umask 0077 && echo ${GIST_TOKEN} > ~/.gist)
```

Результат: утилита Gist установлена, токен сохранен.


## Report

```sh
$ export LAB_NUMBER=01
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
Редактировал в текстовом редакторе nano.
$ gist REPORT.md
```

## Homework

1. Скачайте библиотеку *boost* с помощью утилиты **wget**. Адрес для скачивания `https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz`.
2. Разархивируйте скаченный файл в директорию `~/boost_1_69_0`
3. Подсчитайте количество файлов в директории `~/boost_1_69_0` **не включая** вложенные директории.
Команда: find ~/boost_1_69_0 -maxdepth 1 -type f | wc -l
Вывод: 16.
4. Подсчитайте количество файлов в директории `~/boost_1_69_0` **включая** вложенные директории.
Команда: find ~/boost_1_69_0 -type f | wc -l
Вывод: 62050.
5. Подсчитайте количество заголовочных файлов, файлов с расширением `.cpp`, сколько остальных файлов (не заголовочных и не `.cpp`).
Команда: find ~/boost_1_69_0 -type f \( -name "*.hpp" -o -name "*.h" \) | wc -l
Вывод: 15208.
Команда: find ~/boost_1_69_0 -type f -name "*.cpp" | wc -l
Вывод: 13789.
Остальные файлы по команде: find ~/boost_1_69_0 -type f ! -name "*.hpp" ! -name "*.h" ! -name "*.cpp" | wc -l
Вывод: 33053.
6. Найдите полный пусть до файла `any.hpp` внутри библиотеки *boost*.
Команда: find ~/boost_1_69_0 -name any.hpp > 1.txt
Вывод в файле 1.txt
7. Выведите в консоль все файлы, где упоминается последовательность `boost::asio`.
Команда: grep -r "boost::asio" ~/boost_1_69_0 > 2.txt
Вывод в файле 2.txt
8. Скомпилирутйе *boost*. Можно воспользоваться [инструкцией](https://www.boost.org/doc/libs/1_61_0/more/getting_started/unix-variants.html#or-build-custom-binaries) или [ссылкой](https://codeyarns.com/2017/01/24/how-to-build-boost-on-linux/).
9. Перенесите все скомпилированные на предыдущем шаге статические библиотеки в директорию `~/boost-libs`.
10. Подсчитайте сколько занимает дискового пространства каждый файл в этой директории.
Команда: du -h ~/boost-libs/* > 3.txt
Вывод в файле 3.txt
11. Найдите *топ10* самых "тяжёлых".
Команда: du -h ~/boost-libs/* | sort -hr | head -10 > 4.txt
Вывод в файле 4.txt
Copyright (c) 2015-2021 The ISC Authors
```
