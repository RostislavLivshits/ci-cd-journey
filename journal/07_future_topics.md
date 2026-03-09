# Future Topics

Этот документ фиксирует темы, которые будут изучаться позже после базового освоения CI.

---

# 1. Continuous Deployment (CD)

## Что это

Автоматическая доставка приложения после успешного CI.

Типичный pipeline:

PR → CI → merge → build → deploy

---

## Go deployment

Возможный сценарий:

merge → build binary / docker image → deploy to staging server → restart service

Что нужно изучить:

* Docker
* Docker registry
* VPS deployment
* systemd / container runtime
* health checks

---

## Flutter delivery

CI может автоматически:

* собрать APK / AAB
* собрать iOS build
* загрузить в beta distribution

Возможные инструменты:

* Firebase App Distribution
* Google Play Internal Testing
* TestFlight

---

# 2. Docker

Docker позволяет:

* изолировать окружение
* создавать reproducible builds
* упрощать деплой

Типичный backend pipeline:

build → docker image → push → deploy container

---

# 3. Artifact management

CI может сохранять:

* build artifacts
* coverage reports
* binaries

Примеры:

* APK
* Go binary
* coverage report

---

# 4. Advanced linting

Настройка:

.golangci.yml

Позволяет:

* включать / отключать линтеры
* ограничивать complexity
* контролировать качество кода

---

# 5. Advanced CI optimization

Оптимизация CI:

* smarter caching
* parallel jobs
* matrix builds
* selective pipeline runs

---

# 6. Secrets management

CI требует безопасного хранения:

* API keys
* deployment tokens
* signing keys

Инструменты:

GitHub Secrets
Vault
Environment variables

---

# 7. Infrastructure as Code

Описывает инфраструктуру кодом.

Инструменты:

* Terraform
* Pulumi
* Ansible

---

# Итог

Текущий этап обучения:

✔ Git
✔ GitHub workflow
✔ CI pipeline
✔ lint
✔ tests
✔ caching
✔ Makefile
✔ pre-commit hooks

Следующие этапы:

* Docker
* CD
* deployment
* secrets
* infrastructure


---

# 8. Monorepo Architecture

Некоторые проекты используют **monorepo**, где несколько частей системы находятся в одном репозитории.

Пример структуры:

```
repo/
 ├ backend/        (Go service)
 ├ mobile/         (Flutter app)
 ├ web/            (optional frontend)
 ├ .github/
 └ Makefile
```

Такой подход позволяет:

* управлять backend и mobile в одном месте
* синхронизировать изменения API
* упростить CI/CD

---

# 9. Unified Makefile

В monorepo часто используется **единый Makefile**, который становится интерфейсом разработки.

Пример:

```
.PHONY: help backend-test mobile-test ci

backend-test:
	cd backend && make test

mobile-test:
	cd mobile && flutter test

backend-lint:
	cd backend && golangci-lint run

mobile-analyze:
	cd mobile && flutter analyze

ci: backend-lint backend-test mobile-analyze mobile-test
```

Теперь разработчик может запустить:

```
make ci
```

И будут выполнены проверки:

* Go lint
* Go tests
* Flutter analyze
* Flutter tests

---

# 10. Unified Developer Workflow

Единый Makefile позволяет использовать **одинаковые команды**:

```
локально
↓
make ci

CI pipeline
↓
make ci
```

Это предотвращает проблему:

```
локально работает
CI падает
```

Потому что используется один и тот же набор команд.

---

# 11. Simplified CI

CI pipeline в этом случае становится очень простым:

```
- name: Run CI
  run: make ci
```

Вся логика проверок находится в Makefile.

---

# Когда используется такой подход

Unified Makefile чаще встречается в проектах, где есть:

* backend (Go / Node / Python)
* mobile (Flutter / React Native)
* web frontend
* shared libraries

Это делает репозиторий удобнее для разработчиков.

---

# Роль Makefile

В такой архитектуре Makefile становится:

**developer interface**

к проекту.

Он описывает стандартные команды:

```
make build
make test
make lint
make ci
make deploy
```

и позволяет запускать их одинаково:

* локально
* в CI
* в deployment pipeline
