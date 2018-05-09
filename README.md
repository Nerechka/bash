# bash
Bash: Основы командной строки с сайта hexlet.io

# Команды навигации
* **pwd** - где я? 
* **ls** -  выводит все содержимое директории;
* **cd** - используется для просмотра или изменения пути текущего каталога (пермещение в домашнюю категорию);
* **cd..** - перемещение в директорию уровнем выше;
* **cd /** - перемещение в корневую директорию;
* **cd ~/filename/** - сокращенное перемещение в папку из домашней директории;

# Команды, изменяющие файловую структуру
* **mkdir** - создает директорию;
* **mkdir test** - создаст директорию test;
* **mkdir -p test2/test3** - создаст директорию test3 и её родительскую директорию test2;
* **touch file1** - создаст file1;
* **three filename** - выведет структуру файлов внутри filename в виде дерева;
* **mv** - переименовывает файл;
* **mv test test3** - переименует папку test в test3;
* **mv test2/\* test3** - перемещает всё содержимое папки test2 в test3;
* **rm file** - удаляет файл;
* **rm -r test1** - удаляет ДИРЕКТОРИЮ test1;
* **rm -r \*** - удаляет содержимое директории (при учете, что вы находитесь в директории во время ввода команды);
* **rm -r test3/\*** - то же самое, "изнутри" папки test3;
* **rm -r -f** или **rm -rf** - флаги для удаления файлов по умолчанию, без вопросов об их удалении;

# Команды для просмотра содержимого
* **cat file** - выводит содержимое файла;
* **head file** - выводит первые 10 строк по умолчанию;
* **tail file** - 10 последних записей;
* **tail -f file** - автоматически показывает изменения, происходящее в файле (если они есть);
* **grep** - позволяет искать подстроку в файле;
* **grep 'Apr 27' file** - найдёт все записи в которых встречается 27 апреля в file;

# Программы - пейджеры
Используются, когда открываемый файл слишком большой.  
Открывает файл не целиком, а только часть, видимую на экране. При перемещении - подгружаются другие части.
Работает в режиме vim(а);

# Документация
* **man** - показывает страницу документации конкретной программы/команды;  
Работает в режиме пейджера

# Переменные окружения
Переменные окружения регистрозависые, поэтому переменные **MYVAR** и **MyVar** - две разные переменные;
* **which названиеКомандыBash** - показывает, где лежит программа. Например, **which ls**;
* **VAR=3** - задать переменную;
* **echo $VAR** - вывести переменную;
* **env** - выводит переменные в текущей сессии;
* **unset VAR** - удаляет переменную в рамках текущей сессии;

Например, есть простая программа **./printer**, которая содержит в себе: 
**echo 'MYVAR: $MYVAR'**
Зададим переменную **MYVAR=5** и вызовем программу **./printer**: 
В выводе будет **MYVAR:**, но если просто вывести переменную **echo MYVAR**:
**5**. 
Так происходит, потому что команда **MYVAR=5** делает переменную доступной только в рамках текущей сессии, а при вывозве программы **./printer** запускается новая сессия. 
Поэтому существует два варианта: 
* **MYVAR=3 ./printer** - задание переменной непосредственно перед вызовом программы;
* **export MYVAR=4** - экспорт переменной, она становится доступной для всех программ, запускаемых с помощью данной командной оболочки её можно увидеть, вызвав команду **env**.

# Перенаправления и Потоки
При вызове команды **ls** происходит вывод данных "на экран", но с точки зрения программы, он происходит не "на экран", а в стандартный поток вывода **STDOUT**. Bash по умолчанию печатает его "на экран". При этом можно делать перенаправления, и вывести поток в файл.  
**ls > output** - в файле output окажется вовод данных команды ls.  
Так же мы можем читать файл с помощью стандартного потока ввода **STDING**  
Например, имеется набор неотсортированных данных **unsorted**. С помощью команды **sort** их можно отсортировать и прочитать прямо из файла:  
**sort < unsorted**  
Так же можно отсортировать и вместо вывода результата на экран, записать его в файл **sorted**:  
**sort < unsorted > sorted**  
Можно передать данные не только из файла в файл, а из программы в программу.  Это называется **конвейер** и обозначается **|**. Конвейер перенаправляет STDOUT одного процесса в STDIN другого. Например:  
**cat unsorted | sort** - в вывод команды **cat** передается **unsorted** , и уже он перенаправляется в **sort**.  
В конвейер можно подставлять любое количество элементов, например:  
**cat unsorted | sort | uniq** - теперь все повторяющиеся данные исключены и присутствуют в единственном варианте  

Конвейер часто используется в поиске **grep**, как фильтр, например:  
* **ls | grep test**; (**unic** убирает дубли, идущие подряд)
* **ls | wc** - выводит количество строк - слов - букв, которые были в выводе команды **ls** (**wc** = **world count**. Команда **Wc -l** выводит количество строк).

# История команд
История команд пользователя сохраняется в директории **~/.bash_history**
Существует так же большое количество команд для взаимодействия с историей  
* **history** - выводит всю историю;  
* **!210** - где 210 - номер команды в истории, так происходит её вызов;  
* **!!** - вызов последней команды;  
Поиск по истории
Режим поиск включается по **Ctrl-r**. Для поиска следующего совпадения надо повторно нажать **Ctrl-r**

# Алиасы
**alias** - список всех алиасов;  
**alias l='ls - CF'** - задаёт алиас l;
**type l** - смотрит, чему равен алиас l
**unalias l** - удаляет алиас;

