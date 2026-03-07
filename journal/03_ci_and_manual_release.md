# CI and Manual Release Architecture

## Что построено

### 1. CI workflow
Автоматический workflow для Pull Request в `main`.

Он выполняет:
- flutter pub get
- flutter analyze
- flutter test --coverage

Дополнительно:
- используется cache для `~/.pub-cache`
- включен concurrency для отмены старых CI запусков
- coverage сохраняется как artifact (`coverage/lcov.info`)

### 2. Branch protection
Для ветки `main` включено:
- merge только через Pull Request
- required status check: `test`

Это означает, что PR нельзя мержить, если CI не зелёный.

### 3. Manual Release workflow
Отдельный workflow, который запускается вручную через `workflow_dispatch`.

Он выполняет:
- flutter pub get
- flutter build apk --release
- upload APK artifact

## Почему CI и Release разделены

CI должен быть:
- быстрым
- дешёвым
- частым

Release workflow:
- тяжёлый
- запускается редко
- нужен только когда реально требуется release APK

## Что я понял

- CI = проверка качества кода перед merge
- Release = создание артефакта для публикации
- Эти процессы лучше разделять
- Cache и concurrency уменьшают расход CI минут
- Coverage можно генерировать в CI и сохранять как artifact
- Manual release — хороший подход для solo-разработки