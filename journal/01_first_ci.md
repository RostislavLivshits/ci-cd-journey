# First CI Pipeline

## Добавить workflow GitHub Actions
Находясь в папке проекта ci_demo, создай папки и файл:
```bash
mkdir -p .github/workflows
touch .github/workflows/flutter_ci.yml
```

Открой файл в редакторе (можно VS Code):
```bash
code .
```

И вставь в .github/workflows/flutter_ci.yml:
```YAML
name: Flutter CI

on:
  push:
    branches: [ "main" ]
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Flutter
        uses: subosito/flutter-action@v2
        with:
          channel: "stable"

      - name: Install dependencies
        run: flutter pub get

      - name: Analyze
        run: flutter analyze

      - name: Run tests
        run: flutter test
        
      - name: Build APK (release)
        run: flutter build apk --release

      - name: Upload APK artifact
        uses: actions/upload-artifact@v4
        with:
          name: app-release-apk
          path: build/app/outputs/flutter-apk/app-release.apk
```

## Commit + push (через CLI)
```bash
git status
git add .github/workflows/flutter_ci.yml
git commit -m "Add Flutter CI workflow"
git push
```
### Проверить результат
Открой GitHub репозиторий → вкладка Actions.

Ты должен увидеть workflow Flutter CI и статус:

✅ зелёный — отлично

❌ красный — тоже отлично (будем читать логи как инженеры)


## Что было сделано
- Создан Flutter проект `ci_demo`
- Настроен GitHub Actions workflow
- Pipeline запускается на push и pull_request
- Запускаются:
  - flutter pub get
  - flutter analyze
  - flutter test

## Намеренно сломал тест
Изменил:
expect(find.text('0'), findsOneWidget);

на:

expect(find.text('1'), findsOneWidget);

## Что произошло
CI упал.
Ошибка:
Expected: exactly one matching candidate
Actual: Found 0 widgets with text "1"

## Почему CI упал
Не из-за сборки.
Не из-за Flutter.
А из-за падения теста.

`flutter test` вернул exit code 1 → job стал красным.

## Что я понял
- CI — это автоматизированный запуск команд.
- Если команда возвращает exit code != 0, job падает.
- Падение теста = красный CI.
- Логи CI читаются сверху вниз, важна первая ошибка.

## Build artifact (APK) in CI

### Зачем
Чтобы CI проверял, что release build реально собирается, а не только что тесты проходят.

### Что добавил в workflow
- flutter build apk --release
- upload-artifact: build/app/outputs/flutter-apk/app-release.apk

### Результат
После каждого run можно скачать APK из GitHub Actions → Artifacts.