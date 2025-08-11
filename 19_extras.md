# 🎯 Git Extras: дополнительные команды и фишки

Команды и возможности Git, которые не вошли в основной курс, но могут быть очень полезными в работе.  
Эти инструменты помогут углубить понимание Git и повысить продуктивность.

---

## 🔍 Git Blame: кто написал эту строчку?

```bash
git blame filename
```

Показывает, кто и когда изменял каждую строку файла.

### Пример вывода:
```
a1b2c3d4 (John Doe    2023-01-15 14:30:25 +0300  1) function login() {
e5f6g7h8 (Jane Smith  2023-02-20 09:15:42 +0300  2)   console.log("Login");
a1b2c3d4 (John Doe    2023-01-15 14:30:25 +0300  3) }
```

### Полезные опции:
```bash
git blame -L 10,20 filename  # только строки 10-20
git blame -w filename        # игнорировать пробелы
git blame -M filename        # отслеживать перемещения кода
```

---

## ✂️ Git Bisect: поиск багов в истории

Бинарный поиск коммита, который ввёл баг.

### Процесс:
```bash
# Начать bisect
git bisect start

# Отметить текущий коммит как плохой
git bisect bad

# Отметить хороший коммит (например, неделю назад)
git bisect good HEAD~10

# Git переключится на средний коммит
# Тестируем и отмечаем:
git bisect good   # если баг отсутствует
git bisect bad    # если баг присутствует

# Git автоматически найдёт проблемный коммит
# Завершить bisect
git bisect reset
```

### Автоматический bisect:
```bash
git bisect run npm test  # автоматически тестировать
```

---

## 📊 Git Log: продвинутое форматирование

### Красивый однострочный лог:
```bash
git log --pretty=oneline
git log --oneline  # сокращённая версия
```

### Кастомный формат:
```bash
git log --pretty=format:"%h %s" --graph
```

### Полезные форматы:
```bash
# Хеш и сообщение
git config --global alias.last 'log -1 HEAD'

# График с именами авторов
git log --pretty=format:"%h %s" --graph

# Статистика изменений
git log --stat

# Только файлы
git log --name-only
```

---

## 🎨 Git Config: настройка редактора

```bash
# Настроить Notepad++ как редактор по умолчанию
git config --global core.editor "C:/Program Files (x86)/Notepad++/notepad++.exe"

# Другие популярные редакторы:
git config --global core.editor "code --wait"  # VS Code
git config --global core.editor "vim"          # Vim
git config --global core.editor "nano"         # Nano
```

---

## 🔍 Git Filter-Branch: массовые изменения истории

⚠️ **Очень мощная и опасная команда!**

### Удалить файл из всей истории:
```bash
git filter-branch --tree-filter 'rm -f passwords.txt' HEAD
```

### Изменить email во всей истории:
```bash
git filter-branch --env-filter '
if [ "$GIT_COMMITTER_EMAIL" = "old@example.com" ]
then
    export GIT_COMMITTER_EMAIL="new@example.com"
fi
' HEAD
```

---

## 🔄 Git Rerere: запоминание решений конфликтов

**Rerere** = "Reuse Recorded Resolution"

```bash
# Включить rerere
git config --global rerere.enabled true

# Git будет запоминать, как вы решаете конфликты
# При повторном конфликте предложит то же решение
```

### Полезно при:
- Частых rebase операциях
- Повторяющихся конфликтах
- Работе с долгоживущими ветками

---

## 📦 Git Submodule: подключение внешних репозиториев

### Добавить submodule:
```bash
git submodule add https://github.com/user/lib.git lib
```

### Клонировать проект с submodules:
```bash
git clone --recursive https://github.com/user/project.git
```

### Обновить submodules:
```bash
git submodule update --init --recursive
```

### Полезные команды:
```bash
git submodule status    # статус submodules
git submodule foreach git pull  # обновить все submodules
```

---

## 🎭 Git Aliases: создание псевдонимов

### Настройка полезных алиасов:
```bash
# Красивый лог
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# Статус
git config --global alias.st status

# Быстрый коммит
git config --global alias.ci commit

# Checkout
git config --global alias.co checkout

# Последний коммит
git config --global alias.last 'log -1 HEAD'

# Unstage файлов
git config --global alias.unstage 'reset HEAD --'

# Показать ветки
git config --global alias.br branch
```

### Использование:
```bash
git st        # вместо git status
git lg        # красивый лог
git last      # последний коммит
git unstage file.txt  # убрать из staging
```

---

## 🔧 Git Maintenance: обслуживание репозитория

### Очистка и оптимизация:
```bash
# Сборка мусора
git gc

# Агрессивная оптимизация
git gc --aggressive

# Проверка целостности
git fsck

# Очистка удалённых веток
git remote prune origin

# Удаление локальных веток, которые уже смержены
git branch --merged | grep -v '\*\|main\|master' | xargs -n 1 git branch -d
```

---

## 📈 Git Reflog: журнал изменений HEAD

```bash
git reflog
```

Показывает все изменения HEAD, даже после reset или rebase.

### Восстановление "потерянных" коммитов:
```bash
# Найти нужный коммит в reflog
git reflog

# Восстановить
git checkout HEAD@{2}
git branch recovery-branch  # создать ветку для сохранения
```

---

## 🎯 Git Worktree: несколько рабочих директорий

```bash
# Создать дополнительную рабочую директорию
git worktree add ../project-feature feature-branch

# Посмотреть все worktree
git worktree list

# Удалить worktree
git worktree remove ../project-feature
```

### Полезно когда:
- Нужно работать с несколькими ветками одновременно
- Тестировать разные версии параллельно
- Не хочется делать stash при переключении веток

---

## 📋 Git Notes: заметки к коммитам

```bash
# Добавить заметку к коммиту
git notes add -m "Важное замечание" abc123

# Показать заметки
git log --show-notes

# Редактировать заметку
git notes edit abc123

# Удалить заметку
git notes remove abc123

# Отправить заметки на сервер
git push origin refs/notes/*
```

---

## 🛡️ Git Hooks: автоматизация процессов

Скрипты, которые выполняются при определённых событиях Git.

### Расположение: `.git/hooks/`

### Популярные хуки:
- **pre-commit** — перед коммитом
- **commit-msg** — проверка сообщения коммита  
- **pre-push** — перед отправкой на сервер
- **post-merge** — после слияния

### Пример pre-commit хука:
```bash
#!/bin/sh
# Запуск тестов перед коммитом
npm test
if [ $? -ne 0 ]; then
    echo "Тесты не прошли, коммит отменён"
    exit 1
fi
```

---

## 📊 Git Statistics: статистика репозитория

### Количество коммитов по авторам:
```bash
git shortlog -sn
```

### Статистика по файлам:
```bash
git log --stat
git log --numstat
```

### Активность по времени:
```bash
git log --pretty=format:"%ai" | cut -d' ' -f1 | sort | uniq -c
```

---

## 🔍 Git Grep: поиск в истории

```bash
# Поиск текста в файлах
git grep "function"

# Поиск в конкретном коммите
git grep "function" HEAD~5

# Поиск с номерами строк
git grep -n "function"

# Поиск в истории коммитов
git log -S "function" --source --all
```

---

## 💡 Полезные трюки

### Временно игнорировать изменения в файле:
```bash
git update-index --skip-worktree file.txt
git update-index --no-skip-worktree file.txt  # отменить
```

### Показать изменения между ветками:
```bash
git diff main..feature
git diff --name-only main..feature  # только имена файлов
```

### Найти общего предка веток:
```bash
git merge-base main feature
```

### Экспортировать патчи:
```bash
git format-patch HEAD~3  # создать 3 patch файла
git am *.patch          # применить патчи
```

---

## 📘 Команды из темы

| Команда                          | Назначение                                        |
|----------------------------------|---------------------------------------------------|
| `git blame <file>`               | Показать, кто изменял каждую строку файла         |
| `git bisect`                     | Бинарный поиск проблемного коммита                |
| `git filter-branch`              | Массовое изменение истории коммитов               |
| `git rerere`                     | Запоминание решений конфликтов                    |
| `git submodule`                  | Управление внешними репозиториями                 |
| `git reflog`                     | Журнал всех изменений HEAD                        |
| `git worktree`                   | Создание дополнительных рабочих директорий        |
| `git notes`                      | Добавление заметок к коммитам                     |
| `git grep`                       | Поиск текста в файлах и истории                   |

---

## ⚠️ Важные предупреждения

- **git filter-branch** может полностью переписать историю
- **git bisect** требует хороших тестов для автоматизации
- **git submodule** усложняет работу с репозиторием
- **git hooks** могут замедлить операции Git
- Всегда делайте backup перед экспериментами с историей

---

## 🧠 Полезно знать

- Изучайте команды постепенно, по мере необходимости
- Многие "продвинутые" команды имеют простые альтернативы
- Документация Git очень подробная: `git help <command>`
- В сложных ситуациях лучше спросить у опытных коллег
- Большинство проблем решаются базовыми командами из основного курса