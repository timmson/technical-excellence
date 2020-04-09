---
title: Автоматизация Тестирования
order: 60
---

## Ручные Тесты

Разработчики, следующие гибким принципы разработки ПО, подчёркивают важность автотестов. В коротких циклах ручное регрессионное тестирование почти невозможно. Значит ли это, что не должно вообще ручного тестирования? Нет. Рекомендуемы только некоторые виды ручного тестирования, например, тестирование, отличное от традиционного сценарного ручного тестирования. 

### Автоматизируйте ваши ручные тесты

В продуктовых группах часто утверждают: “Невозможно автоматизировать тесты, основанные на потере сетевого соединения“ или “Вы не можете автоматизировать тесты с падением аппаратного обеспечения“. Наш ответ обычно: “Нет, это не так” или “Да, вы можете”.

Элизабет Хендриксон, автор небольшой книги [*Exploratory Testing in an Agile Context*](/papers/et.pdf), осмеливается утверждать:

> Я думаю, если вы можете написать сценарий для ручного тестирования, то вы можете его автоматизировать

Автоматизировать ручные тесты *как есть* может быть не лёгкой задачей. Например, почти невозможно вытащить сетевой шнур автоматически в тесте с потерей соединения. Однако автоматический тест может быть выполнен в другом ключе. Вместо того, чтобы физически вытащить шнур, автоматический тест даёт команд драйверу сетевой карты, *как если бы* шнур был вытащен на самом деле.

Имеет ли ценность автоматизация всех тестов? Согласно Хендриксон:

> Если тест достаточно важен, чтобы создать для него сценарий и выполнять его, он также достаточно важен для автоматизации.

Почему так? Итеративно-инкрементальная разработка по подразумевает, что исходный код не фиксируется навсегда в конце каждой итерации, а потенциально готов к изменениям в следующих итерациях. Однако ручное регрессионное тестирование может означать повторное прохождение большинства тестов -- каждую итерацию. Автоматизация тестирования быстро себя окупает.  

Особенно в крупномасштабной разработке с фиче-командами и практикой общего владения кодом, страхующая сеть из автотестов имеет первостепенное значение.

### Проводите некоторые тесты вручную

Автоматизация *всех* тестов может быть бесполезной или даже невозможной. Следующие тесты могут выполняться вручную:

* *Тесты, требующие человеческого внимания и творческого подхода* -- Для оценки пользовательского интерфейса требуется человек -- тестирование удобства (usability testing). Исследовательское тестирование по определению требует кого-либо, кто принимает решение о дальнейших шагах.
* *Тесты, требующие физического движения* -- Например, тесты с различными физическими конфигурациями системы. Это может быть автоматизировано с помощью симуляции, но реальная конфигурация будет необходим для финального запуска тестов. 
* *Дорогие тесты* -- Запуск ёмкостных тестов (capacity tests) в промышленной среде может слишком дорогим, поэтому может быть выполнено один или два раза. Это откладывает риск. Эти риски должны быть снижены за счёт дешёвых тестов -- например, путём запуска ёмкостных тестов в среде симуляции -- таки образом запуск дорогих тестов становится просто окончательной проверкой.

Ложной дихотомии тут нет: Попытайтесь автоматизировать все тесты, но не забывайте тестировать вручную, когда это требуется.

### Проводите исследовательское тестирование

В книге [Perfect Software and Other Illusions about Testing](http://www.amazon.com/Perfect-Software-Other-Illusions-Testing/dp/0932633692), Джеральд Вайнберг называет их, “Исчерпывающая ошибка тестирования, что можно проверить все!” It is not. Количество возможных сценариев тестирования бесконечно, следовательно, автоматизация всех тестов означает бесконечные трудозатраты. Вместо этого автоматизируйте все типовые тесты и потратьте время эффективно, насколько это возможно, на исследовательское тестирование, чтобы обнаружить непредвиденные сценарии.
обзор исследовательского тестирования


<figure>
  <img src="/img/test_automation/et.png" alt="et.png">
  <figcaption>Исследовательское тестирование</figcaption>
</figure>

What is exploratory testing? “Simultaneous learning, test design, and test execution” [[Bach03]](http://www.satisfice.com/articles/what_is_et.shtml). This is in contrast to traditional scripted testing where test-case design and execution are separated and sequential steps—first design then execution. Exploratory testing aims at fully utilizing human creativity during test execution, using feedback and observations rather than mindlessly following a script. In exploratory testing, the tester is exploring the system, learning about it and using that information to make test-design decisions. It is best explained by an example.

Imagine that Gita is testing a 2D modeling application. First, she defines the goal of her test session—in exploratory testing this is called a mission or charter. Her charter is “Explore changing shapes by dragging the control points.” She takes a shape, drops it on the canvas, and creates a couple of control points on it. She drags one of them and observes what happens. Based on this observation (learning), she determines the next step (design) and performs it (execute). The shape takes its new form, though she notices—while dragging the control points—that the shape temporarily took a form that it probably should not have. Therefore, she continues dragging it and moving it around until she can reproduce the accidental transformation.

In the example, there is no detailed preconceived script or test case but instead an area of focus—a charter. The first step is to observe the system, and the next action is determined from that observation—this is test design. All traditional test techniques and heuristics are applied during this design step.

<figure>
  <img src="/img/test_automation/et_scripted_difference.png" alt="et.png">
  <figcaption>Exploratory testing</figcaption>
</figure>

## Automated Testing

### Create maintainable tests

“Automated tests will increase our test maintenance load” is a common objection we hear. Test maintenance will cost some effort, but a few straightforward techniques can minimize this cost:

* remove duplication in and between tests
* delete tests
* do not test through the UI
* run tests frequently

### Remove duplication in and between tests

Code duplication causes extra complexity, obscurity, and defects—resulting in extra maintenance effort. This is as true for test code as it is for production code. Avoid this by removing the duplication.

Workflow tests are a common cause of duplication. They often consist of one mother scenario and multiple derived cases with only slight variations in them. When one step changes, all these workflow tests need to be updated. This duplication can be avoided by data-driven tests that focus on business rules or by separating the duplication into test libraries or fixtures.

We coached a team that made a common mistake—they delayed their test automation until the end of the iteration. Four days remaining and only automation tasks left. In the previous iterations, these tasks were done by the test specialist, but now they had to be done by the whole team.

They started with a one-day workshop in which the one specialist coached the other team members. After that, they split into two pairs and one triplet working in parallel on automating the tests. Something interesting happened: The team members who were experienced in programming complained about the extra effort needed because of the duplication in the tests. Previously, none of them had noticed it and the test specialist—who did not have much programming experience—never cared. Now that the whole team was involved, they cared and the quality of the tests improved immensely.

### Delete tests when not adding value

Tests serve multiple purposes. They act as requirements, as verification, and as a safety net preventing system regression.

When an existing test is not needed anymore—because it is a subset of another test—then delete it. Leaving unnecessary tests brings no benefit but still increases maintenance effort and lowers test execution speed.

### Avoid testing through the UI

User interfaces (UI) tend to change frequently. Running your tests through the UI makes them vulnerable to these changes—even when there is no change in test logic. This increases the test maintenance effort.

Therefore, avoid testing through the UI and instead call the application logic directly through an API. Another advantage of doing this is that it speeds up your test since testing through the UI is slow.

### Run tests frequently

Long ago, we worked with a large group following waterfall development. Traditional test automation advice is to select and automate only the most important cases—with a separate automation team— after the release. So they did. At the end of the next release, they executed the tests and... they all failed. Updating them would take much time, so they decided to do all testing manually.

Executing tests once or twice a release seems efficient—fewer CPU cycles are wasted—but much will have changed and therefore many fail and cause a large batch of maintenance work. Alternatively, executing tests frequently—using a continuous integration system— uses more CPU cycles but results in less maintenance work since the effort to fix failing tests is small and straightforward. If you have a high test-maintenance load, chances are you are not executing the tests frequently enough.

### Treat нефункциональные the same as функциональные

Automating and continuously running non-functional tests is essential. Delaying them to the end means moving one of the biggest risks to where they hurt most. For example, if the system needs a certain performance level, test early to reach it early, and continuously run the test while new functionality is added to ensure that the system does not regress from its performance target.

нефункциональные are often treated экзотично people believe they cannot be specified and cannot be tested. This is unfortunate. In a requirements workshop, нефункциональные can be considered the same as функциональные, and example tests are created for clarifying them.

### Continuously run long-running tests

Non-functional tests frequently cannot be run in the normal continuous-integration-system cycle because they may take too long to execute—a stability test might take two weeks. Some product groups delay them until near the release—creating a delayed feed-back cycle. Not a good idea.

Run the long-running tests all the time in a slower continuous-integration-system cycle. Treat them as any other tests. When they fail, inform all people who checked in code. After they pass, get the latest build and immediately run them again. This way the feedback cycle is as short as it can be.

### Используйте виртуализацию или контейнеризацию

In order to speed up the tests and keep the investment in hardware low, maximize the use of виртуализацию using [VirtualBox](https://www.virtualbox.org/) or [VMWare](http://www.vmware.com/). An alternative to virtual machines (which aren't always fast to build and easy to maintain) are linux virtual containers such as [Docker](http://www.docker.io/)

### Avoid using commercial test tools

We once coached at a company building a commercial “automated testing” tool—a GUI testing tool. The requested coaching? To learn how to do automated testing for developing their automated testing tool...

A огромное множество commercial test tools are available. We rarely meet people who are actually satisfied with any of them. Most are overly complex and focus more on reporting and ‘management’ than on robust test automation. Favor free and open-source tools—made by developers solving real problems—over commercial tools.

Example of common test automation tools:

* [RobotFramework](http://www.robotframework.org/)
* [Cucumber](https://cucumber.io/)
* [Fitnesse](http://www.fitnesse.org/)
* [Selenium](http://www.seleniumhq.org/)
* [Capybara](https://github.com/jnicklas/capybara)

There are much more. The above is just a list of common tools, but new tools pop up all the time.