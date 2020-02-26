---
title: Модульное тестирование
order: 30
---

## Что такое модульные тесты?

**Модульные тесты** (или unit-тесты) - это программы, созданные для запуска других программ (называемых **тестируемым кодом** (Code Under Test, CUT) или **продуктивным кодом** (Production Code)) с **конкретными** предварительными условиями и проверкой **ожидаемого поведения** CUT.

Модульные тесты обычно написаны на том же языке программирования что и код, проверяемый ими.

Каждый **unit-тест** должен быть небольшим и проверять ограниченный объем функциональности. Тест-кейсы (Test cases) часто объединяются в **Группы Тестов**(Test Groups) или **Наборы Тестов**(Test Suites). Существует огромное количество **фреймворков модульного тестирования**. Самые популярные из них реализуют шаблон **xUnit**, представленный [Кентом Беком](http://c2.com/cgi/wiki?KentBeck "Kent Beck"). Например, JUnit для Java или CppUTest для C/C++.

Модульные тесты также должны быть быстрыми. Обычно предполагается, что **сотни тест-кейсов выполняются за несколько секунд**.

## Почему именно модульные тесты?

Предназначение модульных тестов не в нахождение ошибок. Они являются **спецификацией** ожидаемого поведения тестируемого кода. Этот тестируемый код как раз реализует ожидаемое поведение. Поэтому unit-тесты и CUT используются для проверки корректности и защиты друг друга. Если кто-то модифицирует продуктивный код, и это изменяет первоначально заложенное поведение программы, то тест упадёт. Если ваш код покрыт адекватными unit-тестами, то вы можете его развивать, не боясь сломать текущий функционал. Майкл Физерс описывает **унаследованный код** (legacy code), как _код, непокрытый модульными тестами_.

<img src="/img/technical-excellence/unit_test.png" width="60%">

Предназначение модульного тестирования состоит в том, чтобы защитить уже реализованный функционал, нежели найти в нем дефекты. Это похоже на страховочный якорь, который используют скалолазы. Такие якоря защищают от того, чтобы не упасть ниже уже набранной высоты.

### Цель модульного теста

Цель модульного теста в том, чтобы

* Облегчать изменения
  * Он защищает поведение, определённое предыдущими разработчиками. Так что люди могут менять код, не нарушая существующую функциональность.
* Упрощать интеграцию
  * Модульный тест проверяет основные модули программы, функции и классы. Это гарантирует, что основные блоки функционируют, как ожидалось. Когда эти блоки объединены вместе, мы можем отделить интеграционные проблемы (проблемы связывания, the coupling problem) от внутренних проблем блока (проблемы зацепления, the cohesion problems).
* Документировать
  * Хорошо написанный модульный тест может использоваться, как документация для описания функциональности тестируемого кода. Модульное тестирование содержит информацию, которую вы обычно не можете найти в тестируемом коде, например, цель, которую преследовал разработчик, написавший код, и как он ожидал, как его код будут использовать. Модульное тестирование как документация, в отличие от другой традиционной документации, не "лжёт". Потому что, если он лжёт, тест не пройдёт. И это означает, что либо тест, либо код неверен.
* Быть инструментом проектирования
  * Модульное тестирование также является важным инструментом проектирования. Модульное тестирование требует тестируемости понимания кода. Простота тестирования обычно означает простоту использования. Таким образом, модульное тестирование может быть использовано для того, чтобы убедиться, что проект имеет смысл с точки зрения использования, а не только с точки зрения реализации. Тестируемый код требует лучшей модульности и меньшего количества зависимостей. Так что модульный тест может легко взять небольшую часть тестируемого кода ("модуль", unit), не заботясь о подавляющем количестве зависимостей. Таким образом, модульное тестирование может быть использовано, чтобы убедиться, что спроектированный продукт имеет "высокая степень зацепления, низкая степень связанности" (high cohesion, low coupling).

### Почему именно уровень модулей?

"Да, важно использовать автоматические тесты для защиты текущей функциональности. Но почему это необходимо на уровне модулей?"

Вы можете спросить, почему бы нам просто не использовать тщательные автоматизированные функциональные или системные тесты для такой цели?

**Совокупная стоимость владения** (Total cost of ownership, TCO) -- Модульный тест находится на том же уровне абстракции языка программирования, что и основной код . Это просто какой-то код, использующий другой код. Он не должен работать в той же среде, что и production код. Для компилируемых языков программирования даже не нужно использовать тот же компилятор, что и для продуктивной среды. Стоимость создания и запуска unit-теста очень низкая. При правильной разработке стоимость обслуживания таких тестов также очень низкая. Вы можете не получить такой же уровень уверенности в одном успешном модульном тесте, как в функциональном тесте. Вам понадобится много небольших тест-кейсов, чтобы получить примерно сравнимый уровень доверия. Но стоимость владения небольшими модульными тестами все ещё намного ниже, чем владение несколькими функциональными тестами.

Если кодовая база ПО не содержала каких-либо модульных тестов в течение последних 2 лет, то это будет дополнительная плата за внедрение модульного тестирования в таком коде. Стоимость в основном из двух источников:

1. Стоимость внедрения тестового фреймворка в проекте. Это относительно просто для динамических языков программирования, таких как Python, Ruby или Javascript. Обычно это также тривиально для проектов на Java и C#. Это может быть сильно сложнее для проекта на C/C++. Независимо от того, легко это или трудно, это всего лишь разовые инвестиции.

2. Существующая кодовая база не готова для тестирования. Код был разработан без возможности его тестирования. Применение модульного тестирования в таком коде часто влечёт за собой улучшение существующего дизайна системы. Это не только увеличивает стоимость создания теста, но также может привести к появлению новых ошибок. Таким образом, добавление модульного теста к существующей кодовой базе должно сочетаться с другими мероприятиям, которые требуют изменений в тестируемом коде, что отличается от ситуации, когда вам необходимо изменить этот фрагмент кода независимо.

**Внутреннее vs. Внешнее качество** - Высокоуровневые автоматические тесты, такие как функциональные и системный тесты, проверяют внешнее качество программного обеспечения. Внешнее качество показывает, насколько хорошо программное обеспечение работает в соответствии с требованиями. Модульный тест не так эффективен, как функциональный тест для защиты внешнего качества. С другой стороны, модульное тестирование обеспечивает внутреннее качество программного обеспечения. Внутреннее качество здесь означает тестируемость кода и то, насколько хорошо он защищён. Дизайн с возможностью  тестирования - это, в общем, хороший дизайн. Другие уровни автоматического тестирования не могут служить этой цели также хорошо, как unit-тестирование.

**Качество обратной связи** - Когда вы прошли функциональный тест, вы можете быть уверены в функциональности, которую вы только что протестировали. Но когда вы обнаружили, что это не помогло, обычно вам нужно выполнить отладку, чтобы увидеть, что не так. Модульный тест может дать вам более точную информацию о том, что работает, а что нет.

Unit test is on the abstraction level of the programming language. When running unit test, everything should happen just within the CPU and memory. And each test case should be small. Therefore, it should run very fast. Typically, you should be able to run hundreds of unit tests within a few seconds. Including the compiling or other preparation time, the whole process of running unit test should take less than 1 minute.

Unit test should also be repeatable. If nothing changes, unit test runs should always return the same result.

If the unit test is very fast and repeatable, programmers can run it as often as they want, e.g. every a few minutes. The unit test will continuously provide quality feedback to the programmer. So that the programmer can go with a steady progress and focus on more important things rather than spending too much energy on trivial issues.

<img src="/img/technical-excellence/test_levels.png" width="50%">

A reasonable automated test structure should be like a pyramid. At the bottom are a lot of unit test cases. In the middle are much fewer integration level test cases. On the top, there are even fewer functional/system level tests.

## Common Misconceptions of Unit Test

### Unit test is not as important as the production code

It is true that in the end, it's production code that makes the product. But most software products have evolutionary life cycles. The code is not static. It changes over time. Code without unit test does not have the necessary protection when being changed. Unit test also contains important information that is not included in the production code.

So unit test is just as important as the production code. They should be **in the same SCM repository**. They should follow the same coding standard as the production code.

### Unit Test is done by testing engineers

The purpose of unit test is not for finding bugs. Technically, it _checks_ rather than _tests_ if the code under test has implemented the behaviour intended by the programmer who designed it. So the reasonable choice is just let the same programmer writes both the test and the code under test.

It's also encouraged to have two or more people pair up to do the programming together. They write the unit test and the code under test together. There are many fun ways of _pair-programming_. You may find more information in the Test-Driven Development section.

### You can write unit test without changing the code under test

This is often not true. If the code doesn't have good testability, you might still be able to write unit test for it technically. But the unit test written for non-testable code is usually very hard to maintain and understand. Therefore, it doesn't make much sense to have it.

**The secret of unit test is not about writing test, but writing testable code under test.** We want testable code and easy test, which is a win-win. We don't want non-testable code and hard-to-maintain code, which is a lose-lose.

### I can add unit test later

Well, try asking the rock climbers to set their anchors later.

<img src="/img/technical-excellence/unit_test.png" width="40%">

## Good Unit Test Patterns

### No news is good news

If the test passes, it should just print OK (and perhaps some dots to show the progress). No other information.

<img src="/img/technical-excellence/unit_test_success.png" width="500px">

Rule of thumb:

> No human intervention should be needed to get ready for the test, running the test cases or checking the result.

And when it fails, it should provide precise information. The goal is to limit the amount of time you spend on debugging when the test fails.
<img src="/img/technical-excellence/unit_test_fail.png" width="342px">

### Arrange, Act, Assert

A good pattern to follow in a unit test is "**AAA**": **Arrange**, **Act** and **Assert**. 

If you can easily find this pattern in each of your test cases, your tests should be easy to understand, and they should be fairly specific and to the point. One unit test case should test only one thing. Therefore, there should be only one set of AAA in one test case. A test case shouldn't be very long (longer than 10 lines of code) if it follows the AAA pattern.

<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="kn">import</span> <span class="nn">unittest</span>
<span class="k">class</span> <span class="nc">TestGroupForTextWrapping</span><span class="p">(</span><span class="n">unittest</span><span class="o">.</span><span class="n">TestCase</span><span class="p">):</span>
    
    <span class="k">def</span> <span class="nf">test_should_have_no_wrapping_when_string_length_is_5_and_line_width_is_10</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="c"># Arrange:  Arrange all necessary preconditions and inputs. </span>
        <span class="n">wrapper</span> <span class="o">=</span> <span class="n">TextWrapper</span><span class="p">(</span><span class="n">width</span><span class="o">=</span><span class="mi">10</span><span class="p">)</span>
        
        <span class="c"># Act:  Act on the object or method under test. </span>
        <span class="n">wrapped</span> <span class="o">=</span> <span class="n">wrapper</span><span class="o">.</span><span class="n">wrap</span><span class="p">(</span><span class="s">"a"</span> <span class="o">*</span> <span class="mi">5</span><span class="p">)</span>
        
        <span class="c"># Assert:  Assert that the expected results have occurred. </span>
        <span class="bp">self</span><span class="o">.</span><span class="n">assertEqual</span><span class="p">([</span><span class="s">"a"</span> <span class="o">*</span> <span class="mi">5</span><span class="p">],</span> <span class="n">wrapped</span><span class="p">)</span>
</pre></div>

</div>
</div>

### Behaviour Driven Development (BDD) Style

Similar to the **AAA** pattern, the **BDD** style uses three other keywords to specify each test case: **Given**, **When** and **Then**. (You can also use **And** as another keyword.)

    Given The Text Wrapper's Width Defined As 10
    And Using '-' As Word Connector
    When The Wrapper Wrap Text Length is Less Than 10
    Then The Text Should Not Be Wrapped
    
As you can see, "given-when-then" maps to "arrange-act-assert" pretty well. They both simply define a state transition of a Finite State Machine (FSM). You can find more on this in the [Uncle Bob's article](https://sites.google.com/site/unclebobconsultingllc/the-truth-about-bdd). Some differences:

* BDD is more "outside-in", which means that it emphasises more the external behaviour
* With BDD, you need to define a **domain specific language** to write your test specifications. Because of this, usually you'll need a different framework. One example for Python is [behave](http://pythonhosted.org/behave/).

### The Golden Rule Of a Unit Test

In general, a good rule for unit test case is:

> **Each unit test case should be very limited in scope.**

So that:

* When the test fails, no debugging is needed to locate the problem.
* Tests are stable because dependencies are simple.
* Less duplication, easier to maintain.

There is no secret to write good unit test. In order to write good unit test, you need to create easy-to-test design.