---
title: Модульное тестирование
order: 40
---

## Что такое модульные тесты?

**Модульные тесты** (или unit-тесты) - это программы, созданные для запуска других программ (называемых **тестируемым кодом** (Code Under Test, CUT) или **продуктивным кодом** (Production Code)) с **конкретными** предварительными условиями и проверкой **ожидаемого поведения** CUT.

Модульные тесты обычно написаны на том же языке программирования что и код, проверяемый ими.

Каждый **unit-тест** должен быть небольшим и проверять ограниченный объем функциональности. Тест-кейсы (Test cases) часто объединяются в **Группы Тестов**(Test Groups) или **Наборы Тестов**(Test Suites). Существует огромное количество **фреймворков модульного тестирования**. Самые популярные из них следуют шаблону **xUnit**, представленному [Кентом Беком](http://c2.com/cgi/wiki?KentBeck "Kent Beck"). Например, JUnit для Java или CppUTest для C/C++.

Модульные тесты также должны быть быстрыми. Обычно предполагается, что **сотни тест-кейсов выполняются за несколько секунд**.

## Почему именно модульные тесты?

Предназначение модульных тестов не в поиске ошибок. Они являются **спецификацией** ожидаемого поведения тестируемого кода. Этот тестируемый код как раз реализует ожидаемое поведение. Поэтому unit-тесты и CUT используются для проверки корректности и защиты друг друга. Если кто-то модифицирует продуктивный код, и это изменяет первоначально заложенное поведение программы, то тест упадёт. Если ваш код покрыт адекватными unit-тестами, то вы можете его развивать, не боясь сломать текущий функционал. Майкл Физерс описывает **унаследованный код** (legacy code), как _код, непокрытый модульными тестами_.

<img src="/img/technical-excellence/unit_test.png" width="60%">

Предназначение модульного тестирования состоит в том, чтобы защитить уже реализованный функционал, нежели найти в нем дефекты. Это похоже на страховочный якорь, который используют скалолазы. Такие якоря защищают от того, чтобы не упасть ниже уже набранной высоты.

### Цель модульного теста

Цель модульного теста в том, чтобы

* Облегчать изменения
  * Он защищает поведение, определённое предыдущими разработчиками. Так что люди могут менять код, не нарушая существующую функциональность.
* Упрощать интеграцию
  * Модульный тест проверяет основные модули программы, функции и классы. Это гарантирует, что основные блоки функционируют, как ожидалось. Когда эти блоки объединены вместе, мы можем отделить интеграционные проблемы (проблемы связывания, the coupling problem) от внутренних проблем блока (проблем зацепления, the cohesion problems).
* Документировать
  * Хорошо написанный модульный тест может использоваться, как документация для описания функциональности тестируемого кода. Unit-тесты содержат информацию, которую вы обычно не сможете найти в тестируемом коде, например, цель, которую преследовал разработчик, написавший код, и как он ожидал, как его код будут использовать. Модульное тестирование как документация, в отличие от другой традиционной документации, не "лжёт". Потому что, если он лжёт, тест не пройдёт. И это означает, что либо тест, либо код неверен.
* Быть инструментом проектирования
  * Модульное тестирование также является важным инструментом проектирования. Модульное тестирование требует тестируемости для понимания кода. Простота тестирования обычно означает простоту использования. Таким образом, модульное тестирование может быть использовано для того, чтобы убедиться, что проект имеет смысл с точки зрения использования, а не только с точки зрения реализации. Тестируемый код требует лучшей модульности и меньшего количества зависимостей. Так что модульный тест может легко взять небольшую часть тестируемого кода ("модуль", unit), не заботясь о подавляющем количестве зависимостей. Таким образом, модульное тестирование может быть использовано, чтобы убедиться, что спроектированный продукт имеет "высокую степень зацепления и низкую степень связанности" (high cohesion, low coupling).

### Почему именно уровень модулей?

"Да, важно использовать автоматические тесты для защиты текущей функциональности. Но почему это необходимо на уровне модулей?"

Вы можете спросить, почему бы нам просто не использовать тщательные автоматизированные функциональные или системные тесты для такой цели?

**Совокупная стоимость владения** (Total cost of ownership, TCO) -- Модульный тест находится на том же уровне абстракции системы, что и основной код. Это просто какой-то код, использующий другой код. Он не должен работать в той же среде, что и production-код. Для компилируемых языков программирования даже не нужно использовать тот же компилятор, что и для продуктивной среды. Стоимость создания и запуска unit-теста очень низкая. При правильной разработке стоимость обслуживания таких тестов также очень низкая. Вы можете не получить такой же уровень уверенности в одном успешном модульном тесте, как в функциональном тесте. Вам понадобится много небольших тест-кейсов, чтобы получить примерно сравнимый уровень доверия. Но стоимость владения небольшими модульными тестами все ещё намного ниже, чем владение несколькими функциональными тестами.

Если кодовая база продукта не содержала каких-либо модульных тестов в течение последних 2 лет, то потребуется дополнительные расходы на внедрение модульного тестирования в таком коде. Стоимость в основном состоит из двух источников:

1. Стоимость внедрения тестового фреймворка в проекте. Это относительно просто для динамических языков программирования, таких как Python, Ruby или Javascript. Обычно это также тривиально для проектов на Java и C#. Это может быть сильно сложнее для проекта на C/C++. Независимо от того, легко это или трудно, это всего лишь разовые инвестиции.
2. Существующая кодовая база не готова для тестирования. Код был разработан без возможности его тестирования. Применение модульного тестирования в таком коде часто влечёт за собой улучшение существующего дизайна системы. Это не только увеличивает стоимость создания каждого теста, но также может привести к появлению новых ошибок. Таким образом, добавление модульного теста к существующей кодовой базе должно сочетаться с другими мероприятиям, которые требуют изменений в тестируемом коде, что отличается от ситуации, когда вам необходимо изменить этот фрагмент кода независимо.

**Внутреннее vs. Внешнее качество** - Высокоуровневые автоматические тесты, такие как функциональные и системный тесты, проверяют внешнее качество программного обеспечения. Внешнее качество показывает, насколько хорошо программное обеспечение работает в соответствии с требованиями. Модульный тест не так эффективен, как функциональный тест для защиты внешнего качества. С другой стороны, модульное тестирование обеспечивает внутреннее качество программного обеспечения. Внутреннее качество здесь означает тестируемость кода и то, насколько хорошо он защищён. Дизайн с возможностью  тестирования - это, в общем, хороший дизайн. Другие уровни автоматического тестирования не могут служить этой цели также хорошо, как unit-тестирование.

**Качество обратной связи** - Когда вы прошли функциональный тест, вы можете быть уверены в функциональности, которую вы только что протестировали. Но когда вы обнаружили, что это не помогло, обычно вам нужно выполнить отладку, чтобы увидеть, что не так. Модульный тест может дать вам более точную информацию о том, что работает, а что нет.

Модульный тест находится на уровне абстракции исходного кода языка программирования. При запуске unit-теста всё должно происходить внутри ЦПУ и памяти. Каждый тест-кейс должен быть небольшим и выполняться очень быстро. Обычно, вы должны иметь возможность запускать сотни unit-тестов за несколько секунд. Включая компиляцию и время других подготовок, весь процесс запуска тестов должен занимать не более 1 минуты.

Модульные тесты должно быть повторяемы. Если ничего не поменялось в коде, результат работы модульного теста всегда один и тот же. 

Если модульный тест очень быстрый и повторяемый, разработчики могут запускать их так часто, как хотят. Например, каждые несколько минут. Таким образом модульный тест будет непрерывно обеспечивать качественную обратную связь программисту. Следовательно программист может двигаться вперёд с постоянным прогрессом и сосредоточиться на более важных вещах, а не тратить слишком много энергии на тривиальные вопросы.

<img src="/img/technical-excellence/test_levels.png" width="50%">

Разумная структура автоматических тестов должна выглядит как пирамида. На нижнем уровне большое количество модульных тестов. В середине чуть меньше интеграционных тест-кейсов. На вершине ещё меньше функциональных/системных тестов.

## Основные заблуждения, связанные с модульным тестированием

### Модульный тест не так важен, как продуктивный код

Это правда, что, в конце концов, продуктивный код составляет конечный продукт. Но большинство программных продуктов имеют эволюционный жизненный цикл. Код не является статичным. Он меняется со временем. Код без unit-теста не имеет необходимой защиты при изменении. Модульное тестирование также содержит важную информацию, которая не включена в продуктовый код.

Поэтому модульные тесты так же важны, как и тестируемый код. Они должны быть **в одном и том же SCM-репозитории**. Они должны следовать тем же стандартам разработки, что и production-код.

### Модульные тесты пишут инженеры по тестированию

Предназначение модульных тестов не в нахождение ошибок. Технически, они скорее _проверяют_, а не _тестируют_, что CUT ведёт себя так, как это предполагал написавший его разработчик. Поэтому будет разумным решением дать возможность одному программисту написать тест и код, который он проверяет.

Также рекомендуется объединять двух или более человек для совместного программирования. Они пишут unit-тесты и продуктивный код вместе. Существует много занимательных видов _парного программирования_. Больше информации об этом вы можете найти в разделе "Разработка через тестирование" (Test-Driven Development).

### Вы можете писать unit-тесты без изменения тестируемого кода

Часто это не так. Если код не обладает хорошими возможностями для тестирования, вы все равно технически можете написать для него unit-тест. Но это тест, написанный для такого кода, часто бывает довольно сложным в понимании и сопровождении. Поэтому, в нем нет особого смысла.

**Секрет модульного теста не в написании самого теста, а в написание CUT, пригодно для тестирования.** Мы хотим иметь в итоге пригодный для тестирования код и простой тест, что будет "абсолютной победой" (win-win). Мы не хотим иметь сложный в сопровождении код без возможности его тестирования, что было бы "полным провалом" (lose-lose). 

### Я могу потом дописать модульные тесты

Что ж, попробуйте попросить скалолаза зацепить страховочный крюк позже. 

<img src="/img/technical-excellence/unit_test.png" width="40%">

## Хорошие шаблоны для модульных тестов

### Отсутствие новостей - уже хорошая новость

Если тест проходит, он должно просто напечатать "OK" (и, возможно, несколько точек, чтобы показать прогресс). И никакой другой информации.

<img src="/img/technical-excellence/unit_test_success.png" width="500px">

"Правило большого пальца" (эмпирическая закономерность,  rule of thumb)

> Вмешательства человека не должно требоваться для подготовки, запуска тестов или проверки их результатов.

И когда он падает, он должен предоставить точную информацию об этом. Цель состоит в сокращении времени, которое вы тратите на отладке упавших тестов.
<img src="/img/technical-excellence/unit_test_fail.png" width="342px">

### Шаблон Arrange, Act, Assert

"**AAA**" - хороший шаблон для написания unit-тестов: **Arrange**, **Act** and **Assert**. (входные данные, действие, ожидаемый результат)

Если вы можете проследить использование такого подхода в каждом вашем тест-кейсе, то ваши тесты должны бать простыми для понимания, конкретными и вызывающими доверие. Следовательно, каждый тест-кейс должен содержать только один AAA-набор. Тест-кейс не должен быть слишком большим (больше 10 строк кода), если он следует шаблону ААА.

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

### Шаблон в стиле "Разработки через поведение" (Behaviour Driven Development, BDD style)

Будучи похожим на **AAA** паттерн, подход BDD использует три других ключевых слова для описания каждого тест-кейса: **Given**, **When** and **Then**. (Вы также можете использовать **And** в качестве ключевого слова.) На русском  **Дано**, **Когда**, **Тогда**, **И** соответственно.

    Given The Text Wrapper's Width Defined As 10
    And Using '-' As Word Connector
    When The Wrapper Wrap Text Length is Less Than 10
    Then The Text Should Not Be Wrapped
    
Как вы видите, "given-when-then" подход почти аналогичен "arrange-act-assert" подходу. Они оба просто определяют переход из одного состояния в другое в теории Конечного Автомата (Finite State Machine, FSM). Более подробную информацию вы можете найти в [статье "Дяди Боба" (Uncle Bob)](https://sites.google.com/site/unclebobconsultingllc/the-truth-about-bdd). Но между этими подходами есть ряд отличий:

* BDD смотрит на модуль как-бы "извне", т.е фокусируется на его поведении
* Используя BDD, вы должны определить **язык предметной области** (domain specific language, DSL) при написании ваших спецификаций. Из-за этого, скорее всего вам потребуется использовать другой фреймворк. Например, для языка Python это [behave](http://pythonhosted.org/behave/).

### Золотое правило модульного тестирования

В общем, хорошие правило для каждого модульного тест-кейса звучит так:

> **Каждый модульный тест-кейс должен быть сильно ограничен с точки зрения масштабов проверяемого участка системы**

Поэтому

* Когда тест падает, отладка не требуется для локализации проблемы.
* Тесты стабильны, потому что имеют мало зависимостей.
* Минимум дублирования, удобнее в сопровождении.

Нет секрета в там, как написать хороший модульный тест. Для того чтобы это сделать, вы должны создавать "легко тестируемый" дизайн ваших систем.

Перевод статьи осуществлён [Кротовым Артёмом](https://www.facebook.com/artem.v.krotov).