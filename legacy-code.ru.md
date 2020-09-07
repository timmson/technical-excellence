# Унаследованный код

> Я не хочу достичь бессмертия с помощью своей работы, я просто не буду умирать. — Вуди Аллен

Если вы работаете в большой продуктовой группе, значит за время чтения этой статьи вы, вероятно, будете думать: “Это статья содержит столько полезных идей, но у нас пять миллионов строк кода на нашем доморощенном языке программирования, которые мы обязаны поддерживать. Это идеи не будут у нас работать”. В общем, это статья как раз для вас.

Существующий хорошо структурированный переиспользуемый код является ценным активом. Тем не менее, этот актив может стать плохо структурированным с неадекватной документацией унаследованным кодом (legacy code) с большим количеством повторений и без автотестов. Унаследованный код ограничивает организационную гибкость, и как мы увидим, ведёт к серьёзному конкурентному недостатку. Это статья о том, как писать такой унаследованный код, и как этого избегать.

Но перед погружением в тему будет нужно отметить, сколько работы существуют благодаря унаследованному коду. Мы путешествуем по миру и часто работаем в развивающихся странах. Там люди вышли из бедности благодаря рабочим местам, созданным для поддержки устаревшего кода. В таких странах, как Индия и Китай, несколько городов выросли в размерах и уровне жизни за последнее десятилетие не без помощи индустрии заказной разработки (outsourcing industry), и большая её часть относится к унаследованному коду. Это стоит отметить тоже. С другой стороны, что бы произошло, если бы всю эту энергию направили на творческие, инновационные продукты? Кроме того, унаследованный код разрушал компании...

![_](/img/legacy-code/browser-wars-en.png)

*Рынок и релизы браузеров*

Браузер Netscape - один из лучших примеров, который по началу *владел* рынком браузеров. Но в 1995 года компания Microsoft осознала громадный потенциал сети Интернет и начала то, что в последствии назовут “войнами браузеров“ [[см. книгу Competing On Internet Time](https://www.amazon.com/Competing-Internet-Time-Netscape-Microsoft/dp/0684863456)]. В 2000 году она выиграла первую битву браузеров.

Для этого было много причин. Одна из них в том, что Netscape [не выпускала](http://news.cnet.com/2100-1023-248549.html) новой версии своего браузера три с половиной года. Но почему? *“Потому что браузер был переписан заново, без использования кодовой базы, что формировала основу Netscape’s Communicator browser”*. В 2007 компания AOL, (которая купила Netscape в 1999 году) официально [убила](http://blog.netscape.com/2007/12/28/end-of-support-for-netscape-web-browsers) браузер Netscape.

Это статья решит все ваши проблемы с унаследованным кодом... хорошо, а может и нет. Но она сделает вашу проблему унаследованного кода немного менее болезненной и возможно, в один день, решённой.

## Как Писать Новый Унаследованный Код

Писать унаследованный код просто - мы объясним это за несколько простых шагов. Компании создают кучи унаследованного кода за одно десятилетие. В компании Xerox мы однажды услышали изречение: “Мы преподавали много уроков, не выучили мы несколько”. Это отчасти правда для унаследованного кода. Как предотвратить *преподавание* такого урока унаследованного кода снова и снова, который так и не бы выучен?  

Как долго он преподаётся? Ещё в 1967 году, возможно, в первой [книге](https://www.amazon.com/management-computer-programming-projects/dp/B0006BRZGU) о проектах по разработке ПО автор учил нас:

> В равной степени ответственным за начало проекта с заранее понятным провалом является руководство, которое настаивает на наличии фиксированных обязательств со стороны программистов до того, как последний поймёт, для чего эти обязательства. Слишком часто руководство не осознает, что, прося сотрудников о “невозможном”, сотрудники будут чувствовать себя обязанными ответить из уважения, страха или ошибочной лояльности. Чтобы сказать начальнику “нет”, часто требуется смелость, политическая и психологическая мудрость, а также деловая зрелость, которая приходит с большим опытом.

Ниже указаны чёткие причины унаследованного кода:

* нереалистичные сроки сдачи фиксированного объёма работ
* низкий уровень навыков разработки

И конечно в этих причинах лежат ключи к предотвращению унаследованного кода...

## Как Избежать Написания Унаследованного Кода

### Избегайте нереалистичных сроков сдачи фиксированного объёма работ

“Мы обещали передать этот релиз нашим ключевым клиентам, и ждём первое февраля, как *единственно приемлемые обязательства* от отдела разработки” - было написано в злом письме директора менеджменту продуктовой группы, которую мы консультировали. Мы недоверчиво прочитали это письмо и задались вопросом о *единственно приемлемых обязательствах*. Мы решили не обращать пока на него внимания и вернуться к *обычной* работе - обучению разработчика рефакторингу унаследованного компонента, который был сломан вместе с последним релизом, чтобы успеть к этому срок.

Много компаний застревают в порочном круге *навязанных обещаний* и *неосуществимых обязательств*. Сегодня в эру высоких скоростей клиенты ‘принуждают’ их обещать слишком многое. “Если вы не можете поставить к концу года, мы купим у вашего конкурента, кто даёт такое обещание”. Отдел продаж или руководство могли бы отреагировать, проявив прозрачность и стремясь к взаимовыгодным долгосрочным отношениям (сотрудничество с клиентами), но вместо этого они проверяют, является ли штраф в договоре за несоблюдение сроков приемлемым (переговоры по контракту) и отвечают: “Да, без проблем, мы это сделаем!”. После этого такой же цикл начинается внутри организации. Руководство приказывает главе разработки “сделать это” или “сделать так, чтобы это случилось”, потому что “это обещано клиентам”. Обещание путешествует по организационной структуре к разработчикам, которые не могут передать его дальше.

Как разработчики должны реагировать? [Чарльз Лехт](https://www.amazon.com/management-computer-programming-projects/dp/B0006BRZGU) (Charles Lecht) уже нас предупреждал более 40 лет назад: Разработчик будет *“чувствовать себя обязанными ответить из уважения, страха или ошибочной лояльности”* и неохотно соглашаются на предложенные сроки. Разработчик открывает свой *секретный ящик с инструментами* и делает всё возможное, чтобы успеть к ближайшему сроку, используя *инструменты*, такие, как зашитые в код данные (hardcoding), программирование методом скопировать-вставить-поправить (copy-paste-modify programming), отсутствие тестов, переработки и другие, разрушающие качество и срезающие углы практики [см. книгу The Enterprise and Scrum](https://www.amazon.com/Enterprise-Scrum-Developer-Best-Practices/dp/0735623376). Никто не замечает этих ‘инструментов’, и поэтому сроки соблюдены. Менеджмент награждает разработчиков за их тяжёлый труд и восхваляет их за “отличную командную работу” и “дух борьбы”.

Эти разрушающие качество и срезающие углы практики отражаются в плохом унаследованном коде, который замедляет разработку, и организация проигрывает конкуренцию. Предсказуемый сценарий. Им необходимо вернуть себе рынок и, следовательно, дать новые обещания, снова запуская порочный круг. **Технический долг** - унаследованный код, замедляющий разработку. **Долг обучения** - недостаток развития новых навыков у разработчиков усугубляет это замедление. Разработчики настолько заняты, давай неосуществимые обязательства, что у них нет времени поддерживать свои навыки в актуальном состоянии.

![_](/img/legacy-code/causal-loop-legacy-en.png)

*Динамика нереалистичных сроков*

Боб Мартин в книге *[Чистый Код](http://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)* утверждает, что мастера не давали бы таких невыполнимых обещаний, и проблема унаследованного кода могла быть решена обучением разработчиков, чтобы повысить их *профессионализм*.

Мартин частично прав. Но это представление игнорирует тот факт, что разработчик является частью большой системы, которая изменяет его поведение. Нужно, чтобы не только разработчики поменялись, но и *система* в целом, в которой они работают.

Однажды в Европе мы посетили директора большой продуктовой группы (которая разрабатывала встраиваемые системы) и его команду менеджеров. Директор объяснил, что группа успешно достигла цель в последнем релизе, и поставил под сомнение мотивацию для внедрения масштабируемого Скрама. В этот момент один из его менеджеров заговорил и сказал: “Что ж, на самом деле ближе к концу последнего релиза мы сильно отстали, поэтому мы много работали сверхурочно, вытащили более сотни человек из другого продукта и заставили их помочь. Вот почему мы выполнили поставку к сроку. Сейчас мы серьёзно отстаём от графика текущего релиза, потому что в последнем релизе было создано так много плохого кода, что мы тратим большую часть времени на исправление дефектов, о которых сообщают нам наши клиенты, и вынуждены работать с беспорядком в кодовой базе”.  

Обратите внимание на взаимосвязь между этими ситуациями и отсутствием бережливого мышления. Например, *потеря от выдачи желаемого за действительное* присутствует в этих случаях. Один из трёх источников потерь в бережливом мышлении - *перегрузка* (overburden) - легко увидеть, как героический толчок ближе к концу релиза приводит к ещё большим потерям в будущем. И тут также нет культуры *остановись и исправь* (stop and fix) - с точностью противоположная “продолжай и не исправляй”.

Сказать вашим клиентам “Мы не понимаем сути и понятия не имеем, когда это будет сделано будет” коммерческим суицидом. Но это беспокойство, которое мы часто слышим от руководителей, является ложной дихотомией - либо *брать на себя нереалистичные обязательства, либо вообще не брать на себя никаких обязательств*.

Есть альтернатива, когда клиент и заказчик вместе принимают реальность продуктовой разработки: Она не предсказуема на 95%. Вы можете принять эту реальность, если будете демонстрировать прозрачность по отношению к своим клиентам во время разработки. Например, ...

* отчитываясь о вашем статусе разработки вашим ключевым клиентам каждую итерацию; например, с помощью Диаграммы Сгорания Релиза (Release Burndown chart) и обновлённого Бэклога Продукта
* давая возможность ключевым клиентам оставлять обратную связь по приоритетам и изменении целей по мере того, как они видят, как идут дела, а затем корректируют план соответствующим образом
* предоставляя оценки с распределением вероятности или несколько оценок [см. книгу Вальсируя с Медведями](https://www.amazon.com/Waltzing-Bears-Managing-Software-Projects/dp/0932633609)
* используя другие техники, которые продвигают частое взаимодействие с клиентами, основанные на реальности и прозрачности

Благодаря изменениям, как продуктовые компании относятся к своим клиентам, уменьшается давление, создающее унаследованный код.

Обычный быстрый ответ менеджмента на давление рынка в ‘приказе’ разработке “добавить больше ресурсов”, пока они ‘дешёвые’. Мы работали с продуктовой группой, которую *принудили* набрать сотни людей за период в один-два года. Исключение? Нет, вот ещё пример: руководитель продуктовой группы, с которой мы работали, недавно был ‘повышен‘ до нового продукта. В новом продукте было 900 человек, 12 разных офисов и 20 активных филиалов. Этот продукт отставал от конкурентов, и предыдущее руководство пыталось спасти его, добавляя больше людей - теперь оно отставало ещё больше.

Вот другой урок, который *преподаётся* снова и снова. Возможно, первым крупномасштабным проектом в мире была [SAGE](https://en.wikipedia.org/wiki/Semi-Automatic_Ground_Environment) система, которая разрабатывалась в 1950-х. Проект торопился, поэтому...

> В течение года примерно **1000 человек** было вовлечено в разработку SAGE системы. Были набраны и обучены люди из самых разных слоёв общества. Проводники трамвая, сотрудники похоронного бюро (по крайней мере, с одним годом обучения математике), школьные учителя, чистильщики занавесок и другие были в спешном порядке собраны, обучены программированию в течение определённого количества недель и распределены по частям в очень сложной организации... Первоначально ожидаемые **мощности системы были значительно сокращены**. Система была впервые поставлена **с опозданием в год** и **значительно дороже**, чем ожидалось<sup>[1](#footnote-1)</sup>.

Вместо фокуса на выращивании великих разработчиков или найма небольшого количества крутых людей они сконцентрировались на найме максимального количества “голов” (англ. *heads*, *head count*) что, в свою очередь, приводит к поспешной и неадекватной образовательной программе для новых сотрудников. Это быстрое решение приводит к группам с низким средним уровнем навыков разработки, группам с низкой способностью быть хорошими разработчиками и, в конечном итоге, ко все большему и большему количеству плохого унаследованного кода.

### Низкие Навыки Разработчиков

Организационная динамика обещаний и обязательств полностью не описывает историю об унаследованном коде. Боб Мартин прав - индустрии определённо точно нужны хорошие инженеры.

Нам кажется, что средний уровень навыков разработчиков в больших продуктовых группах довольно низкий. Разработчики часто не знакомы с хорошими базовыми техниками - простыми практиками, таки как сокрытие и инкапсуляция, или принципы хорошего дизайна. При разработке встраиваемых систем мы иногда слышим восклицания “Это техники для ООП, а мы пишем на языке Си”, но их авторы не понимают, что некоторые из этих концептов были разработаны для не-объектно-ориентированных языков <sup>[2](#footnote-2)</sup>. Мы наблюдали следующий тренд

> Чем больше продуктовая группа, тем меньший объём знаний ‘современных’ практик разработки

Но эти практики являются основными для бесконечно [повторяемого процесса разработки](https://www.amazon.com/Sustainable-Software-Development-Agile-Perspective/dp/0321286081). К счастью, навыки разработки зависят не только от чистого таланта; они могут быть изучены и улучшены с помощью

* школ
* поддержки в организации
* самообучения

The leadership of a product group may believe they understand how these educational forums are working, but it may not be so...

**Школы** — Universities are not doing a good job in teaching basic skills to developers. There is a shocking gap between what is happening in industry and in universities. Many educators have never worked in industry and have not seen the long-term dynamics of development skills and legacy code. They also lack a Go See attitude. Some universities recently added agile development practices to their computer science curriculum. This is good. However, deep experience is required to really grasp agile practices such as testdriven development, and educators seldom have this experience.

As such, do not assume that university graduates have much skill in software development—especially in agile development.

**Поддержка в организации** — Most companies do a poor job at educating developers. We frequently hear, “Everybody who graduated from university can code,” thereby implying that educating basic development skills is unnecessary. Our coaching experiences suggest otherwise. Many developers in large product groups lack fundamental skills such as good design of software, efficiently working with editors, effectively using their programming language, or automating tasks by writing scripts. Organizations are failing to educate in these areas because many business leaders have reasonably but incorrectly assumed that people learned these skills at university—unaware that a computer science curriculum does not teach software development skills, and that most university professors do not know and cannot teach modern development practices<sup>[3](#footnote-3)</sup>.

In contrast, lean organizations invest in educating their employees. One study shows that Japanese lean companies spend eight times as much effort educating new employees than their USA counterparts and twice as much as their European counterparts [[WJR90](https://www.amazon.com/Machine-That-Changed-World-Revolutionizing/dp/0743299795)].

Organizations also fail to recognize the need for continuous improvement. They not only need to provide education in basic skills, they need to create an environment in which employees are constantly challenged and learning. How? Managers acting as teachers, peers educating one another (for example, by pair programming) and internal or external dedicated coaches—all supporting an environment of learning and continuous improvement.

**Самообучение** — Many developers do not keep themselves up to date. Quality guru Philip Crosby saw lack of knowledge caused by a shortage of learning as a main cause of bad quality.

> People subconsciously retard their own intellectual growth. They come to rely on cliches and habits. Once they reach the age of their own personal comfort with the world, they stop learning and their mind runs on idle for the rest of their days. They may progress organizationally, they may be ambitious and eager, and they may even work night and day. But they learn no more. [[Crosby80](https://www.amazon.com/Quality-Free-Certain-Becomes-Business/dp/0070145121)]

In 1999, Dave Thomas and Andy Hunt published an excellent book, *The Pragmatic Programmer* [[HT99](http://www.amazon.com/Pragmatic-Programmer-Journeyman-Master/dp/020161622X)], summarizing the attitude and behavior of a modern, professional developer. We encourage people to read this, and more broadly, to take responsibility for keeping up to date.

### Избегайте тривиализации разработки

“*I’m an architect, writing code is something the low-level implementation people do.*” We hear statements such as this from ivory-tower architects who consider programming to be beneath them. The organization for which this architect works has created a culture of trivializing programming. Such a culture de-emphasizes code, devalues writing clean code, and devalues learning about programming. In such a culture people want to rise in the social and organizational hierarchy—and that means move away from programming. Coding is just the early career phase that they have to go through. Such a culture is one that gives rise to legacy code.

Организации тривилизируют разработку с помощью:

* outsourcing the programming
* career paths
* salary differences

**Outsourcing the programming** — Especially in  large  product groups, we encounter businesses that do not consider writing code their “core business” and so have outsourced it. They write specifications, architectural documents, and design documents, and then send them to cheap-rate developers offshore to “do the implementation and testing.” A recipe for disaster. The source code is the place of real value—gemba. For more, see:

* [“Выращивание”, а не “строительство” - Создавайте культуру живого, растущего дизайна системы”](architecture-design.ru.md#выращивание-а-не-строительство---создавайте-культуру-живого-растущего-дизайна-системы)
* [“Архитекторы и системные инженеры являются постоянными членами фиче-команд”](architecture-design.ru.md#архитекторы-и-системные-инженеры-являются-постоянными-членами-фиче-команд)
* [“Избегайте архитектурных астронавтов (PowerPoint-архитекторов)”](architecture-design.ru.md#избегайте-архитектурных-астронавтов--powerpoint-архитекторов)
* [“Не позволяйте архитекторам просто “передавать” требования конечным разработчикам”](architecture-design.ru.md#не-позволяйте-архитекторам-просто-передавать-требования-конечным-разработчикам)
* [“Избегайте создания ‘дизайна’ и последующей отправки его в оффшор для реализации”](architecture-design.ru.md#избегайте-создания-дизайна-и-последующей-отправки-его-в-оффшор-для-реализации)

**Career paths** — Large organizations want to offer a future for their employees; predefined management or technical career paths are a typical solution. People who follow the management path shift away from technical work and become “professional managers.” Those who follow the technical path spend their time writing “architectural documents.” Whatever career path you follow, it won’t contain any programming.

Salary differences—Of all software-development-related jobs, the salary of programmers is, on average, among the lowest [[Jones08](https://www.amazon.com/Applied-Software-Measurement-Analysis-Productivity/dp/0071502440)]. Naturally but unfortunately, these salary differences do not promote becoming a better developer but instead promote stopping work as a developer. Is there an alternative? Pete McBreen promotes a model of software craftsmanship in which salary is directly linked to skill. Development skill is measured by a developer’s portfolio and peer references [[McBreen01](https://www.amazon.com/Software-Craftsmanship-Imperative-Pete-McBreen/dp/0201733862)].

## Try... Raise awareness of the negative impact of legacy code

More *legacy* code is more than a liability, it’s a *boat anchor*. It is hard to deliver value fast and adapt quickly when your massive 15 million lines of code is a steaming pile of...  well, you know.

Some developers and many nontechnical people in product development do not grasp the negative impact of legacy code—in terms of cost servicing this technical debt and in terms of opportunities lost because of degradation of speed and ability to change.

We encourage technical leaders to proactively educate their business and technical community on this issue, and to explore the cost of legacy code.

## Ok, I’ve Got Legacy, Now What

You probably recognize these causes of legacy code, but you already have piles of it. How to get rid of it? In *Working Effectively with Legacy Code* [[Feathers04](http://www.amazon.com/Working-Effectively-Legacy-Michael-Feathers/dp/0131177052)], Michael Feathers provides concrete codelevel techniques for gradually improving your code. This chapter does not repeat these; we recommend Feathers’s book. But we do cover some general strategies for dealing with legacy code.

### Avoid... Rewriting legacy code

When confronted with legacy code, developers frequently suggest rewrite, redesign, or rearchitect—scrap the legacy and write it again. Next time it will be better...  Resist that temptation. Why?

In a product group with a 30-year-old code base, a developer asked us if we could help refactor a 5000-line function. We thought he was exaggerating. But when we paired up and measured the function, we discovered it was slightly larger than 5000 lines of code (LOC). How are 5000 LOC functions created? Does a developer wake up and think, “Gosh, what a wonderful day today! Let’s write a 5000 LOC function?” Probably not. When a developer writes new code, he usually *will* write it with decent quality. But over time the quality degrades. A function *becomes* 5000 LOC. Why does this happen? The customer requests a new requirement and this is hacked in because of poor development skills or unrealistic schedules. Code quality goes down and the effort needed to make changes goes up (see Figure 3).

![Figure 3. Code quality decreases over time](/img/legacy-code/code-quality1-en.png)

After some time it is too painful and takes too much effort to make changes to the code; developers start asking for a rewrite. At first the Product Owner refuses—a rewrite means high cost without new value. But as development speed drops, developers complain more, and eventually the Product Owner ‘agrees’ to the rewrite. During the rewrite, the ability to respond to changes—new requirements— is zero. But after the rewrite the code is of high quality, and consequently, new development is fast (see Figure 4).

![Figure 4. Rewrite Increases Code Quality](/img/legacy-code/code-quality2-en.png)

After the rewrite is finished, what happens? Pressure to rush in new requirements leads to hacks in the freshly cleaned code, causing the quality to degrade again and the implementation effort to increase (Figure 5). After a while, developers demand another rewrite. In some large product groups, we have seen components being rewritten three times.

![Figure 5. Code Base Quality Degrades Again After The Rewrite](/img/legacy-code/code-quality3-en.png)

---
Key insight: The problem is not having legacy code, it is creating legacy code.

---

The focus needs to be on preventing the creation of new legacy code instead of on the legacy code itself. It needs to be on *growing code healthfully* instead of allowing it to degrade over time. How? Improve the code every time a change is made. *“If we all checked-in our code a little cleaner than when we checked it out, the code simply could not rot”* [[Martin08](http://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)] (see Figure 6).

![Figure 6: Growing the Code Healthfully](/img/legacy-code/code-quality4-en.png)

## Try... Clean up your neighborhood

Growing healthy code is a key strategy for eliminating legacy code. You can do so by cleaning up your neighborhood; by gradually fixing your “broken windows” [[HT99](http://www.amazon.com/Pragmatic-Programmer-Journeyman-Master/dp/020161622X)]. Every time you make a change, look around your change point—the neighborhood—for code that can be improved—the broken windows—and add a couple of tests and refactor (see Figure 7). When starting this practice, every change is a little slower. But over time the code improves and the development speed increases because of the healthier code base.

![Figure 7: Clean Up Your Neighborhood](/img/legacy-code/clean-neighbourhood-en.png)

Having legacy code means having technical debt—and it costs to get out of debt. A rewrite strategy attempts to settle the debt all at once. On the other hand, cleaning up your neighborhood distributes the payments. It focuses the effort to the parts that change most—the most important ones. The legacy code that does not change does not get improved—and that is okay.

### Try... Write both high-level and unit tests

We are frequently asked whether to start with unit tests or highlevel tests. Another false dichotomy. They are both important! It is often easier to add high-level tests to a legacy code base, and they help in ensuring that existing functionality works. But unit tests run fast. Fast-running unit tests help when you are gradually refactoring legacy code. Therefore, write unit tests *and* high-level tests when cleaning up your neighborhood.

### Try... Rewrite lethal legacy code

Sometimes it is impossible to gradually grow the code base healthfully. For example, suppose that part of the low-level code is written in PL/M and no one is willing to learn PL/M. Or, part of your code base is written in a home-grown language, whose compiler only runs on VAX/VMS. When gradual change is impossible<sup>[4](#footnote-4)</sup> — the legacy is lethal—then it is necessary to ‘amputate’ that part of the code instead of letting it kill your product [Parnas94 - Parnas, D., 1994. “Software Aging,” Proceedings of the 16th International Conference on Software Engineering, also in [HW01](https://www.amazon.com/Software-Fundamentals-Collected-Papers-Parnas/dp/0201703696)].

While replacing lethal code:

* cover it with test
* do not add functionality to the old code
* do not add functionality to the replacement code

## Заключение

There are billions of lines of legacy code in the world, and the total is increasing every day. This has created massive problems (for example, Y2K), and it will still create monumental ones in the future. But egacy code will not disappear unless the root causes are tackled:

* unrealistic deadlines with fixed content
* poor developer skills

These can be solved by educating people in the causes of legacy code and by improving developer education. However, the industry has failed to recognize these causes for decades. It is not likely to change in the next few years.

How to deal with existing legacy code? It is better to gradually improve the code than to replace it. This requires investing in development skills and applying modern practices such as test-driven development. The only way to grow better code is to develop excellent people. This is a theme in lean thinking.

> Making things is about making people. [[Kato06 - Kato, I., 2006. Summary Notes from Art Smalley Interview with Mr. Isao Kato](http://artoflean.com/documents/pdfs/Mr_Kato_Interview_on_TWI_and_TPS.pdf)]

## Рекомендуем к Прочтению

At the time we write this book, surprisingly little has been written about such a huge and costly problem as legacy code. Here are some references we found useful related to improving your code gradually:

* Working Effectively with Legacy Code, by Michael Feathers. Concrete advice on how to gradually improve your legacy system at code level.
* Refactoring: Improving the Design of Existing Code, by Martin Fowler. The classic work on improving existing code.
* Refactoring Workbook, by Bill Wake. A concrete guide for becoming better at refactoring code.
* Refactoring to Patterns, by Joshua Kerievsky. In this book, Joshua explains how to gradually refactor your code to standard, robust design patterns.
* Refactoring in Large Software Projects,  by Stefan  Roock  and Martin Lippert. Large systems might need large refactorings. This book explains how to do these in as small steps as possible
so that your systems stays stable.

The following material covers the organizational dynamics behind legacy code:

* Enterprise Scrum, by Ken Schwaber. Chapter 9 of Enterprise Scrum is one of the few descriptions explaining the relationship between customer promises and the creation of legacy
code.
* Sustainable Software Development: An Agile Perspective, by Kevin Tate. This book does not cover many new techniques but provides an excellent overview of the practices for creating software in a sustainable way.

Software craftsman prevent creating legacy code and hence develop software at a sustainable rate. Some material on being a software craftsman:

* The Pragmatic Programmer: From Journeyman to Master, by Andrew Hunt and Dave Thomas. Classic book on modern software craftsmanship.
* Software Craftsmanship, by Pete McBreen dives in craftsmanship approach and compares it to the traditional software engineering perspective.
* Agile Development, Principles, Patterns and Practices, by Bob Martin. Also known as Agile PPP, links good  code, modern practices, and eternal design principles to explain what it means to be a craftsman.
* Clean Code: A Handbook of Agile Craftsmanship, by Bob Martin. The subtitle says it all. Clean Code is the code-focused prequel to Agile PPP

## Сноски

1. <a name="footnote-1"></a> статья Дж. Шварфца “Построение ПО: Проблемы и Практики” (J. Schwartz, Constructing of Software: Problems and Practices), позже опубликованная в [книге](http://www.amazon.com/Practical-Strategies-Developing-Software-Systems/dp/0201029774)), жирный шрифт добавлен.
2. <a name="footnote-2"></a> Например, статья Д. Парнаса (D. Parnas) [“O критериях декомпозиции систем на модули”](https://www.win.tue.nl/~wstomv/edu/2ip30/references/criteria_for_modularization.pdf).
3. <a name="footnote-3"></a> “Use your editor” is perhaps the most productivity increasing course you can give in many companies.
4. <a name="footnote-4"></a> It is rarely impossible to do a gradual change. Therefore, challenge each time someone says that a gradual change is not possible.
