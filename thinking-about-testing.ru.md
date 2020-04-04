---
title: Thinking About Testing ???
order: 55
---

<div class="chapter_quote"><p>
Тестирование программы может весьма эффективно продемонстрировать наличие ошибок, но безнадёжно неадекватно для демонстрации их отсутствия.
<br/>
--Эдсгер Дейкстра
</p></div>

## *Тестирование* больше не означает *тестирование*

Запутаны? Можем себе представить. Раньше цель тестирования была достаточно ясной -- "Тестирование - это процесс выполнения программы с целью нахождения ошибок" [[Myers79]](http://www.amazon.com/Art-Software-Testing-Glenford-Myers/dp/1118031962). Но она меняется при переходе к гибкой и бережливой разработке.

Параллельное проектирование требует распараллеливания работы. Выделенные кросс-функциональные команды поощряют отдельных специалистов расширять свою экспертизу. Это приводит цели обычных действий по разработке -- таких как тестирование -- к смещению.

Практики работы с кодом, такие как (модульная) разработка через тестирование, размывают границы между тестированием и проектированием, на что явно указывает лидера гибкой разработки [Уорда Каннингема](http://ieeexplore.ieee.org/xpl/articleDetails.jsp?arnumber=951502&sortType%3Dasc_p_Sequence%26filter%3DAND%28p_IS_Number%3A20576%29): 

> “Написание тестов сначала - это не практика тестирования”

Разработка через приёмочное тестирование (A-TDD) *убирает* различия между *тестированием* и *анализом требований*. В журнале IEEE Software в статье [“Тесты и Требования, Требования и Тесты: Лента Мёбиуса (Test and Requirements, Requirements and Test: A Möbius strip.)”](http://gmelnik.com/papers/Melnik-Martin-Tests-and-Requirements-The-Moebius-Strip-IEEE-Software-2008.pdf) Роберт Мартин и Григорий Мельник утверждают...

<figure>
  <img src="/img/test_automation/moebius.png" alt="mobius.png">
</figure>

> ... для раннего написания приёмочных тестов, как методики разработки требований. Мы считаем, что конкретные требования сочетаются с приёмочными тестами во многом так же, как две стороны полосы бумаги становятся одной в ленте Мёбиуса. Другими словами, требования и тесты становятся неразличимыми, поэтому вы можете указать поведение системы, написав тесты, а затем проверить это поведение, выполнив эти тесты.

Это размывание границ может привести к заблуждениям. Внедрение (модульной) разработки через тестирование в качестве техники *тестирования* упускает его цель из виду и приводит к поверхностному внедрению. Точно так же мы должны регулярно разъяснять группам тестирования, что *они* не могут внедрить разработку через приёмочное тестирование без участия других членов команд.

Тестирование больше не тестирование.
{: .box_top_bottom  .text_centered_bold }

## Бросьте вызов убеждениями о тестировании

Как уже говорилось выше, дискуссии о тестировании изобилуют убеждениями. Бросьте им вызов! Чтобы было ясно, мы не говорим, что эти убеждения являются *ложными*, но не ставя их под сомнения, мы *ограничиваем* наше мышление и способность улучшаться. Глубоко укоренившийся принцип в культуре Тойота является одним из столпов Пути Toyota (Toyota Way): *непрерывное улучшение*, бросая вызов всему. Тайити Оно (основатель бережливого мышления) сказал: 

> Если вы собираетесь постоянно следовать философии Кайдзен... Вы должны предположить, что все неидеально. Слишком много людей предполагают, что все в порядке, как они есть... Кайдзен о том, как все изменить. Если вы предполагаете, что все в порядке, то вы не сможете заниматься Кайдзен. Так что измените что-нибудь!

Что за убеждения? Мы *сталкиваемся* с некоторыми из них:

* тестирование должно быть независимым и поэтому отделённым от разработки
* тестирование не может начаться, пока код не написан полностью
* тестирование следует последовательности (1) создание тест-кейса, (2) выполнения тест-кейса, (3) отчёта о прохождении тест-кейса (тестовый водопад)
* должен быть отдельное подразделение тестирования
* должен быть *менеджер по тестированию*
* тестирование должно быть сделано в конце
* тестирование должно быть “хорошо спланировано”
* должна быть “стратегия тестирования” и “генеральный план тестирования”
* 100% покрытие тестами слишком дорого
* 100% автоматизация тестирования слишком дорога
* тестирование требует сложного инструмента для управления тестированием
* тестирование должно проводиться ‘тестерами’
{: .two_columns .box_top_bottom}


Не ставя под сомнение эти убеждения, вы поддерживаете *коробочное* мышление. Если вы считаете, что “тестирование может начаться только после завершения кодирования”, вы никогда не будете рассматривать инновационные способы проведения раннего тестирования. Но как только вы осознаете своё убеждение, вы можете усомниться в нём и спросить: “Существует ли способ, следуя которому я мог бы работать по-другому, чтобы тестирование началось до завершения кодирования?”

## Избегайте использования сложной терминологии в тестировании

Вопрос, который нам нравится задавать крупным продуктовым группам, звучит так: “Что всем вам нужно сделать, прежде чем поставить свой продукт?”

Давным-давно мы узнали, что нам нужны два столбца: один для ‘нормальных’ действий, а другой большего размера - для активностей *тестирования*. Первый столбец заполнен такими элементами, как кодирование, создание документации для пользователей, разработка оборудования, ценообразование и обучение торгового персонала. Второй столбец содержит тестовые *активности*, тестовые *уровни* или тестовые *классификации*. Обобщённые записи из второго столбца показаны ниже:

* блочное тестирование
* функциональное тестирование
* стресс-тестирование
* тестирование совместимости
* нагрузочное тестирование
* тестирование установки
* обезьянье тестирование
* тестирование документации
* модульное тестирование
* системное тестирование
* тестирование стабильности
* тестирование совместимости
* тестирование под трафиком
* тестирование безопасности
* исследовательское тестирование
* приёмочное тестирование
* разработческое тестирование
* интеграционное тестирование
* регрессионное тестирование
* тестирование надёжности
* тестирование производительности
* ёмкостное тестирование
* тестирование удобства
* пользовательское приёмочное тестирование
{: .two_columns .box_top_bottom}

## Сохраняйте простую классификацию тестов

Простая терминология вдохновляет разумное поведение. Например, технологические тесты, которые поддерживают команду, обычно выполняются программистами во время кодирования, в то время как тесты, ориентированные на клиента, которые проверяют продукт, обычно выполняются человеком, не являющимся первоначальным автором, и выполняются сразу после реализации некоторой пользовательской функциональности.

Две группы:

* [разработческое тестирование](unit-testing.html)
* [пользовательское тестирование](test-automation.html)

*Разработческое тестирование* -- оно обычно проводится  человеком, который пишет код. Цель состоит в том, чтобы проверить, выполняет ли код то, что хочет программист. Если тесты пройдены, это означает, что система делает то, что задумал разработчик, но это не обязательно означает, что она делает то, что хотят клиенты.

*Пользовательское тестирование* -- оно проверяет, выполнены ли требования. Они часто реализуются и выполняются человеком, отличным от того, кто написал код. В этой группе нефункциональные тесты классифицируются как тесты, ориентированные на клиента, поскольку требования для них в больших системах обычно являются явными и наиболее важными.

## Не разделяйте разработку и тестирование

Бил Хетцель (Bill Hetzel), организатор первой конференции по тестированию ПО, определил в книге [*The Complete Guide to Software Testing*](http://www.amazon.com/Complete-Guide-Software-Testing/dp/0471565679) шесть принципов тестированию. Шестой принцип -- независимость -- общая мотив на протяжении всей истории тестирования ПО. Гленфорд Майерс (Glenford Myers), автор первой книги о тестировании ПО, подчёркивал независимость тестирования в ней [*Software Reliability*](http://www.amazon.com/Software-Reliability-Principles-Glenford-Myers/dp/0471627658) :

> Тестирование всегда должно выполняться внешней стороной, которая несколько отстранена от программы и проекта... Тестирование системы всегда должно выполняться независимой группой, такой как обособленный отдел обеспечения качества.

Почему разделение так важно? Некоторые часто приводимые аргументы:

* Программирование конструктивно, тогда как тестирование деструктивно -- поэтому программисты не могут тестировать.
* Если программисты тестируют свой собственный код, они изменят тест в соответствии с реализацией.
* Когда тестирование выполняется той же группой, что и разработка, они могут уложиться в срок, пропустив тестирование.

Первые два аргумента предполагают команды узкофункциональных специалистов, а не кросс-функциональные команды. Последний аргумент предлагает быстрое решение гораздо более серьёзной проблемы, связанной с разрушением качества путём срезания углов при оказании давления на разработчиков.

В этих аргументов, *независимость* тестов приравнено к отделению тестирования от разработки. Однако, [Хетцель](http://www.amazon.com/Complete-Guide-Software-Testing/dp/0471565679) проясняет этот принцип:

> Требуется, чтобы была достигнута независимость ***духа***, но не обязательно, чтобы тестирование проводилось отдельной группой людей.

Этот момент повторяется в книге [*Agile Testing*](http://www.amazon.com/Agile-Testing-Practical-Guide-Testers/dp/0321534468), в которой авторы также указывают на локальную субоптимизацию, создаваемую отделением тестирования:

> Команды часто путают “независимость” и “раздельность”. Если структура отчётности, бюджеты и процессы находятся в разных функциональных областях, различие между программистами и тестировщиками неизбежно. Тратиться время на дублированные совещания: программисты и тестировщики не разделяют общей цели, а обмена информацией вообще не происходит.

Независимость тестирования не означает независимых тестеров.
{: .box_top_bottom  .text_centered_bold }

Как добиться *духа* независимости тестирования в без отделения тестирования? *Путём написания тестов до реализации кода*. Тест не может оказаться под влиянием реализации, потому что она ещё не существует. Таким образом, разработка через тестирование позволяет достичь *духа* независимости разделения разработки и тестирования на обособленные отделы.

## Тестировщики и программисты работают вместе

Отделение тестирования от разработки часто приводит к конфликту между программистами и тестировщиками. Тестеры -- охотясь за ошибками -- пытаются доказать, что часть программы неисправна. Программисты -- гордясь своим кодом -- защищают себя, свой код и свою программу. Вероятно, это испытал каждый, кто работал в роли тестировщика в отделе тестирования.

В команде Скрам-команде *‘тестеры’ уже не тестеры*, а ‘просто’ члены команды - с тестированием в качестве *основной специализации*. ‘Программисты’ - это *любые* члены команды, которые могут писать код. Каждый член команды разделяет общую цель и -- как и вся команда -- ответственен за достижение этой цели. Члены команды с разными основными специализациями должны сотрудничать для достижения этой цели.

## Обучайте и тренируйте навык тестирование

Хорошие навыки тестирования приходят с осознанной практикой и временем. К сожалению, особенно в крупных организациях, навыки тестирования не находят уважения. *“Каждый* может это делать” - распространённое убеждение в крупных компаниях по поводу тестирования, поэтому поиском тестировщиков занимается подрядная компания, которая случайным образом отбирает людей с улицы и назначает их на позиции тестирования. Случайные люди, нанятые, чтобы *отмахиваться* от приложения, обычно рассматривают свою работу как временную стадию, через которую они должны пройти, прежде чем перейти к “настоящей работе”. Они не заботятся об углублении своих навыков тестирования и, таким образом, внушают ложное убеждение, что тестирование тривиально.

> Тестировщики, которые не стремятся повышать свою квалификацию и расти профессионально, способствовали мнению о том, что тестирование - низкоквалифицированная работа. [[CG09]](http://www.amazon.com/Agile-Testing-Practical-Guide-Testers/dp/0321534468)

Попасть в ловушку “тестирование тривиально” дорого. Поддержите мастерство тестирования, предоставляя материал для самостоятельного изучения, обучение и [коучинг](../adoption/coaching.html). Мы перечислили некоторую общую литературу по навыкам тестирования в рекомендуемом разделе чтения.

Конечно, обучение и коучинг по тестированию также важны для традиционной среды. В кросс-функциональных командах это становится ещё более актуальным, поскольку тестеры иногда чувствуют себя изолированными. Отсутствие в организации функциональных подразделений тестирования может повлиять на чувство карьерного роста и их интерес к тестированию. И это усугубляется, если все образование и коучинг связаны с практиками разработки или менеджмента. Высокая текучесть тестировщиков во время перехода к гибкой организации не редкость.

> Они (рассказ одного из участников сессии "Конференция внутри конференции" на Agile 2007, [прим. переводчика]) разделили свою организацию тестирования... Однако они включили тестировщиков в подразделения разработчиков без какого-либо тренинга; после этого в течение трёх месяцев все тестировщики уволились, потому что не понимали своей новой роли.[[CG09]](http://www.amazon.com/Agile-Testing-Practical-Guide-Testers/dp/0321534468)

Similarly, in an agile transition we worked with, many testers left to different products because they felt they had lost their identity and did not know how to work in a Scrum team. Prevent this by developing the team’s testing expertise.

## Create community of testing

Education and coaching are not the only ways to grow expertise. Open discussion and experience-sharing foster learning. One purpose of a functional unit--a test department--is to enable this learning. Without it, other means for discussion and sharing experiences are needed. For instance, by establishing a [Community of Practice](../structure/communities.html) for testing. People interested in testing--not only those with testing as their main specialization--meet every now and then to learn from each other or discuss via a mailing list or wiki.

Test managers can play an important role in this community. They can use their expertise in testing and management and become CoP coordinators--in accordance with the [lean principle of manager-teachers](../principles/lean-thinking.html).

> Rather than keeping the testers separate... [think about] a community of testers. Provide a learning organization to help your testers ... share ideas and help each other. If the QA manager becomes a practice leader in the organization, that person will be able to teach the skills that testers need to become stronger and better able to cope with the ever-changing environment. [[CG09]](http://www.amazon.com/Agile-Testing-Practical-Guide-Testers/dp/0321534468)

## Don't have separate test automation teams

We advise organizations to invest in test automation and create a safety net of regression tests around their legacy code so that they can gradually work themselves out of the mess. They listen, and then create a separate test automation team.

Sometimes the test automation team tries to solve *all world problems* with their testware, and the effort produces only a lot of paper. But, sometimes we encounter a more pragmatic test automation team that actually creates testware such as an automation framework. They release every couple of months and everyone is impressed with the results.

What happens then? New functionality is implemented. Interfaces change and the automated tests fail. The development teams are upset and tell the test automation team to fix the tests. Or, the development teams comment out the tests because they do not understand them. Or, the testware is handed over to the development teams who discover it is unusable or incomprehensible and ignore it. Or... we have experienced a dozen different scenarios in organizations. It never worked.

Why? The assumption that is the *creation* *of the testware* is the difficult part and the most important thing. But other important aspects are under-appreciated:

* Creating testware requires deep understanding of the product.
* Maintenance and evolution is more effort than initial creation.
* Insights obtained during testware creation is perhaps more important than the testware itself.
* Creating testware without *using* it leads to complex and unusable testware.

Considering these aspects, a separate automation team causes additional complexity, the потери от передач, and knowledge scatter. No wonder it so often fails.

Test automation should be the responsibility of the cross-functional development teams--just as testing is also their responsibility.

There is no shortcut to learning how to automate; a separate automation team is a *quick fix* --and harmful in the long run.

## Feature team as test automation team

A separate test-automation team has many drawbacks but also some advantages. They can create the initial test framework, produce training material, and support the teams.

How to get these benefits without the drawbacks?

A [feature team](../structure/feature-teams.html) can temporarily take on the role of test-automation team. Advantages:

* They have a deep understanding of the system.
* They can take a small feature so that the automation is concrete and realistic.
* The learning created during test -automation will not be lost.
* There is visibility into test automation as the items go on the Product Backlog.

## All tests pass--stop and fix

Test fails?

Stop and fix it!

“What about your automated tests?” we ask product groups when we visit them. Sometimes they reply, “We have 800 automated tests of which 200 are failing right now.” This is a huge queue and causes a complete lack of transparency in the development. When automated tests fail, fix them immediately.

## Have zero tolerance on open defects

Why do people insist on creating defects? They spend effort to insert a defect, then they need to search for it, prioritize it, and finally fix it. Not creating the bug in the first place would be a lot less work.

We *do* believe it is possible to write *bug-free code* . We do *not* believe it is easy or common. Still, focus on preventing defects.

“Zero tolerance on open defects” is a guideline used by one of our clients. If they find a defect, they fix it as soon as possible. This prevents

* effort spent on tracking many defects
* усилия, потраченные на приоритизацию
* delaying the learning that happens when fixing a defect
* spending extra time on fixing because the developers do not remember the code anymore

Delaying the fixing of bugs is a false economy inasmuch as they need to be fixed anyway and the cost will be higher. Moving bugs from queue to queue is fooling yourself--they are still there!

## Conclusion

Testing is not what it used to be. The barriers between testing and programming have to be demolished. Testing and programming are two sides of the same activity done by the same people. The purpose of the tests changes from finding defects to preventing them by writing the specifications as tests; and from checking the implementation to driving the design. This fundamentally different perspective leads to vital changes in the way people work--and work together.

## Рекомендуем к прочтению

* [*Agile Testing* , by Lisa Crispin and Janet Gregory](http://www.amazon.com/Agile-Testing-Practical-Guide-Testers/dp/0321534468). A great overview of the role of testing in agile development. It covers the challenges organizations face when adopting agile development and also describes the concrete role of testing during the iteration.
* [*Lessons Learned in Software Testing* , by Cem Kaner, James Bach, and Bret Pettichord](http://www.amazon.com/Lessons-Learned-Software-Testing-Context-Driven/dp/0471081124). This book describes the lessons learned from decades of experience in testing and also introduces the context-driven school of thinking in software testing.
* [*Agile Testing Directions* , by Brian Marick](http://www.exampler.com/old-blog/2004/05/26/). A series of blog posts wherein Brian Marick introduces the agile testing quadrants.
