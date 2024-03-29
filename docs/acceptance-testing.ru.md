# Приёмочное Тестирование

## Не путайте приёмочное и пользовательское приёмочное тестирование

В идеальной ситуации, приёмочное тестирование (acceptance test) и пользовательское приёмочное тестирование (user-acceptance test, UAT) это одно и тоже, но... Литература по гибкой разработке использует термин “приёмочное тестирование” там, где мы используем термин “пользовательское тестирование” (customer-facing tests). Однако, в традиционной разработке под “приёмочным тестированием” зачастую подразумевается “пользовательское приёмочное тестирование,” что на самом деле может быть разными вещами. Избегайте такого недопонимания.

![_](/img/test_automation/acceptance_vs_uat.png)

*UAT является подмножеством приёмочного тестирования*

Схема выше объясняет взаимосвязь между этими двумя видами тестирования посредством диаграммы. Пользовательское приёмочное тестирование (UAT) является частью приёмочного тестирования в гибкой разработке ПО. Но приёмочные тесты могут также включать другие виды тестирования, помимо пользовательских приёмочных тестов, например, традиционные функциональные или системные тесты, созданные командой.

В идеальном случае все приёмочные тесты, включая UAT, выполняются в рамках итерации. Однако, включение UAT в итерацию может быть затруднено тем, что это требует активного участия конечных пользователей, но не все клиенты готовы к такому. В таких случаях, UAT исключается из Критериев Готовности до тех пор, пока продуктовая группа не выстроит взаимоотношения с клиентами, и тогда их Критерии Готовности смогут быть расширены.

## Показывайте тесты на Обзоре Спринта

На Обзоре Спринта команды демонстрируют видимый прогресс Владельцу Продукта, показывая результаты итерации.

Мы работали с некоторыми продуктовыми группами, которые определяли, как они будут показывать инкремент, ещё на Планировании Спринта. Команда тратила чрезмерное количество времени на подготовку к демонстрации. Это чистые потери.

Во время Планирования Спринта более подходящей альтернативой будет определение примеров сценариев, которые должны успешно выполняться, и демонстрация прогресса с использованием этих примеров на Обзоре Спринта.

### Используйте разработку через приёмочное тестирование

[Разработка через приёмочное тестирование (acceptance test-driven development, A-TDD) или Спецификация на основе примеров (Specification by Example)](specification-by-example.md) это подход коллективного прояснения требований, в котором примеры и автоматизируемые тесты используются для уточнения требований — создания "исполняемых" спецификаций. Они совместно создаются командой, Владельцем Продукта и другими заинтересованными лицами, во время специализированных сессий совместной работы по прояснению требований.
