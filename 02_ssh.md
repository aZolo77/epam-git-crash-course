# 🔐 Работа с SSH-ключами

## Генерация ключа

```bash
ssh-keygen -t ed25519 -C "email@example.com"
```

> Если не поддерживается ed25519:

```bash
ssh-keygen -t rsa -b 4096 -C "email@example.com"
```

## Добавление ключа в GitHub

1. Копировать ключ:
```bash
cat ~/.ssh/id_ed25519.pub
```
2. Вставить в GitHub: **Settings → SSH and GPG keys → New SSH key**

## Проверка подключения

```bash
ssh -T git@github.com
```