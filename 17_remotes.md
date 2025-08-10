# 🌐 Git Remotes: работа с удалёнными репозиториями

Remotes (удалённые репозитории) — это ссылки на репозитории, расположенные на серверах (GitHub, GitLab и др.).  
Они позволяют синхронизировать локальную работу с командой.

---

## 🔗 Добавление удалённого репозитория

```bash
git remote add <name> <url>
```

### Пример:

```bash
git remote add origin git@github.com:user/repo.git
```

Добавляет удалённый репозиторий с именем `origin`.

---

## 👀 Просмотр удалённых репозиториев

```bash
git remote -v
```

Показывает список всех удалённых репозиториев с URL:

```
origin  git@github.com:user/repo.git (fetch)
origin  git@github.com:user/repo.git (push)
```

### Просмотр подробной информации:

```bash
git remote show <name>
```

Показывает детальную информацию об удалённом репозитории.

---

## 🗑️ Удаление удалённого репозитория

```bash
git remote remove origin
```

Удаляет ссылку на удалённый репозиторий с именем `origin`.

---

## 🔄 Синхронизация с удалёнными репозиториями

### Отправка изменений:

```bash
git push
git push origin master
git push origin feature
```

### Получение изменений:

```bash
git fetch
git fetch origin
```

Загружает изменения, но не сливает их автоматически.

---

## 📊 Схема работы с remotes

```
Local Repository          Remote Repository
┌─────────────────┐      ┌─────────────────┐
│   local master  │────► │  origin master  │  git push
│                 │ ◄────│                 │  git fetch
└─────────────────┘      └─────────────────┘

┌─────────────────┐      ┌─────────────────┐
│  local feature  │────► │ origin feature  │  git push
│                 │ ◄────│                 │  git fetch  
└─────────────────┘      └─────────────────┘
```

---

## 🛠️ Дополнительные команды

### Переименование remote:

```bash
git remote rename old_name new_name
```

### Изменение URL remote:

```bash
git remote set-url origin git@github.com:user/new-repo.git
```

### Просмотр всех remote веток:

```bash
git branch -r
```

---

## 🎯 Типичные имена remote

| Имя        | Назначение                                      |
|------------|-------------------------------------------------|
| **origin** | Основной удалённый репозиторий (по умолчанию)  |
| **upstream** | Оригинальный репозиторий (при форке)         |
| **fork**   | Ваш форк чужого репозитория                     |

---

## 📋 Практический пример

```bash
# 1. Клонирование создаёт remote автоматически
git clone git@github.com:user/repo.git
# Создаётся remote с именем "origin"

# 2. Просмотр существующих remote
git remote -v

# 3. Добавление дополнительного remote
git remote add upstream git@github.com:original/repo.git

# 4. Работа с ветками
git push origin feature-branch
git fetch upstream

# 5. Удаление remote при необходимости
git remote remove upstream
```

---

## 📘 Команды из темы

| Команда                          | Назначение                                        |
|----------------------------------|---------------------------------------------------|
| `git remote add <name> <url>`    | Добавить новый удалённый репозиторий              |
| `git remote -v`                  | Показать список удалённых репозиториев            |
| `git remote show <name>`         | Показать детальную информацию о remote            |
| `git remote remove <name>`       | Удалить ссылку на удалённый репозиторий           |
| `git push origin <branch>`       | Отправить ветку в удалённый репозиторий           |
| `git fetch origin`               | Получить изменения из удалённого репозитория      |

---

## 💡 Полезно знать

- `origin` — стандартное имя для основного remote
- При `git clone` remote добавляется автоматически
- Можно работать с несколькими remote одновременно
- `git fetch` безопаснее `git pull` (не делает автоматический merge)
- Remote ветки отображаются как `origin/master`, `origin/feature`
- Удаление remote не влияет на локальные ветки