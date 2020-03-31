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

Запутаны? Можем себе представить. Раньше цель тестирования была достаточно ясной -- "Тестирование - это процесс выполнения программы с целью нахождения ошибок" [[Meyers79]](http://www.amazon.com/Art-Software-Testing-Glenford-Myers/dp/1118031962). Но она меняется при переходе к гибкой и бережливой разработке.

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

*Разработческое тестирование* --these are usually created by the person who is implementing. The purpose is to check whether the code is doing what the programmer wants. If the tests pass, it means that the system does what the developer intended--but this does not necessarily mean it does what the customers wants.

*Пользовательское тестирование* --these test whether the requirements are fulfilled. They are frequently implemented and executed by a person other than the one who wrote the code. In this grouping, non-functional tests are classified as customer-facing tests because non-functional requirements for large systems are typically explicit and the most important.

## Don't separate development and testing

Bill Hetzel, the organizer of the first software testing conference, defined in [*The Complete Guide to Software Testing*](http://www.amazon.com/Complete-Guide-Software-Testing/dp/0471565679) six principles of testing. The sixth principles--test independence--is a common theme throughout the history of software testing. Glenford Meyers, author of the first book on software testing, stressed the independence of testing in [*Software Reliability*](http://www.amazon.com/Software-Reliability-Principles-Glenford-Myers/dp/0471627658) :

> Testing should always be done by an outside party who is somewhat detached from the program and project... System testing should always be done by an independent group such as a separate quality-assurance department.

Why is separation important? Some frequently stated arguments:

* Programming is constructive whereas testing is destructive--thus, programmers cannot test.
* If programmers test their own code, then they will change the test according to the implementation.
* When testing is done by the same group as implementation, then they can meet their deadline by skipping testing.

The first two arguments assume single-specialist teams rather than cross-functional teams. The last argument suggests a quick fix for the much larger problem of quality-destroying shortcuts when pressuring developers.

In these arguments, test *independence* is equated to test separation from development. However, [Hetzel](http://www.amazon.com/Complete-Guide-Software-Testing/dp/0471565679) clarifies the principle:

> The requirement is that an independence of ***spirit*** be achieved, not necessarily that a separate individual of group do the testing.

This point is reiterated in [*Agile Testing*](http://www.amazon.com/Agile-Testing-Practical-Guide-Testers/dp/0321534468) in which the authors also point out the локальной субоптимизацией created by separating testing:

> Teams often confuse “independent” with “separate.” If the reporting structure, budgets, and processes are kept in discrete functional areas, a division between programmers and testers is inevitable. Time is wasted on duplicate meetings, programmers and testers don’t share a common goal, and information sharing is nonexistent.

Test independence does not mean independent testers.
{: .box_top_bottom  .text_centered_bold }

How to achieve test independence in *spirit* without separating testing? *By writing tests before implementing code* . The test cannot be influenced by the implementation, because it does not exist yet. This way, test-driven development achieves the *spirit* of independence without separation of departments.

## Testers and programmers work together

Separating testing from development often leads to a conflict between programmers and testers. Testers--hunting for bugs--try to prove that part of the program is faulty. Programmers--with their ego in their code--defend themselves, their code, and the program. Probably everyone who has been in the role of a tester in a test department has experienced this.

In a Scrum team, *‘testers’ are no longer testers* but ‘simply’ members of the team--with testing as their *primary specialization* . ‘Programmers’ are *any* members of the team who can code. Every member of the team has a shared goal and is held--as a team--accountable to that goal. Team members with different primary specializations have to cooperate in order to reach that goal.

## Educate and coach testing

Good testing skills come with deliberate practice and time. Unfortunately, especially in large organizations, testing skills are not respected. *“Everybody* can do that” is their belief, so they offshore it to a company that grabs people randomly from the street and assigns them to test. Random people hired to *bang away* on an application routinely see their job as a temporary stage they need to go through before advancing to a “real job.” They do not bother deepening their testing skills and so contribute to the false belief that testing is trivial.

> Testers who don’t bother to learn new skills and grow professionally contribute to the perception that testing is low-skilled work. [[CG09]](http://www.amazon.com/Agile-Testing-Practical-Guide-Testers/dp/0321534468)

Falling into the “testing is trivial” trap is costly. Support testing mastery by providing self-study material, education, and [coaching](../adoption/coaching.html). We have listed some general testing-skills literature in the recommended reading section.

Of course, providing education and coaching in testing is also important to traditional environments. In cross-functional teams, this becomes even more relevant as testers at times feel marginalized. Not having a testing functional organization may impact the feeling of career progression and their interest in testing. And this is exacerbated if all education and coaching is related to development or management practices. High test turnover during an agile transition is not uncommon

> They split up their test organization... However, they put the testers into the development units without any training; within three months, all of the testers had quit because they didn’t understand their new role. [[CG09]](http://www.amazon.com/Agile-Testing-Practical-Guide-Testers/dp/0321534468)

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

## Recommended Readings

* [*Agile Testing* , by Lisa Crispin and Janet Gregory](http://www.amazon.com/Agile-Testing-Practical-Guide-Testers/dp/0321534468). A great overview of the role of testing in agile development. It covers the challenges organizations face when adopting agile development and also describes the concrete role of testing during the iteration.
* [*Lessons Learned in Software Testing* , by Cem Kaner, James Bach, and Bret Pettichord](http://www.amazon.com/Lessons-Learned-Software-Testing-Context-Driven/dp/0471081124). This book describes the lessons learned from decades of experience in testing and also introduces the context-driven school of thinking in software testing.
* [*Agile Testing Directions* , by Brian Marick](http://www.exampler.com/old-blog/2004/05/26/). A series of blog posts wherein Brian Marick introduces the agile testing quadrants.
