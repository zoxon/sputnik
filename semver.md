# Семантическое Версионирование

## Кратко

Учитывая номер версии МАЖОРНАЯ.МИНОРНАЯ.ПАТЧ, следует увеличивать:

* МАЖОРНУЮ версию, когда сделаны обратно несовместимые изменения API.
* МИНОРНУЮ версию, когда вы добавляете новый функционал, не нарушая обратной совместимости.
* ПАТЧ-версию, когда вы делаете обратно совместимые исправления.

Дополнительные обозначения для предрелизных и билд-метаданных возможны как дополнения к МАЖОРНАЯ.МИНОРНАЯ.ПАТЧ формату.

## Зачем использовать семантическое версионирование?

Это не новая или революционная идея. Вероятно, вы уже используете что-то подобное. Проблема в том, что «подобное» — не достаточно хорошо. Без соответствия формальной спецификации, номера версий практически бесполезны для управления зависимостями. Ясно определив и сформулировав идею версионирования, становится легче сообщать о намерениях пользователям вашего ПО. Когда эти намерения ясны, гибки (но не слишком), спецификации зависимостей наконец могут быть созданы.

Простой пример демонстрирует, как Семантическое Версионирование может сделать «ад зависимостей» вещью из прошлого. Представим библиотеку, названную «Firetruck». Она требует Семантически Версионированный пакет под названием «Ladder». Когда Firetruck был создан, Ladder был 3.1.0 версии. Так как Firetruck использует функционал версии 3.1.0, вы спокойно можете объявить зависимость от Ladder версии 3.1.0, но менее чем 4.0.0. Теперь, когда доступен Ladder 3.1.1 и 3.2.0 версии, вы можете интегрировать его в вашу систему и знать, что он будет совместим с текущим функционалом.

Как ответственный разработчик, вы, конечно, хотите быть уверены, что все обновления функционируют как заявлено. В реальном мире полный бардак и ничего нельзя с этим поделать. Что вы можете сделать — это дать Семантическому Версионированию предоставить способ выпуска релизов без выпуска новых версий зависимых пакетов и сохранить вам время и нервы.

Если это звучит соблазнительно, всё что вам нужно — это начать использовать Семантическое Версионирование, объявить, что вы его используете, и следовать правилам. Добавьте ссылку на этот сайт в вашем README, тогда пользователи будут знать правила и извлекать из этого пользу.

## FAQ

* **Что я должен делать с ревизиями в 0.y.z на начальной стадии разработки?**

  Самое простое — начать разработку с 0.1.0 и затем увеличивать минорную версию для каждого последующего релиза.

* **Как я узнаю, когда пора делать релиз 1.0.0?**

  Если ваше ПО используется на продакшене, оно, вероятно, уже должно быть версии 1.0.0. Если у вас стабильный API, от которого зависят пользователи, версия должна быть 1.0.0. Если вы беспокоитесь за обратную совместимость, вероятно, версия вашего ПО уже 1.0.0.

* **Не препятствует ли это быстрой разработке и коротким итерациям?**

  Мажорная версия 0 как раз и означает быструю разработку. Если вы изменяете API каждый день, вы должны быть на версии 0.y.z или на отдельной ветке разработки работать над следующей главной версией.

* **Даже если малейшие обратно несовместимые изменения в публичном API требуют выпуска новой главной версии, не закончится ли это тем, что очень скоро версия станет 42.0.0?**

  Это вопрос ответственной разработки и предвидения. Несовместимые изменения не должны быть представлены как незначительные в ПО, имеющем много зависимого кода. Стоимость обновления может быть велика. Практика увеличения главных версий релизов с обратно несовместимыми изменениями означает, что вам придётся думать о последствиях ваших изменений и учитывать соотношение цена/качество.

* **Документирование всего API — слишком много работы!**

  Это ваша ответственность, как профессионального разработчика, правильно документировать ПО, предназначенное для широкого использования. Управление сложностью ПО очень важная часть поддержки высокой эффективности проекта. Это тяжело сделать, если никто не знает, как использовать ваше ПО или какой метод можно вызывать безопасно. В долгосрочной перспективе Семантическое Версионирование и настойчивость в качественном документировании публичного API поможет всем и всему работать слаженно.

* **Что мне делать, если я случайно зарелизил обратно несовместимые изменения как минорную версию?**

  Как только вы поняли, что нарушили спецификации Семантического Версионирования, исправьте проблему и выпустите новую минорную версию, которая исправляет проблему и восстанавливает обратную совместимость. Даже в таких обстоятельствах неприемлемо модифицировать уже выпущенные релизы. Если это необходимо, укажите в документации о нарушении обратной совместимости, версионирования и проинформируйте ваших пользователей, чтобы они знали о нарушении порядка версий.

* **Что я должен делать, если я обновляю свои собственные зависимости без изменения публичного API?**

  Это можно рассматривать как совместимые изменения, так как они не влияют на публичный API. ПО, которое явно зависит от тех же зависимостей что и ваш пакет, должно иметь собственные спецификации зависимостей и автор будет уведомлен о возможных конфликтах. Являются ли данные изменения уровня патча или минорного уровня, зависит от того, обновили ли вы свои зависимости чтобы исправить баг или реализовать новый функционал. В последнем случае, как правило, добавляется некоторое количество дополнительного кода и как следствие, увеличивается минорная версия.

* **Что если я нечаянно изменил публичный API в несоответствии с изменением номера версии (т.е. код содержит обратно несовместимые изменения в патч-релизе)?**

  На ваше усмотрение. Если у вас огромная аудитория, которая будет поставлена перед фактом возвращения прежнего поведения API, то лучше выпустить новый релиз с увеличением главной версии, даже несмотря на то, что фикс содержит исправления уровня патча. Запомните, в Семантическом Версионировании номера версий изменяются строго следуя спецификации. Если эти изменения важны для ваших пользователей, используйте номер версии, чтобы информировать их.

* **Что делать с устаревшим функционалом?**

  Объявление функционала устаревшим — это обычное дело в ходе разработки и часто необходимо для продвижения вперёд. Когда вы объявляете устаревшим часть публичного API, вы должны сделать две вещи: (1) обновить вашу документацию, чтобы дать пользователям узнать об этом изменении; (2) выпустить новый релиз с увеличением минорной версии. Прежде чем вы полностью удалите устаревший функционал в релизе с увеличением главной версии, должен быть как минимум один минорный релиз, содержащий объявление функционала устаревшим, чтобы пользователи могли плавно перейти на новый API.

* **Есть ли в SemVer лимиты на длину строки версии?**

  Нет, но руководствуйтесь здравым смыслом. 255 символов в строке версии, пожалуй, перебор. Кроме того, определенные системы могут предъявлять свои собственные ограничения на размер строки.

## Ссылки

* [semver.org](http://semver.org/lang/ru/)
