# CI/CD Journey — Foundation

## Цель
Научиться CI/CD как системный инженер (процесс, качество, релизный флоу).

## Правила обучения
- Маленькие шаги
- Практика > теория
- Каждый шаг фиксирую в журнале
- Любая ошибка = материал для понимания

## Текущий статус
- Репозиторий создан
- Локально склонирован
- Структура папок готова

## Настройка Git и SSH

### Проблема
`git push` через CLI не работал.
Ошибка: Password authentication is not supported.

### Причина
Remote был настроен на HTTPS.
GitHub больше не поддерживает пароль для Git операций.
Требуется SSH или Personal Access Token.

### Решение
1. Проверил remote:
   git remote -v

2. Переключил на SSH:
   git remote set-url origin git remote set-url origin git@github.com:RostislavLivshits/ci-cd-journey.git

3. Добавил публичный ключ в GitHub:
   ~/.ssh/id_rsa.pub

4. Проверил соединение:
   ssh -T git@github.com

5. После этого git push заработал.

### Что я понял
- Git transport (https vs ssh) влияет на способ аутентификации.
- VS Code может скрывать проблемы, CLI показывает реальное состояние.
- SSH — профессиональный способ работы с Git.