# Автоматизация Тестирования

## Ручные Тесты

Разработчики, следующие гибким принципы разработки ПО, подчёркивают важность автотестов. В коротких циклах ручное регрессионное тестирование почти невозможно. Значит ли это, что не должно быть вообще ручного тестирования? Нет. Только некоторые виды ручного тестирования рекомендуемы, например, виды тестирования, отличные от традиционного сценарного ручного тестирования.

### Автоматизируйте ваши ручные тесты

В продуктовых группах часто утверждают: “Невозможно автоматизировать тесты, основанные на потере сетевого соединения“ или “Мы не можем автоматизировать тесты с падением “железа“. Наш ответ обычно: “Нет, это не так” или “Да, вы можете”.

Элизабет Хендриксон, автор буклета [*Exploratory Testing in an Agile Context*](/papers/et.pdf), осмеливается утверждать:

> Я думаю, если вы можете написать сценарий для ручного тестирования, то вы можете его автоматизировать.

Автоматизировать ручные тесты *как есть* может быть нелёгкой задачей. Например, почти невозможно вытащить сетевой шнур автоматически в тесте с потерей соединения. Однако автоматический тест может быть выполнен в другом ключе. Вместо того, чтобы физически вытаскивать сетевой шнур, автоматический тест даст команд драйверу сетевой карты, *как если бы* шнур был вытащен на самом деле.

Есть ли ценность в автоматизации всех тестов? Согласно Хендриксон:

> Если тест достаточно важен, чтобы создать для него сценарий и выполнять его, он также достаточно важен для автоматизации.

Почему так? Итеративно-инкрементальная разработка ПО подразумевает, что исходный код не фиксируется навсегда в конце каждой итерации, а потенциально готов к изменениям в следующих итерациях. Поэтому ручное регрессионное тестирование подразумевает повторное прохождение большинства тестов -- каждую итерацию. Автоматизация тестирования быстро себя окупает.  

Страхующая сеть из автотестов имеет первостепенное значение, особенно в крупномасштабной разработке с фиче-командами и практикой общего владения кодом

### Проводите некоторые тесты вручную

Автоматизация *всех* тестов может быть бесполезной или даже невозможной. Следующие тесты могут выполняться вручную:

* *Тесты, требующие человеческого внимания и творческого подхода* -- Для оценки пользовательского интерфейса требуется человек -- тестирование удобства (usability testing). Исследовательское тестирование по определению требует кого-либо, кто принимает решение о дальнейших шагах.
* *Тесты, требующие физического движения* -- Например, тесты с различными физическими конфигурациями системы. Это может быть автоматизировано с помощью симуляции, но реальная конфигурация будет необходима для финального запуска тестов.
* *Дорогие тесты* -- Тестирование ёмкости (capacity tests) в промышленной среде может быть слишком дорогим, поэтому может выполняться один или два раза. Это отсрочка увеличивает риски. Эти риски должны быть снижены за счёт дешёвых тестов -- например, путём тестирование ёмкости в среде симуляции -- таки образом запуск дорогих тестов становится просто окончательной проверкой.

Ложной дихотомии тут нет: Попытайтесь автоматизировать все тесты, но не забывайте тестировать вручную, когда это требуется.

### Проводите исследовательское тестирование

В книге [Perfect Software and Other Illusions about Testing](http://www.amazon.com/Perfect-Software-Other-Illusions-Testing/dp/0932633692) Джеральд Вайнберг называет их, “Глубочайшая ошибка тестирования в том, что можно проверить все!”. Это так. Количество возможных сценариев тестирования бесконечно, следовательно, автоматизация всех тестов означает бесконечные трудозатраты. Вместо этого автоматизируйте все типовые тесты и потратьте время эффективно, насколько это возможно, на исследовательское тестирование, чтобы обнаружить непредвиденные сценарии.

#### Краткий обзор исследовательского тестирования

<figure>
  <img src="/img/test_automation/et.png" alt="et.png">
  <figcaption>Исследовательское тестирование</figcaption>
</figure>

Что такое исследовательское тестирование? Это “одновременное обучение, разработка выполнение тестов” [[Bach03]](http://www.satisfice.com/articles/what_is_et.shtml). Это контрастирует с обычным сценарным тестированием, где проектирование тест-кейсов и их исполнение разделены и выполняются последовательно - сначала проектирование, потом исполнение. Исследовательское тестирование помогает полностью использовать творческое начало людей во время исполнения тестов, получение обратной связи и наблюдений в отличие от бездумного следования сценарию. В исследовательском тестировании тестировщик исследует систему, изучает её и использует эту информацию для принятия решений о дизайне самого теста. Это лучше объяснить на примере.

Представьте, что Гита тестирует программу для 2D-моделирования. Сначала, она определяет цель сессии тестирования - в исследовательском тестировании она называется миссией или чартером. Её чартер состоит в том, чтобы “Исследовать изменение фигур при перетаскивании контрольных точек.” Она берет фигуру, переносит её в рабочую область и создаёт пару контрольных точек на ней. Она перетаскивает одну из них и наблюдает, что произойдёт. Основываясь на этом наблюдении (новых знаниях), она определяет следующие шаг (дизайн) и выполняет его. Фигура приобретает новую форму, но она замечает - во время перетаскивания контрольных точек - что фигура временно приняла такую форму, котору не должна была принять. Поэтому, Гита продолжает перетаскивать фигуру и перемещать её вокруг, пока не сможет воспроизвести это случайное преобразование.

В этом пример нет детального предопределённого сценария или тест-кейса, но есть фокус на области - чартере. Первым шагом является исследование системы, на нём строится определение следующего действия - это и есть дизайн теста. Все традиционные методы испытаний и эвристики применяются на этом этапе проектирования.

<figure>
  <img src="/img/test_automation/et_scripted_difference.png" alt="et.png">
  <figcaption>Сценарное и Исследовательское тестирование</figcaption>
</figure>

## Автоматизированное тестирование

### Создавайте поддерживаемые тесты

“Необходимость поддержки автотестов увеличит нашу загрузку” - возражение, которое мы слышим. Поддержка автотестов потребует дополнительных усилий, но следующие техники могу их снизить:

* удаляйте дублирование внутри тестов и между ними
* удаляйте тесты, не добавляющие ценности
* избегайте тестирования через пользовательский интерфейс
* запускайте тесты часто
* относитесь функциональным м нефункциональным требованиям одинаково
* непрерывно выполняйте длительные тесты
* используйте виртуализацию или контейнеризацию
* избегайте использования коммерческих инструментов тестирования

### Удаляйте дублирование внутри тестов и между ними

Дублирование в коде приводит к дополнительной сложности, снижение прозрачности и дефектам - что ведёт к накладным расходам в сопровождении. Это правда для кода тестов, так и для продуктивного кода. Избегайте этого, удаляя дубликаты.

Процессные тесты (workflow tests) являются основной причина дублирования. Они часто состоят из одного материнского сценария и множества сценариев, незначительно отличающих друг от друга. Когда один шаг меняется, все эти тесты нужно обновить. Такое дублирование можно избежать с помощью тестов на основе данных (data-driven tests), которые фокусируются на бизнес-правилах, или переносом дубликатов в тестовые библиотеки или фикстуры.

Мы консультировали команду, которая совершила типичную ошибку - они отложили автоматизацию тестирования на конец итерации. За 4 дня до конца остались только задачи на автоматизацию. В предыдущих итерациях эти задачи были выполнены специалистом по тестированию, но теперь их нужно было сделать всей команде.

Они начали с однодневного воркшопа, на котором специалист по тестированию обучал других членов команды. После это, они разбились на пары и одну тройку для работы над автоматизацией тестирования параллельно. Далее произошло следующее: члены команды с опытом в разработке жаловались на трату дополнительных усилий из-за дублирований в тестах. До этого никто из них не замечал этого, и специалист по тестированию - не имевший достаточного опыта в разработки - никогда об это не заботился. Теперь вся команда была вовлечена и заботились об этом, и качество тестов улучшилось значительно.

### Удаляйте тесты, не добавляющие ценности

Тесты служат нескольким целям. Они выступают требованиями, проверкой и страхующей сетью, не допуская регресса системы.

Когда существующий тест уже больше не нужен - потому что он включён в другой тест - то удалите его. Сохранение ненужных тестов пользы не приносит, но увеличивает затраты на содержание и снижает скорость тестирования.

### Избегайте тестирования через пользовательский интерфейс

Пользовательские интерфейсы (UI) часто меняются. Запуск ваших тестов через пользовательский интерфейс делает их уязвимыми для этих изменений - даже в случае, когда в логике тестов изменений не было. Это увеличивает затраты на их сопровождение.

Следовательно, избегайте тестирования через пользовательский интерфейс, а вместо этого обращайтесь к приложению напрямую через программный интерфейс (API). Ещё одно преимущество состоит в том, что это ускорит ваши тесты, поскольку тестирование через пользовательский интерфейс выполняется медленно.

### Запускайте тесты часто

Много лет назад мы работали с большой продуктовой группой, следовавшей водопадному подходу разработки. Традиционный совет в сфере автоматизации тестирования состоит в том, чтобы выбрать и автоматизировать наиболее важные кейсы - силами отдельной команды автоматизации тестирования - после релиза. Они это сделали. К концу следующего релиза они запустили эти тесты... и они упали. Обновление тестов требует много времени, поэтому они решили провести всё тестирование вручную.

Запуск тестов единожды или дважды за релиз кажется эффективным - меньше процессорного времени будет потрачено - но больше будет изменений, и поэтому многие тесты могут упасть, что породит большую порцию работы по их исправлению. Напротив, частый запуск тестов - используя систему непрерывной интеграции - требует больше процессорного времени, но в результате мы получаем меньший объём работы в части поддержки тестов, поскольку сил на исправление упавших тестов требуется не так много. Если у вас большая загрузка по сопровождению тестов, то есть не мало шансов, что вы будете редко запускать эти тесты.

### Относитесь функциональным м нефункциональным требованиям одинаково

Автоматизация и непрерывный запуск нефункциональных тестов также важны. Перенос их на конец может означать сдвиг снижения одно из самых больших рисков туда, где его реализация принесёт больше всего вреда. Например, если требуется определённый уровень производительности системы, начните его раннее тестирование, чтобы также достичь его раньше, и непрерывно запускайте эти тесты, пока будет добавляться новая функциональность, чтобы убедиться в том, что система не деградирует по производительности от её целевого уровня.

К нефункциональным требованиям часто относятся по-особенному - люди верят, что их нельзя описать и протестировать. Это прискорбно. На воркшопе по уточнению, нефункциональные требования могут быть разобраны так же, как и функциональные, а также могут быть созданы тесты из примеров для их прояснения.

### Непрерывно выполняйте длительные тесты

Нефункциональные тесты часто не могут запускаться в системном цикле непрерывной интеграции, потому что они занимают много времени - тесты стабильности могут занимать до двух недель. В некоторых продуктовых группах их оставляют до релиза - создавая отложенный цикл обратной связи. Не самая хорошая идея.

Запускайте длительные тесты все время в медленном системном цикле непрерывной интеграции. Относитесь к ним также, как и к любым другим. Когда они падают, оповещайте всех, кто изменял код. После их прохождения получите последнюю сборку и запустите их заново. Таким способом цикл обратной связи будет на столько коротким, насколько мог бы быть.

### Используйте виртуализацию или контейнеризацию

В порядке ускорения тестов и экономии на аппаратном обеспечении максимизируйте использование инструментов для виртуализации, например [VirtualBox](https://www.virtualbox.org/) или [VMWare](http://www.vmware.com/). Альтернативой виртуальным машиным (которые не всегда быстро собираются и легко поддерживаются) являются виртуальные linux контейнеры, такие как [Docker](http://www.docker.io/).

### Избегайте использования коммерческих инструментов тестирования

Однажды мы консультировали компании, которая разрабатывала коммерческий инструмент для “автоматизации тестирования” - инструмент с графическим интерфейсом. В чем состоял их запрос? Научить их, как автоматизировать тестирование их инструмента, автоматизирующего тестирование...

Доступно огромное множество коммерческих инструментов. Мы редко встречали людей, которые по настоящем удовлетворены какими-либо из них. Большинство из них чрезмерно сложно и фокусируются на отчётности и ‘менеджменте‘, а не на автоматизации тестирования. Предпочтите свободные инструменты с открытым исходным кодом - созданные разработчиками для решения реальных проблем - коммерческим.

Список распространённых инструментов для автоматизации тестирования:

* [RobotFramework](http://www.robotframework.org/)
* [Cucumber](https://cucumber.io/)
* [Fitnesse](http://www.fitnesse.org/)
* [Selenium](http://www.seleniumhq.org/)
* [Capybara](https://github.com/jnicklas/capybara)

Выше всего лишь самый общий список, но каждый день появляются новые и новые инструменты.