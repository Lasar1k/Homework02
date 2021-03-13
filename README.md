# Homework02
Just typing some words so it could be different from main branch // для задания 1 и 2
## Part 1
1.Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2.Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3.Создайте файл hello_world.cpp в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу Hello world на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку using namespace std;.
```
$ cat > hello_world.cpp <<EOF // создаём исполняемый файл hello_world.cpp который печатает "Hello world"
> #include <iostream>
> using namespace std;
> int main(int argc, char** argv)
> {
> cout << "Hello world";
> }
> EOF
```
4.Добавьте этот файл в локальную копию репозитория.
```
$ git add hello_world.cpp
```
5.Закоммитьте изменения с осмысленным сообщением.
```
$ git commit -m "Added alpha version of hello_world.cpp"
```
6.Измените исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение Hello world from @name, где @name имя пользователя.
```
$ nano hello_world.cpp // открываем редактор чтобы изменить файл
> #include <iostream>
> #include <string>
> using namespace std;
> int main(int argc, char** argv)
> {
> string a;
> cout << "Please insert your name: "
> cin >> a;
> cout << endl << "Hello world from " << a;
> }
```
7.Закоммитьте новую версию программы. Почему не надо добавлять файл повторно git add?
```
$ git commit -a //совершает коммит автоматически индексируя изменения в файлах проекта
> Added printing user's name
```
8.Запуште изменения в удалёный репозиторий.
```
$ git push --set-upstream origin master
```
9.Проверьте, что история коммитов доступна в удалёный репозитории.
```
Доступна: $ git log
```
## Part 2
1.В локальной копии репозитория создайте локальную ветку patch1.
```
$ git checkout -b pathc1
```
2.Внесите изменения в ветке patch1 по исправлению кода и избавления от using namespace std;.
```
$ nano hello_world.cpp // открываем редактор и меняем файл
>#include <iostream>
>#include <string>
>int main(int argc, char** argv)
>{
>std::string a;
>std::cout << "Please insert your name: "
>std::cin >> a;
>std::cout << std::endl << "Hello world from: " << a;
>}
$ git add . // добавляем изменённый файл в индекс репозитория patch1 
```
3.commit, push локальную ветку в удалённый репозиторий.
```
$ git commit -m "Remove namespace std" //комиттим
$ git push origin patch1 //добавляем изменения на удалённый репозиторий
```
4.Проверьте, что ветка patch1 доступна в удалёный репозитории.(Доступна)
5.Создайте pull-request patch1 -> master.
```
$ git pull origin patch1
```
6.В локальной копии в ветке patch1 добавьте в исходный код комментарии.
```
$ nano hello_world.cpp
>#include <iostream>
>#include <string>
>//commentarii 1
>int main(int argc, char** argv)
>{ // commentariii2
>std::string a;
>std::cout << "Please insert your name: "
>std::cin >> a;
>std::cout << std::endl << "Hello world from: " << a;
>}
$ git add .
```
7.commit, push.
```
$ git commit -m "Give comments"
$ git push origin patch1
```
8.Проверьте, что новые изменения есть в созданном на шаге 5 pull-request (Есть)
9.В удалённый репозитории выполните слияние PR patch1 -> master и удалите ветку patch1 в удаленном репозитории.
10.Локально выполните pull.
```
$ git checkout master
$ git pull
```
11.С помощью команды git log просмотрите историю в локальной версии ветки master.
```
$ git log
```
12.Удалите локальную ветку patch1.
```
$ git branch -d patch1
```
## Part 3
1.Создайте новую локальную ветку patch2.
```
$ git checkout -b patch2
```
2.Измените code style с помощью утилиты clang-format. Например, используя опцию -style=Mozilla.
```
$ sudo apt-get install clang-format // устанавливаем утилиту clang-format
$ clang-format -i -style=Mozilla hello_world.cpp // изменяем стиль кода
```
3.commit, push, создайте pull-request patch2 -> master.
```
$ git add hello_world.cpp
$ git commit -m "Changed code style to Mozilla"
$ git push origin patch2
```
4.В ветке master в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5.Убедитесь, что в pull-request появились конфликтны.
```
$ git push origin patch2 // В pull-request появился флаг с конфликтом
```
6.Для этого локально выполните pull + rebase (точную последовательность команд, следует узнать самостоятельно). Исправьте конфликты.
```
$ git checkout patch2
$ git pull origin master
$ git rebase master // появились конфликты в файле hello_world.cpp
$ git add hello_world.cpp
$ git commit -m 'Solved conflict'
$ git rebase master // конфликт остался
$ git add hello_world.cpp
$ git rebase --continue // конфликты ушли
```
7.Сделайте force push в ветку patch2
```
$ git push origin patch2 --force
```
8.Убедитель, что в pull-request пропали конфликтны. // конфликтов нет
9.Вмержите pull-request patch2 -> master.
