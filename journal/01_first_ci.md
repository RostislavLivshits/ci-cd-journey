# First CI Pipeline

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