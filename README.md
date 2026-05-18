# DataProject: Управление версиями с Git (CLI + Visual Studio)

## Описание проекта

Этот проект демонстрирует полный рабочий процесс управления версиями с использованием Git и Visual Studio.

**Цель:** Создать локальный репозиторий, выполнить изменения в коде, объединить коммиты через **интерактивный ребейз** (squash) и отправить результат в удалённый репозиторий.

**Ключевая задача:** Превратить два коммита (`Add Data.cs` и `change data type`) в один чистый коммит `Add Data.cs with final content` перед отправкой на сервер.

---

## Технологии

- **Git** (командная строка)
- **Visual Studio** (Team Explorer / Git Changes)
- **GitHub** (удалённый репозиторий)

---

## Структура репозитория
DataProject/ └── Data.cs # Файл с данными (изменялся в процессе)


### Содержимое `Data.cs` (финальное):
```csharp
string data = "Updated";
Этапы выполнения
Часть 1: Работа в командной строке (Git CLI)
Создание папки и инициализация Git:

mkdir DataProject
cd DataProject
git init
Создание файла и первого коммита (main):

echo "int data = 0;" > Data.cs
git add Data.cs
git commit -m "Add Data.cs"
Создание ветки data-update:

git checkout -b data-update
Изменение данных и второй коммит:

echo "string data = \"Updated\";" > Data.cs
git add Data.cs
git commit -m "change data type from int to string"
Проверка истории (должно быть 2 коммита):

git log --oneline
# f1e2d3c (HEAD -> data-update) change data type...
# a1b2c3d (main) Add Data.cs
Часть 2: Интерактивный ребейз (объединение коммитов)
Выполняем команду для объединения двух последних коммитов:

git rebase -i HEAD~2
В открывшемся редакторе (Vim/Nano/VS Code):

Меняем вторую строку:
pick a1b2c3d Add Data.cs
squash f1e2d3c change data type from int to string   # Меняем pick на squash
Сохраняем и закрываем (:wq для Vim, Ctrl+X для Nano).
Редактируем сообщение нового коммита:
Add Data.cs with final content

- Initial: int data = 0;
- Updated: string data = "Updated";
Сохраняем.
Результат:

git log --oneline
# g3h4i5j (HEAD -> data-update) Add Data.cs with final content
Готово! В ветке data-update теперь один коммит вместо двух.

Часть 3: Отправка в удалённый репозиторий
Способ А: Командная строка
git remote add origin https://github.com/user/data.git
git push -u origin data-update
Способ Б: Visual Studio (без команд)
Открыть проект:
Файл → Открыть → Проект/Решение → выбрать папку DataProject
Подключить Git:
Вид → Team Explorer (Ctrl + 0, E)
Домашняя → Синхронизация → Опубликовать
Ввести URL репозитория → Опубликовать
Отправить ветку:
В Team Explorer → Синхронизация
Нажать Отправить (Push) для ветки data-update
Альтернатива (VS 2022+):

Вид → Git Changes (Ctrl + 0, G)
Нажать кнопку Push (стрелка вверх) рядом с веткой data-update
Результат работы
В локальном репозитории:
$ git log --oneline
b2c3d4e (HEAD -> data-update) Add Data.cs with final content
В удалённом репозитории (GitHub):
Ветка data-update содержит один коммит
История чистая, без промежуточного изменения типа данных
Содержимое файла:
string data = "Updated";
Возможные проблемы и решения
Проблема	Решение
Конфликт при ребейзе	git rebase --abort → повторить попытку, проверив изменения
Закрылся редактор Vim	Нажми Esc, затем введи :wq и Enter
Visual Studio не видит ветку	Нажми Fetch в Git Changes
Ошибка "failed to push"	Убедись, что добавлен remote: git remote -v
Проверочный чек-лист
 Репозиторий DataProject инициализирован
 Файл Data.cs создан и закоммичен в main
 Создана ветка data-update
 В data-update файл изменён и закоммичен
 Выполнен git rebase -i HEAD~2 с заменой pick на squash
 Два коммита объединены в один
 Ветка отправлена в удалённый репозиторий (CLI или VS)
Дополнительная информация
Интерактивный ребейз используется для очистки истории перед публикацией.
Visual Studio поддерживает ребейз через графический интерфейс: Git → Manage Branches → Rebase.
squash объединяет коммиты, сохраняя их изменения в одном.
Автор
Решение выполнено в рамках учебного задания по работе с Git и Visual Studio.

