# Flutter CI Basics

Этот проект используется для изучения базовых принципов CI/CD на примере Flutter.

## Что было реализовано

### 1. Git workflow

Используется стандартный flow:

feature branch → Pull Request → merge в main.

Новая разработка происходит в отдельной ветке:
```bash
git checkout -b feature/some-feature
```


После завершения создаётся Pull Request.

---

### 2. Branch protection

Для ветки `main` включена защита:

- merge только через Pull Request
- required status check: `test`

Это означает:

PR нельзя мержить, если CI не прошёл.

---

### 3. CI pipeline

Workflow:
```bash
.github/workflows/flutter_ci.yml
```


CI запускается на:

- push в main
- pull request в main

Pipeline выполняет:

1. Checkout репозитория
2. Setup Flutter SDK
3. Cache pub packages
4. flutter pub get
5. flutter analyze
6. flutter test

---

### 4. Static analysis

Используется:
```bash
flutter analyze
```


Правила линтера подключены через:
```bash
analysis_options.yaml
```


Включён стандартный набор:
```bash
include: package:flutter_lints/flutter.yaml
```


Это помогает поддерживать единый стиль и качество кода.

---

### 5. Unit tests

Тесты запускаются через:
```bash
flutter test
```


CI падает если хотя бы один тест не проходит.

---

### 6. Cache

Используется cache для:
```bash
~/.pub-cache
```


Это ускоряет CI, потому что зависимости не скачиваются каждый раз.

---

### 7. Concurrency

Добавлена настройка:
```bash
concurrency:
group: ci-${{ github.ref }}
cancel-in-progress: true
```


Если выполняется несколько CI для одной ветки, старые автоматически отменяются.

Это экономит CI минуты.

---

### 8. Manual release workflow

Отдельный workflow:
```bash
.github/workflows/manual_release.yml
```


Запускается вручную через:
```bash
workflow_dispatch
```


Он выполняет:

- flutter pub get
- flutter build apk --release
- upload APK artifact

Это отделяет процесс CI (проверка кода) от release (сборка приложения).

---

## Что я понял

CI нужен для автоматической проверки качества кода перед merge.

CI должен быть:

- быстрым
- дешёвым
- запускаться часто

Release pipeline может быть:

- тяжелее
- запускаться вручную
- создавать build artifacts.

---

## Итог

В проекте реализован базовый production-style CI pipeline для Flutter.