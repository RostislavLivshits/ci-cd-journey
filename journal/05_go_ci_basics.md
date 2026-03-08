# Go CI Basics

Этот проект используется для изучения базовых принципов CI/CD на примере Go.

## Что было реализовано

### 1. Git workflow

Используется стандартный flow:

feature branch → Pull Request → merge в main

---

### 2. CI workflow

Файл:

`.github/workflows/go_ci.yml`

CI запускается на:
- push в main
- pull request в main

---

### 3. Setup Go

В CI используется:

`actions/setup-go@v5`

Go версия берётся из workflow.

---

### 4. Formatting check

Используется:

`gofmt -l .`

Если есть неотформатированные файлы, CI падает.

Для исправления используется:

`gofmt -w .`

---

### 5. Static checks

Используется:

`go vet ./...`

Проверяет подозрительные конструкции и потенциальные ошибки.

---

### 6. Tests

Используется:

`go test -cover ./...`

Это:
- запускает все тесты
- показывает coverage в логах

---

### 7. Concurrency

Используется отмена старых CI запусков для одной и той же ветки.

Это уменьшает расход CI минут.

---

## Что я понял

- Go CI обычно проще, чем Flutter CI
- В Go очень важен стандартный формат кода
- `gofmt` — часть культуры Go
- `go vet` и `go test` — базовый production-level набор
- Coverage в Go добавляется очень просто через `-cover`

---

## Итог

В проекте реализован базовый production-style CI pipeline для Go.