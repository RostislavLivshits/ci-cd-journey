# Go CI Pipeline

Этот документ описывает CI pipeline, реализованный для Go-проекта.

## Цель

Автоматически проверять качество кода при каждом push и pull request.

Pipeline должен проверять:

* форматирование
* линтинг
* статический анализ
* тесты
* покрытие
* корректность сборки

---

# Структура CI

Файл pipeline:

```
.github/workflows/go_ci.yml
```

Pipeline запускается на:

```
push → main
pull_request → main
```

---

# 1. Checkout

Скачивание кода репозитория.

```yaml
uses: actions/checkout@v4
```

---

# 2. Setup Go

Устанавливается Go и включается cache.

```yaml
uses: actions/setup-go@v5
with:
  go-version-file: go.mod
  cache: true
```

### Cache

Кэшируются:

```
~/go/pkg/mod
~/.cache/go-build
```

Это ускоряет:

```
go vet
go test
go build
```

---

# 3. golangci-lint

Основной линтер Go.

```yaml
uses: golangci/golangci-lint-action@v6
with:
  version: v1.59
  args: --timeout 5m
```

golangci-lint объединяет более 30 линтеров:

* staticcheck
* errcheck
* ineffassign
* unused
* gosimple
* govet

---

# 4. Formatting gate

Проверяется стандартный Go-формат.

```bash
gofmt -l .
```

Если файл не соответствует стандарту — CI падает.

Исправление:

```
gofmt -w .
```

---

# 5. Static analysis

Дополнительная проверка:

```
go vet ./...
```

Ищет потенциальные ошибки.

---

# 6. Tests

Запускаются тесты:

```
go test ./...
```

---

# 7. Coverage

Показывается покрытие тестами:

```
go test -cover ./...
```

---

# Локальные инструменты разработки

## Pre-commit hook

Перед commit выполняются проверки:

```
gofmt
go vet
go test
```

Если проверки не проходят — commit блокируется.

---

## Makefile

Для удобства разработчиков добавлены команды:

```
make format
make vet
make test
make lint
make ci
```

Команда:

```
make ci
```

запускает полный набор проверок.

---

# Dev workflow

Типичный цикл разработки:

```
write code
↓
make ci
↓
git commit
↓
pre-commit hook
↓
push
↓
GitHub CI
↓
merge
```

---

# Результат

Реализован production-style Go CI pipeline со следующими компонентами:

* formatting gate
* linting
* static analysis
* automated tests
* coverage
* caching
* pre-commit checks
* Makefile workflow
