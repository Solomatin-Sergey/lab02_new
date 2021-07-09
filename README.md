# lab02_dz
## Изучение систем контроля версий на примере Git
### Part I.
> 1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).

Репозиторий создан.

> 2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.

vim README.md

git add README.md

git commit -m "add README.md"

[master (корневой коммит) e7d0009] add README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
 
 > 3.Создайте файл hello_world.cpp в локальной копии репозитория (который должен был появиться на шаге 2). 
 > Реализуйте программу Hello world на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку using namespace std;. 
 
#include <iostream>
using namespace std; 
int main ()
{ 
cout << "Hello world\n"; 
}

> 4. Добавьте этот файл в локальную копию репозитория.

git add hello_world.cpp

> 5. Закоммитьте изменения с осмысленным сообщением.

git commit -m "add hello_world.cpp"

[master 0eb73a3] add hello_world.cpp
 1 file changed, 6 insertions(+)
 create mode 100644 hello_world.cpp
 
 > 6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. 
 > А в стандартный поток вывода печаталось сообщение Hello world from @name, где @name имя пользователя.
 
#include <iostream>
using namespace std;
int main ()
{
string name;
cin >> name;
cout << "Hello world from " << name << "\n";
}

> 7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно git add?

git commit -m " modified hello_world.cpp" -a

[master ad46de7]  modified hello_world.cpp
 1 file changed, 3 insertions(+), 1 deletion(-)
 
 > 8. Запуште изменения в удалёный репозиторий.
 
 git push origin master
 
 > 9. Проверьте, что история коммитов доступна в удалёный репозитории.
 
 Можно зайти в файл hello_world.cpp, а потом во вкладку History. История коммитов доступна.
 
 ### Part II.

> 1. В локальной копии репозитория создайте локальную ветку patch1.

git branch patch1

git checkout patch1

Переключено на ветку «patch1»


> 2. Внесите изменения в ветке patch1 по исправлению кода и избавления от using namespace std;.

vim hello_world.cpp

#include <iostream>
    int main ()
    {
        std::string name;
        std::cin >> name;
        std::cout << "Hello world from " << name << "\n";
    }


> 3. commit, push локальную ветку в удалённый репозиторий.

git commit -m "correct hello_world.cpp" -a

[patch1 d91e307] correct hello_world.cpp
 1 file changed, 3 insertions(+), 4 deletions(-)
 
git push origin patch1

> 4. Проверьте, что ветка patch1 доступна в удалённом репозитории.

Теперь веток 2: master и patch1.

> 5. Создайте pull-request patch1 -> master.

Solomatin-Sergey wants to merge 1 commit into master from patch1

> 6. В локальной копии в ветке patch1 добавьте в исходный код комментарии.
 
 vim hello_world.cpp

 #include <iostream>
int main ()
{
	std::string name;
	std::cin >> name;
	std::cout << "Hello world from " << name << "\n";
}
// my first comment

> 7. commit, push.
 
 git commit -m"add comment" -a
 
[patch1 c06512d] add comment
 1 file changed, 1 insertion(+)
 
git push origin patch1 

> 8. Проверьте, что новые изменения есть в созданном на шаге 5 pull-request
 
 ![examine](https://github.com/Solomatin-Sergey/lab02_new/blob/master/add%20comment.png)

> 9. В удалённом репозитории выполните слияние PR patch1 -> master и удалите ветку patch1 в удаленном репозитории.

Solomatin-Sergey merged commit 891bda6 into master 1 minute ago
	
Solomatin-Sergey deleted the patch1 branch 1 minute ago

> 10. Локально выполните pull.
	
git pull origin master
	
> 11. С помощью команды git log просмотрите историю в локальной версии ветки master.
	
git log
commit ad46de7587171675c482d55bfbf74413bcbafb54 (HEAD -> master)
Author: Solomatin-Sergey <serg.solomatin@inbox.ru>
Date:   Fri Jul 9 12:21:45 2021 +0300

     modified hello_world.cpp

commit 0eb73a3716febd42225bd46b08ef614847daa0b6
Author: Solomatin-Sergey <serg.solomatin@inbox.ru>
Date:   Fri Jul 9 12:16:59 2021 +0300

    add hello_world.cpp

commit e7d00097c0eb0d0edf5afe2651874f2041c8ea61
Author: Solomatin-Sergey <serg.solomatin@inbox.ru>
Date:   Fri Jul 9 12:11:09 2021 +0300

    add README.md
	
> 12. Удалите локальную ветку patch1.
	
git branch -D patch1
	
Ветка patch1 удалена (была 891bda6).
	
### Part III.	
	
> 1. Создайте новую локальную ветку patch2.
	
git branch patch2
	
git checkout patch2
	
Переключено на ветку «patch2»
	
> 2. Измените code style с помощью утилиты clang-format. Например, используя опцию -style=Mozilla.
	
clang-format -style=Mozilla hello_world.cpp
	
#include <iostream>
using namespace std;
int
main()
{
  string name;
  cin >> name;
  cout << "Hello world from " << name << "\n";
}

> 3. commit, push, создайте pull-request patch2 -> master.
	
git commit -m"style=Mozilla" -a
    
git push origin patch2
	
> 4. В ветке master в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
	
/* This is new comment!!!!!*/
	
> 5. Убедитесь, что в pull-request появились конфликты.
	
This branch has conflicts that must be resolved
	
> 6. Для этого локально выполните pull + rebase (точную последовательность команд, следует узнать самостоятельно). Исправьте конфликты.

git checkout master
	
git rebase master
	
git checkout patch2
	
git merge patch2
	
> 7. Сделайте force push в ветку patch2
	
git push --force origin patch2
	
> 8. Убедитеcь, что в pull-request пропали конфликты.
> 9. Вмержите pull-request patch2 -> master.
	
Pull request successfully merged and closed	
