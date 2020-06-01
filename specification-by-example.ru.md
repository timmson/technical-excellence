---
title: Specification by Example
order: 70
---

<div class="chapter_quote"><p>
Есть две бесконечные вещи: Вселенная и человеческая глупость. Впрочем, насчёт первой я не уверен.
<br/>
--Альберт Эйнштейн
</p></div>

Specification by Example (близкий по смыслу перевод "тесты как требования", но устоявшегося термина нет [прим. переводчика]) или разработка через приёмочное тестирование (A-TDD) - это подход к совместному выявлению требований путём создания примеров и автотестов. На основе них создаются исполняемые спецификации, которые уточняют изначальные требования. Такие спецификации создаются командами вместе с Владельцем Продукта и другими заинтересованными лицами на воркшопах сбору требований.

Заметка по терминологии: Мы будем использовать и A-TDD и Specification by Example.

A-TDD объединяет следующие основные идеи:

* тесты как требования, требования как тесты
* воркшопы по прояснению требований
* одновременное проектирование
* предотвращение вместо обнаружения

**Тесты как требования, требования как тесты** — В книге [Exploring Requirements: Quality before Design](http://www.amazon.com/Exploring-Requirements-Quality-Before-Design/dp/0932633137) её авторы Дональд Гаус and Джеральд Вайнберг исследуют связь между требованиями и тестами: “одним из самых эффективных путей тестирования требований являются тест-кейсы, очень похожие на те, что используются для тестирования завершённой системы". [Григорий Мельник и Боб Мартин](http://gmelnik.com/papers/Melnik-Martin-Tests-and-Requirements-The-Moebius-Strip-IEEE-Software-2008.pdf) расширяют это и утверждают: “По мере увеличения формальности тесты и требования становятся неразличимыми. В пределе они не различимы”. Тесты должны быть настолько чёткими, чтобы их можно было автоматизировать. A-TDD использует это утверждение и формулирует требования путём написания автоматизируемых тестов.

**Воркшопы по прояснению требований** — Шестой принцип гибкой Разработки ПО напоминает нам: “Непосредственное общение является наиболее практичным и эффективным способом обмена информацией как с самой командой, так и внутри команды.” Непосредственное прояснение требований на воркшопах использовалось с момента изобретения [Joint Application Design (JAD)](http://www.amazon.com/Joint-Application-Development-Jane-Wood/dp/0471042994). И также используется в  [Rapid Application Development (RAD)](http://www.amazon.com/Rapid-Application-Development-James-Martin/dp/0023767758) и методе гибкой разработке - [DSDM](http://www.amazon.com/DSDM-Dynamic-Systems-Development-Practice/dp/0201178893). A-TDD так же использует непосредственное общение на воркшопах по формирования тестов в виде требований.

**Одновременное проектирование** — Авторы книги [Concurrent Engineering Effectiveness](http://www.amazon.com/Concurrent-Engineering-Effectiveness-Integrating-Organizations/dp/1569902313) определяют одновременное проектирование так: “Существует настолько тесная связь между участниками в процессе разработки ПО, что они могут осуществлять большую часть их работы одновременно”. Сокращение времени разработки - основной драйвер одновременного проектирования. Двухнедельные итерации слишком малы, поэтому командам нужно постигать путь работать одновременно — последовательная разработка не работает в коротких циклах. Мы видели, как команды изобретают Specification By Example снова и снова, просто потому что они хотели ответить на вопрос: “Как мы можем выполнять нашу работу одновременно.”

**Предотвращение вместо обнаружения** — В одном из первых исследований в книге [A Study of the Toyota Production System](http://www.amazon.com/Study-Toyota-Production-System-Engineering/dp/0915299178), Сигэо Синго пишет: “Предназначение инспекции должно быть в предотвращении; однако, мы должно изменить наш образ мышления, чтобы инспекция имела данную цель.” Так же, в статье [“The Growth of Software Testing,”](https://www.researchgate.net/profile/David_Gelperin/publication/234808293_The_growth_of_software_testing/links/5743149208ae9f741b37d89a/The-growth-of-software-testing.pdf) авторы идентифицируют пять периодов эволюции тестирования ПО. Они называют последний период  “Период направленный на предотвращение” и стадия , “Задавать вопросы, связанные с тестированием… рано часто важнее для обеспечения качества ПО и экономически эффективной разработки, чем собственно выполнение тестов”. Это в точности то, что Specification by Example старается сделать. Когда специалисты по тестированию принимают участие в воркшопе по уточнению требований, они могут задавать вопросы о тестировании, и таким способом улучшать требования и препятствовать появлению дефектов. Всеобщее управление качеством (англ. Total Quality Management, TQM) - повлиявшее на Тойоты и бережливую разработку — также продвигает предотвращение вместо обнаружения.

Как работает A-TDD? Иллюстрация ниже даёт общее представление.

<figure>
  <img src="/img/test_automation/atdd.png" alt="atdd.png">
  <figcaption>Обзор A-TDD</figcaption>
</figure>

## Обзор A-TDD

A-TDD состоит из трёх шагов:

1. Обсудить требования на воркшопе.
2. Реализовать требования одновременно в итерации.
3. Поставить результат заинтересованным лицам для приёмки.

**Обсудить** — Требования выявляются путём обсуждения на воркшопе. Его участниками являются кросс-функциональные команды, Владелец Продукта или его представитель и любые заинтересованные лица, кто потенциально может обладать информацией о данных требованиях. Обычный вопрос, который задаётся на таких воркшопах: “Представьте, что система закончена. Как вы бы использовали её и что ожидали бы от неё?”. Ответом на такой вопрос будут примеры использования,  и такие примеры могут быть записаны как тесты, являющиеся требованиями. Фокус воркшопа должен быть больше на обсуждении и выявлении требований, чем на актуальных тестах.

**Реализовать** — В конце воркшопа, примеры "дистиллированы" в тесты и все активности, которые нужны, чтобы реализовать требования одновременно. Они включают:

* создание "клея" между тестами и продуктивным кодом (“тестовые библиотеки” и “низкоуровневые таблицы” в Robot Framework или ‘фикстуры’ в Fit)
* реализация требований, позволяющая тестам проходить
* обновление архитектурной и другой внутренней документации согласно рабочему соглашению команды
* пользовательская документация
* дополнительное исследовательское тестирование

Точный список зависит от конкретного продукта, контекста, рабочих соглашений, и [Критериев Готовности](../framework/definition-of-done.html).

**Поставить** — Когда тесты проходят, требования проверяются Владельцем Продукта и другими заинтересованными лицами. Это может привести к появлению новых требований или изменению существующих тестов.

Более подробное описание A-TDD показано ниже

<figure>
  <img src="/img/test_automation/atdd_clarified.png" alt="atdd_clarified.png">
  <figcaption>A-TDD в деталях</figcaption>
</figure>

A-TDD шаги хорошо отражаются в LeSS цикле

<figure>
  <img src="/img/test_automation/atdd_in_iteration.png" alt="atdd_in_iteration.png">
  <figcaption>Отражения шагов A-TDD в в Скраме</figcaption>
</figure>

*Обсудить на воркшопе* — Перед детализацией требований на Планированием Спринта, они совместно проясняются командой, Владельцем Продукта, и другими заинтересованными лицами на воркшопе.

*Реализовать одновременно* — Задачи для реализации тестов/требований созданы во время Планирования Спринта и реализованы в течение итерации. Все активности происходят “примерно в одно и то же время”.

*Поставить для приёмки* — Инкремент работающего продукта, проходящего приёмочные тесты, поставляется для приёмки заинтересованным лицам и обсуждается с ними на Обзоре Спринта.

## Обсудить на воркшопе

The workshop-related experiments are strongly connected to those in the Requirements chapter. Этот раздел покрывает A-TDD темы; раздел "Требования" раскрывает тему воркшопов более детально.

### Обсудить на воркшопе во время Уточнения Бэклога Продукта

Команда и Владелец Продукта ‘инспектируют’ Бэклог Продукта во время [Уточнения Бэклога Продукта](../framework/product-backlog-refinement.html), чтобы удостовериться, что он находится в хорошей форме. Эта активность включает следующее:

* Оценить и прояснить недавно добавленные Элементы Бэклога Продукта.
* Разделить большие элементы на маленькие, что бы они могли быть выбраны для реализации.
* Прояснить неотложные элементы так, чтобы команда хороша поняла их на уровне, достаточном для реализации.

Прояснение неотложных элементов может быть сделано через воркшоп в стиле A-TDD. Чтобы прояснить, Уточнение Бэклога Продукта состоит не только из A-TDD воркшопа, но он может быть частью активности по уточнению. Другие активности включают оценку и разбиение.

### Прояснение важнее, чем написание тестов

A-TDD для совместного прояснения требований. Акцент на общении, совместной работе и обучении через примеры и тесты. Цель состоит в улучшении понимания, и тесты являются средством её достижения. Книга на эту тему, названая подходящим образом, [Bridging the Communication Gap](http://www.amazon.com/Bridging-Communication-Gap-Specification-Acceptance/dp/0955683610) подчёркивает:

> [Разработка через приёмочное тестирование] не является техникой программирования: это техника для общения, которая сближает людей, вовлечённых в процесс разработки.

Люди часто озабочены осязаемыми выходом воркшопа - тестами - поэтому они забывают о нематериальных результатах - обучении. Понимание и ясность требований - это ключевой выход воркшопов по уточнению требований; тесты являются выражением этого.

Тут нет ложной дихотомии. Тесты тоже важны, и эта техника называется разработкой через приёмочное тестирование. Без тестов это будет только воркшоп по прояснению требований — но избегайте путаницы целей и средств.

### Используйте примеры

> “Вы можете привести пример?”

Этот вопрос может внезапно превратить смутное и абстрактное обсуждение в понятное и конкретное. Когда обсуждаются новые продукты, люди склонны заканчивать разговор на концептах и абстрактных понятиях. Они говорят друг с другом без понимания - они застряли. Приведение примеров возвращает обсуждение к реальности.

Например, мы слышим утверждение: “Система должна восстанавливаться после сбоя.” Это непонятно, поэтому мы просим привести примеры, что преображает дискуссию. Это могло бы быть: “Когда мы вытаскиваем кабель, система не должна падать”, что конкретно и понятно. Примеры также используются для дальнейшего прояснения, например, “Как система должна восстановиться, если мы удалим её блок, пока она работает?”

Примеры не так полезны для прояснения требований, как для путей работы. “Мы никогда не сможем автоматизировать все наши тесты!” - это то, что мы бы продолжили: “Вы можете привести пример теста, который нельзя автоматизировать?”, и это переносит дискуссию от принципов к практике.

<figure>
  <img src="/img/test_automation/examples.png" alt="examples.png">
  <figcaption>Примеры</figcaption>
</figure>

Иллюстрация выше показывает связь между примерами, требованиями и тестами. Во время воркшопов по уточнению требований, используйте примеры для выработки требований и преобразования их в тесты.

### Не ‘оптимизируйте’ воркшоп по уточнению требований

Когда мы обсуждаем A-TDD в больших продуктовых группах, они указывают: “Мы улучшили A-TDD воркшоп. Его участников только трое: Владелец Продукта, Скрам-мастер, и специалист из команды.“ Мы спрашивали их, как другие члены команды могли бы понять требования и реализовать их, и ответ был “Специалист им расскажет“. Они ‘оптимизировали‘ воркшоп, назвав им традиционную передача требований от аналитика команде.

### Избегайте компьютеров и проекторов на воркшопе

Компьютеры высасывают жизнь из воркшопов. Они становятся центром обсуждения. 
Computers suck the жизнь кровь out of a workshop. They become the center of the discussion. Помимо проверки ссылок с материалами, избегайте необходимости ’оптимизировать’ воркшоп, вводя его непосредственно в компьютер. Вместо этого…

### Выражайте рабочий процесс в бизнес-правилах

Прояснения требований на воркшопе часто начинается с абстрактных концептов, и когда приведены примеры, обсуждение рабочего процесса переходит к: ”Пользуясь системой, я выполняю шаг 1, замет шаг 2, и ожидаю Х”.

Эти примеры рабочего процесса могут заканчиваться похоже, с небольшими различиями в один или два шага. Тесты рабочего процесса содержать скрытые бизнес-правила, которые могут быть извлечены и положены в основу тестов на основе данных. Это фокусирует дискуссию на прояснении области требований и снижает сложность, убирая неуместные детали.

### Проверяйте стены

Правильным домом для тестов должны быть стены - конечно, с ”белыми досками” между ними. Большие пространства ”белых досок” продвигают совместную работу — предназначение воркшопов. Зарисовки на них фотографируется. После воркшопа, тесты могут быть ”дистиллированы” и зафиксированы в инструменте.

<figure>
  <img src="/img/test_automation/atdd_wall1.jpg" alt="atdd_wall1.jpg">
</figure>

<figure>
  <img src="/img/test_automation/atdd_wall2.jpg" alt="atdd_wall2.jpg">
</figure>

### Используйте табличный формат

Выражение бизнес-правила в таблицах делает их более понятными и помогает найти пропущенные сценарии. Таблицы вдохновляют ясное мышление. Влиятельный учёный в области информатики [Дэвид Парнас продвигает на протяжении долгого времени](http://link.springer.com/chapter/10.1007/978-3-7091-6510-2_12#page-1) таблицы для документации требований.

> [Когда документирование требований,] написание, понимание, и раскрытие происходят в одной и той же таблицы… Табличная нотация является лучшей помощью в ситуациях, подобных данной. Сначала определяют структуры таблицы, убеждаясь, что заголовки покрывают все возможные сценарии, а затем обращают внимание на заполнение отдельных записей в таблице.

### Используйте тесты рабочего процесса

Извлечение бизнес-правил и использование тестов на основе данных не всегда возможно или желаемо. Некоторые требования лучше выражать в виде примера рабочего процесса (многошагового сценария). Также, тесты бизнес-правил на основе данных могут быть часто дополнены примерами рабочего процесса, таким образом, связывая их.

Предупреждение: Когда большая часть ваших тестов это тесты рабочего процесса, то вы, возможно, упустили некоторые бизнес-правила.

### Типичный план воркшопа

Из чего состоит A-TDD воркшоп? Мы часто используем следующий план: 

1. *Вступление* — Владелец Продукта приветствует всех на воркшопе и объясняет его цель.
2. *Отбор* — команда и Владелец Продукта выбирают элементы из Бэклога продукта, над которыми будут работать
3. *Обзор* — Владелец Продукта или его представитель дают короткий обзор выбранные требований.
4. *Расхождение* — команда делится на две или три подгруппы, каждая из которых берёт элемент и начинает набрасывать примеры на досках. Владелец Продукта и его представители перемещаются между подгруппами.
5. *Схождение* — подгруппы сходятся на время, чтобы поделиться результатами с остальными.
6. *Повторение* — цикл расхождения-схождения обычно занимает 30-45 минут. Один воркшоп содержит несколько циклов.
7. *Итоги* — Владелец Продукта подводит итоги работы. Далее следует краткое обсуждение воркшопа.
8. *Фиксация результатов* — участники делают фотографии всех записей и размещают их в вики. Они уже могли бы сделать выжимку в виде нескольких тестов и оформить их в A-TDD инструменте.

## Develop in Concurrence

After the requirements are clear, they need to be implemented. The different activities required for implementation are done in concurrence. The team extends the tests while at the same time implementing the code, writing the documentation, updating the design description, and so forth.

### Distill the tests

Many examples are created during the requirements workshop. Not all of these become tests—only the essential parts of the requirements are distilled into tests. The не выжимка or duplicate parts are discarded—they have served their purpose for learning during the workshop.

How to distill tests from examples? Some techniques:

* **Duplication**—Remove duplication among examples by writing the tests in a different form. For example, a set of workflow tests might be combined into a business-rule test. Most of this should have happened during the workshop.
* **Equivalence class**—Some examples are part of the same equivalence class and therefore it is enough to keep one test. People with a testing speciality are especially valuable since equivalence-class partitioning is a classic testing technique.
* **Acceptance**—Since not all examples are of equal importance, ask the Product Owner, “What set of examples do you want to see running at the end of the iteration?”

### Use A-TDD coaches and facilitators

A-TDD is easy to do, and hard to adopt. It requires challenging deeply rooted assumptions and changes in habit. An (external) coach with experience in A-TDD and organizational change is frequently needed for this. Find a coach.

It is important to realize that the skills of a good A-TDD coach are different from those of a good TDD coach. TDD coaching is more technical, and focused on individual developers, whereas A-TDD involves the whole team. In additional to technical skills, a good A-TDD coach has excellent workshop-facilitation skills.

### Use an A-TDD Tool

* Fit is perhaps the first A-TDD tool. It was developed by Уорд Каннингем in 2002. Fit tests consist of HTML tables that are executed by a piece of glue code—called a fixture. Миха and Боб Мартин created an extension of Fit called FitNesse in which the tables are written in a wiki. Fitnesse also includes Slim—a slimmer execution model that offers better portability and the flexibility to explore new test syntaxes. More information can be found in the recommended readings at the end of this chapter.
* Robot Framework originates from Nokia Siemens Networks and was developed by Пекка Кларк. It was открыт in 2008. Robot has some similarities to Fit, such as tabular structured tests and glue code between the tables and the system. However, it also has unique features such as layering tables (user keywords).
* Cucumber was developed by Аслак Хэллисей and inspired by Dan North. It follows the given/when/then format for describing the examples. Cucumber tests are readable sentences in plain text.

### Don't use conventional test tools for A-TDD

Some product groups we worked with try to use their conventional test tools such as Lisp-based scripts or TTCN for A-TDD. This invariably fails. Why? A-TDD-style tests are created so that the Product Owner or user can read and understand the tests. But the test format—scripts—of these conventional tools are created for testers and are thus unsuitable for documenting requirements. It is nearly impossible to involve the Product Owner in writing examples using such tools.

### But do wrap conventional test tools under an A-TDD tool

Should you throw away all conventional test tools when adopting A-TDD? Perhaps not.

A graphics product group we worked with had spent years building a scripting language for automating their tests. It would take an additional few years to develop the glue code (test libraries or fixtures) between the A-TDD framework and their system under test—most of it is the same work they did with their scripting language.

An alternative is to let the glue code wrap their test scripting language and reuse their earlier work. Conventional test tools are not necessarily bad tools, but they just provide the wrong format—the wrong language—for executable specifications.

## Deliver for acceptance

The code is implemented and all the tests pass. What’s next? The A-TDD cycle, like Scrum, contains an inspect–adapt cycle where the results are delivered to stakeholders, who inspect the outcome using the tests and decide how to proceed—which requirements to implement next.

### Show tests in Sprint Review

In a Sprint Review, the team demonstrates visible progress to the Product Owner by showing the output of the iteration.

We worked with some groups that defined the demo steps during the Sprint planning. The team would spend an inordinate amount of time in demo preparation. A complete waste.

During Sprint Planning, an alternative is to define the examples that need to pass and show the progress by using these tests in the Sprint Review.

## Recommended Readings

* [*Specification by Example*](http://www.amazon.com/Specification-Example-Successful-Deliver-Software/dp/1617290084), by Гойко Аджич. This book covers several case studies about "Specification by Example". Гойко coined the term to replace all previous terms such as A-TDD.
* [*Bridging the Communication Gap*](http://www.amazon.com/Bridging-Communication-Gap-Specification-Acceptance/dp/0955683610/ref=sr_1_1?ie=UTF8&qid=1415541943&sr=8-1&keywords=bridging+communication+gap) , by Гойко Аджич. The book before Specification by Example which has a strong focus on requirements clarifications and workshops.
* [*Acceptance Test Driven Development: An Overview*](http://testobsessed.com/2008/12/acceptance-test-driven-development-atdd-an-overview/) , by Элизабет Хендриксон. A blog post and related paper providing an overview of A-TDD by giving a detailed example of using Robot Framework.
* [*Fit for Developing Software*](http://www.amazon.com/Fit-Developing-Software-Framework-Integrated/dp/0321269349) , by Рик Магридж and Уорд Каннингем. This book has a strong focus on improving the communication of requirements by means of Fit tables.
* [*Robot Framework User Guide*](https://code.google.com/p/robotframework/wiki/UserGuide) . Does not cover A-TDD, but does provide an excellent introduction to the Robot Framework tool.
* [*Test-Driven .NET Development with FitNesse*](http://www.amazon.com/Test-Driven-NET-Development-FitNesse/dp/0955683602) , by Гойко Аджич. This book has less emphasis on A-TDD and more on FitNesse. But it does a good job in describing the tool.
