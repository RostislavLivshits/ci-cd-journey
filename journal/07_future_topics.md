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
