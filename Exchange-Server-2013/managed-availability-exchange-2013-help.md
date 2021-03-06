﻿---
title: 'Управляемая доступность: Exchange 2013 Help'
TOCTitle: Управляемая доступность
ms:assetid: ceb99e6f-6dca-446d-abfb-3e6fc6a72704
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dn482056(v=EXCHG.150)
ms:contentKeyID: 59890407
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Управляемая доступность

 

_**Применимо к:**Exchange Online, Exchange Server 2013 SP1_

_**Последнее изменение раздела:**2017-03-29_

Удобные возможности работы с электронной почтой всегда были основной целью администраторов систем обмена сообщениями. Чтобы добиться доступности и надежности вашей организации Microsoft Exchange Server 2013, следует активно отслеживать все аспекты системы и быстро устранять обнаруженные проблемы. В предыдущих версиях Exchange для мониторинга важных системных компонентов обычно использовалось внешнее приложение, например Microsoft System Center 2012 Operations Manager, которое собирало данные и позволяло устранять найденные проблемы после анализа полученной информации. В Exchange 2010 и предыдущих версиях использовались манифесты работоспособности и модули корреляции в форме пакетов управления. Эти компоненты позволяли Operations Manager определить, исправен ли тот или иной компонент. Кроме того, Operations Manager также использовал инфраструктуру командлетов диагностики, встроенную в Exchange 2010, для выполнения искусственных транзакций в разных компонентах системы.

Exchange 2013 использует новый подход для мониторинга и поддержки работы пользователей, применяя компонент *управляемой доступности*, который предоставляет встроенные операции мониторинга и восстановления.

## Управляемая доступность

Управляемая доступность, которую также называют *активным мониторингом* или *локальным активным мониторингом* — это интеграция встроенных операций мониторинга и восстановления с платформой высокой доступности Exchange. Она создана для обнаружения проблем и восстановления после них сразу после их возникновения и обнаружения системой. В отличие от предыдущих решений и методов мониторинга для Exchange функция управляемой доступности не пытается определить основную причину проблемы или уведомить о ней пользователей. Она сконцентрирована на восстановлении, а именно на трех ключевых аспектах работы пользователей:

  - **Доступность** — доступна ли служба для пользователей?

  - **Задержка** — могут ли пользователи нормально использовать службу?

  - **Ошибки** — могут ли пользователи выполнять поставленные задачи?

Из-за консолидации ролей сервера и других архитектурных изменений в Exchange 2013 необходимо использовать новый подход к методам мониторинга и модели работоспособности, применяемой в предыдущих версиях Exchange. Функция управляемой доступности позволяет использовать эти изменения, предоставляя встроенное решение для мониторинга и восстановления работоспособности. Она отходит от наблюдения за отдельными срезами системы, выполняя сквозное наблюдение за работой пользователей и защищая работу конечных пользователей путем ориентированных на восстановление вычислений.

Управляемая доступность — это внутренний процесс, выполняемый на каждом сервере Exchange 2013. Он каждую секунду опрашивает и анализирует сотни метрик работоспособности. Если что-то не так, то в большинстве случаев проблема будет исправлена автоматически. Но всегда будут неполадки, которые функция управляемой доступности не сможет устранить самостоятельно. В этих случаях управляемая доступность передает ошибку на обработку администратору с помощью журнала событий.

Управляемая доступность реализуется в форме двух служб:

  - **Служба диспетчера работоспособности Exchange (MSExchangeHMHost.exe)**   Это процесс-контроллер, используемый для управления рабочими процессами. Он используется для построения, выполнения, запуска и остановки рабочих процессов по мере необходимости. Он также используется для восстановления рабочих процессов при сбоях, чтобы рабочие процессы не становились единственной точкой отказа.

  - **Рабочий процесс диспетчера работоспособности Exchange (MSExchangeHMWorker.exe)**. Этот рабочий процесс отвечает за задачи времени выполнения в инфраструктуре управляемой доступности.

Управляемая доступность использует постоянное хранилище для выполнения своих функций:

  - XML-файлы в папке \\bin\\Monitoring\\config используются для хранения параметров конфигурации некоторых рабочих элементов зондов и мониторов.

  - Active Directory используется для хранения глобальных переопределений.

  - Реестр Windows используется для хранения данных времени выполнения, например закладок, и локальных переопределений (для определенного сервера).

  - Инфраструктура журнала событий красного канала Windows используется для хранения результатов рабочих элементов.

  - Почтовые ящики работоспособности используются для операций зондов. Для каждой базы данных почтовых ящиков на сервере создается несколько почтовых ящиков работоспособности.

Как показано на следующем рисунке, управляемая доступность содержит три главных асинхронных компонента, которые непрерывно выполняют работу.

**Компоненты управляемой доступности**

![Управляемая доступность в Exchange Server 2013](images/Dn482056.7a54dcb5-1e28-4bd4-87e6-0d496b4ab796(EXCHG.150).gif "Управляемая доступность в Exchange Server 2013")

Первый компонент называется *зондом*. Зонды отвечают за измерения на сервере и сбор данных. Результаты этих измерений поступают во второй компонент — *монитор*. Монитор содержит всю используемую системой бизнес-логику на основе того, что считается работоспособным состоянием собранных данных. Подобно подсистеме распознавания шаблонов, монитор ищет различные шаблоны среди всех собранных измерений, а затем принимает решение, можно ли считать компонент работоспособным. Наконец, *ответчики* предпринимают действия по восстановлению и эскалации. Если что-то не работает, первое действие — попытка восстановления соответствующего компонента. Это могут быть действия по многоуровневому восстановлению (например, сначала последовательно перезапускаются пул приложений, служба и сервер, а в самом конце сервер переводится в автономный режим и не может принимать трафик). Если действия по восстановлению не помогают, система уведомляет о проблеме оператора-человека через журнал.

Существует три основных категории зондов: повторяющиеся зонды, уведомления и проверки. Повторяющиеся зонды — это выполняемые системой искусственные транзакции по тестированию работы пользователей. Проверки представляют собой инфраструктуру, которая собирает данные о работе, включая пользовательский трафик, и проверяет собранные данные на соответствие порогам, установленным для определения пиков среди ошибок пользователей. Благодаря этому инфраструктура проверок узнает о том, когда у пользователей происходят ошибки. Наконец, логика уведомлений позволяет системе в случае критического события незамедлительно принять меры и не ждать результатов данных, собранных пробой. Это типичные исключения или условия, которые могут быть обнаружены и распознаны без большого набора образцов.

Повторяющиеся зонды выполняются каждые несколько минут и проверяют некоторые аспекты работоспособности службы. Они могут передавать сообщения электронной почты через службу Exchange ActiveSync в почтовый ящик мониторинга, подключаться к конечной точке RPC или проверять возможность подключения для клиентского доступа к почтовому ящику.

Все зонды определяются при запуске службы диспетчера работоспособности в красном канале Microsoft.Exchange.ActiveMonitoring\\ProbeDefinition. Определения каждого зонда обладают множеством свойств, самые важные из которых перечислены ниже:

  - **Name**. Имя зонда, которое начинается с параметра *SampleMask* его монитора.

  - **TypeName**. Код типа объекта зонда, который содержит его логику.

  - **ServiceName**. Имя настроек работоспособности, в которые входит этот зонд.

  - **TargetResource**. Объект, проверяемый зондом. При выполнении он добавляется к имени зонда для получения результата зонда, *ResultName*.

  - **RecurrenceIntervalSeconds**. Частота выполнения зонда.

  - **TimeoutSeconds**. Время ожидания зонда до появления ошибки.

Существуют сотни повторяющихся зондов. Большинство из них создаются для отдельных баз данных, поэтому их количество растет с числом баз данных. Большинство зондов определяются в коде, поэтому их невозможно обнаружить напрямую.

В основе повторяющихся зондов лежит запуск через равные промежутки времени (*RecurrenceIntervalSeconds*) и проверка (или зондирование) некоторых аспектов работоспособности. Если компонент работоспособен, зонд записывает информационное событие в канал Microsoft.Exchange.ActiveMonitoring\\ProbeResult с параметром *ResultType*, имеющим значение 3. Если происходит ошибка проверки или истекает время ожидания, зонд выдает ошибку и записывает сообщение об ошибке в тот же канал. Значение 4 параметра *ResultType* означает, что произошла ошибка проверки, а значение 1 параметра *ResultType* указывает на истечение времени ожидания. В случае истечения времени ожидания большинство зондов выполняются повторно до достижения значения свойства *MaxRetryAttempts*.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Примечание.</strong> Красный канал ProbeResult может быть занят сотнями зондов, которые выполняются каждые несколько минут и записывают события в журнал. Это может существенно повлиять на производительность сервера Exchange при создании ресурсоемких запросов для журналов событий в производственной среде.</td>
</tr>
</tbody>
</table>


Уведомления — это зонды, которые выполняет не инфраструктура диспетчера работоспособности, а некоторые другие службы на сервере. Эти службы проводят собственный мониторинг, а затем передают их данные в инфраструктуру управляемой доступности, напрямую записывая результаты зондов. Эти зонды не отображаются в канале ProbeDefinition, поскольку в нем описываются только зонды, выполняемые инфраструктурой управляемой доступности. Например, монитор ServerOneCopyMonitor активируют результаты зонда, записанные службой MSExchangeDAGMgmt. Эта служба выполняет собственный мониторинг, определяет наличие проблемы и записывает в журнал результаты зонда. Большинство зондов-уведомлений могут записывать в журнал как красные события (указывают на неработоспособный монитор), так и зеленые (возобновление работоспособности монитора).

Проверки — это зонды, которые записывают в журнал события, только когда счетчик производительности становится больше или меньше порогового значения. На самом деле они представляют особый случай зондов-уведомлений, так существует служба, которая отслеживает счетчики производительности на сервере и записывает события в журнал канала ProbeResult, если достигнуто заданное пороговое значение.

С помощью монитора для этой проверки можно определить счетчик и пороговое значение, которые считаются неработоспособными. За зондом-проверкой следят мониторы типа *Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueAboveThresholdMonitor* или *Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueBelowThresholdMonitor*.

Мониторы отправляют запросы данным, собранным пробами, чтобы определить, требуются ли действия на основании предварительно определенного набора правил. В зависимости от правила или природы ошибки монитор может инициировать отвечающее устройство или передать ошибку на обработку человеку, выполнив запись в журнале событий. Кроме того, мониторы определяют, через какой период времени должно сработать отвечающее устройство и рабочий процесс действий восстановления. Мониторы имеют различные состояния. С точки зрения состояния системы мониторы имеют два состояния:

  - **Работоспособный:** монитор работает надлежащим образом и все собранные метрики имеют нормальные параметры работы

  - **Неработоспособный:** монитор не является работоспособным и инициировал процесс восстановления через отвечающее устройство или уведомил администратора путем эскалации ошибки.

С точки зрения администратора мониторы имеют дополнительные состояния, которые отобразятся в PowerShell:

  - **Ухудшенная производительность.** Если монитор пребывает в неработоспособном состоянии от 0 до 60 секунд, его производительность считается ухудшенной. Если монитор пребывает в неработоспособном состоянии дольше 60 секунд, он считается неработоспособным.

  - **Отключенный:** монитор явно отключен администратором.

  - **Недоступный:** служба работоспособности Microsoft Exchange периодически отправляет запросы каждому монитору для определения его состояния. Если служба не получает ответ на запрос, состояние монитора изменяется на "Недоступный".

  - **Восстановление:** данное состояние устанавливается администратором и означает, что в данный момент сотрудник выполняет корректирующие действия. Это позволяет системе и людям отличать эту ошибку от других ошибок, которые могут произойти во время выполнения корректирующих действий (например, операция повторного заполнения копии базы данных).

В определении каждого монитора есть свойство *SampleMask*. В процессе работы монитор ищет в канале ProbeResult события со свойством *ResultName*, которое соответствует свойству *SampleMask* монитора. Эти события могут происходить из повторяющихся зондов, уведомлений или проверок. Если достигнуто пороговое значение монитора, он становится неработоспособным. С точки зрения монитора все три типа зондов одинаковые, ведь каждый из них создает записи в журнале канала ProbeResult.

Следует отметить, что сбой одного зонда не всегда указывает на проблемы с сервером. Мониторы созданы для того, чтобы правильно определять наличие реальных проблем, которые необходимо исправлять. Потому многие мониторы становятся неработоспособными только после достижения порогового значения количества повторяющихся сбоев зондов. И даже в этом случае ответчики могут автоматически исправить большинство проблем. Потому отслеживать проблемы, которые требуют личного вмешательства, лучше в красном канале Microsoft.Exchange.ManagedAvailability\\Monitoring. В нем отображаются самые новые ошибки зондов.

Как следует из их названия, ответчики реализуют определенный ответ на оповещение от монитора. Ответчики выполняют различные действия восстановления, например сбрасывают рабочий пул приложений или перезапускают сервер. Существует несколько видов ответчиков:

  - **Ответчик перезапуска** — завершает и перезапускает службу.

  - **Ответчика сброса пула приложений** — останавливает и перезапускает пул приложений в службах IIS.

  - **Ответчик отработки отказа** — инициирует отработку отказа базы данных или сервера.

  - **Ответчик критической ошибки** — инициирует критическую ошибку сервера, приводящую к его перезагрузке.

  - **Автономный ответчик** — отключает протокол на сервере (отклоняет запросы клиентов).

  - **Оперативный ответчик** — активирует протокол на сервере (принимает запросы клиентов).

  - **Ответчик эскалации** — передает проблему администратору с помощью журнала событий.

Помимо указанных ответчиков у некоторых компонентов также есть специализированные уникальные ответчики.

Все ответчики поддерживают регулирование, что дает вам встроенный механизм для контроля их действий. Регулирование позволяет добиться того, что система не будет скомпрометирована или не выйдет из строя в результате операций восстановления ответчика. Все ответчики регулируются одинаково. При регулировании действие восстановления ответчика может быть пропущено или отложено в зависимости от действия. Например, когда ответчик регулируется ответчик критической ошибки, его действие пропускается, а не задерживается.

## Настройки работоспособности

С точки зрения отчетности управляемая доступность реализует два представления работоспособности: внутреннее и внешнее. Внутреннее представление использует *настройки работоспособности*. Каждый компонент в Exchange 2013 (например, Outlook Web App, Exchange ActiveSync, служба банка данных, индексация контента, службы транспорта и т. д.) отслеживаются компонентом управляемой доступности с помощью зондов, мониторов и ответчиков. Группа зондов, мониторов и ответчиков для определенного компонента называется *настройками работоспособности*. Настройка работоспособности — это группа зондов, мониторов и ответчиков, определяющих, исправлен ли компонент. Текущее состояние настроек работоспособности (т. е. исправно или неисправно) определяется на основе состояния мониторов настроек работоспособности. Если все мониторы исправны, настройки работоспособности также исправны. Если какой-то монитор неисправен, состояние настроек работоспособности определяется по наименее работоспособному монитору.

Подробные инструкции для просмотра работоспособности сервера или состояния настроек работоспособности см. в статье [Управление настройками работоспособности и работоспособностью сервера](manage-health-sets-and-server-health-exchange-2013-help.md).

## Группы работоспособности

Внешнее представление управляемой доступности состоит из *групп работоспособности*. Группы работоспособности доступны для System Center Operations Manager 2007 R2 и System Center Operations Manager 2012.

Существует четыре основных группы работоспособности:

  - **Точки соприкосновения с пользователями.** Компоненты, которые влияют на взаимодействие с пользователями в реальном времени, например протоколы или банк данных.

  - **Компоненты служб.** Компоненты без прямого взаимодействия с пользователями в реальном времени, например служба репликации почтовых ящиков Microsoft Exchange или процесс создания автономной адресной книги (OABGen)

  - **Серверные компоненты.** Физические ресурсы сервера, например место на диске, память и сетевые компоненты.

  - **Доступность зависимостей.** Возможность сервера получить доступ к необходимым зависимым компонентам, таким как Active Directory, DNS и т. д.

При установке пакета управления Exchange System Center Operations Manager (SCOM) действует как портал работоспособности для просмотра сведений, связанных со средой Exchange. Панель мониторинга SCOM включает три представления работоспособности сервера Exchange:

  - **Активные оповещения.** Ответчики эскалации записывают события в журнал событий Windows, которые используются монитором в SCOM. Они отображаются в виде оповещений в представлении активных оповещений.

  - **Работоспособность организации.** В этом представлении отображается сводка общей работоспособности организации Exchange. В сводном представлении отображается работоспособность отдельных групп доступности базы данных, а также работоспособность отдельных сайтов Active Directory.

  - **Работоспособность сервера.** Связанные настройки работоспособности объединяются в группы работоспособности, сводная информация о которых отображается в этом представлении.

## Переопределения

Переопределения позволяют администратору настраивать некоторые аспекты зондов, мониторов и ответчиков управляемой доступности. Переопределения можно использовать для точной настройки некоторых пороговых значений, используемых компонентом управляемой доступности. С их помощью также можно включить экстренные действия для непредвиденных событий, для которых могут потребоваться параметры конфигурации, отличных от настроек по умолчанию.

Переопределения можно создать и применять для одного сервера (это называют *переопределением сервера*) или для группы серверов (*глобальное переопределение*). Данные конфигурации переопределения сервера хранятся в реестре Windows на сервере, к которому применяется переопределение. Данные конфигурации глобального переопределения хранятся в Active Directory.

Переопределения можно настраивать без срока действия или с заданным сроком действия. Кроме того, глобальные переопределения можно настроить для всех серверов или только серверов с определенной версией Exchange.

При настройке переопределения оно вступит в силу не сразу. Служба диспетчера работоспособности Microsoft Exchange проверяет наличие обновленных данных конфигурации каждые 10 минут. Кроме того, глобальные переопределения зависят от задержки репликации Active Directory.

Подробные инструкции для просмотра или настройки серверных или глобальных переопределений см. в статье [Настройка переопределений управляемой доступности](configure-managed-availability-overrides-exchange-2013-help.md).

## Задачи управления и командлеты

Существует три основных операционных задачи, которые администраторы обычно выполняют для компонента управляемой доступности:

  - извлечение или просмотр состояния системы;

  - просмотр настроек работоспособности и сведений о зондах, мониторах и ответчиках;

  - управление переопределениями.

Два основных средства для работы с управляемой доступностью — это журнал событий Windows и командная консоль. Компонент управляемой доступности записывает много информации в красные каналы ActiveMonitoring и ManagedAvailability журналов событий Exchange, например:

  - определения зондов, мониторов и ответчиков, которые записываются в соответствующие журналы событий \*Definition;

  - результаты зондов, мониторов и ответчиков, которые записываются в соответствующие журналы событий \*Results;

  - сведения о действиях восстановления ответчика, в том числе время начала и завершения действия (при успешном или неудачном выполнении), которые записываются в журнал событий RecoveryActionResults.

Существует 12 командлетов для управляемой доступности, которые описаны в следующей таблице.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Командлет</th>
<th>Описание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ru-ru/library/jj218703(v=exchg.150)">Get-ServerHealth</a></p></td>
<td><p>Используется для получения необработанной информации о работоспособности сервера, например настройки работоспособности и их текущее состояние (исправно или нет), мониторы настроек работоспособности, серверные компоненты, целевые ресурсы для зондов и временные метки, связанные с временем запуска или остановки зонда или монитора, а также время перехода в то или иное состояние.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ru-ru/library/jj218724(v=exchg.150)">Get-HealthReport</a></p></td>
<td><p>Используется для получения сводного представления работоспособности, которое включает в себя настройки работоспособности и их текущее состояние.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ru-ru/library/jj218668(v=exchg.150)">Get-MonitoringItemIdentity</a></p></td>
<td><p>Используется для просмотра зондов, мониторов и ответчиков, связанных с определенными настройками работоспособности.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ru-ru/library/jj218642(v=exchg.150)">Get-MonitoringItemHelp</a></p></td>
<td><p>Используется для просмотра описания некоторых свойств зондов, мониторов и ответчиков.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ru-ru/library/jj218628(v=exchg.150)">Add-ServerMonitoringOverride</a></p></td>
<td><p>Используется для создания локального, предназначенного для конкретного сервера переопределения зонда, монитора или ответчика.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ru-ru/library/jj218664(v=exchg.150)">Get-ServerMonitoringOverride</a></p></td>
<td><p>Используется для просмотра списка локальных переопределений на указанном сервере.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ru-ru/library/dn482411(v=exchg.150)">Remove-ServerMonitoringOverride</a></p></td>
<td><p>Используется для удаления локального переопределения на указанном сервере.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ru-ru/library/jj218683(v=exchg.150)">Add-GlobalMonitoringOverride</a></p></td>
<td><p>Используется для создания глобального переопределения для группы серверов.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ru-ru/library/jj218627(v=exchg.150)">Get-GlobalMonitoringOverride</a></p></td>
<td><p>Используется для просмотра списка глобальных переопределяет, настроенных в организации.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ru-ru/library/jj218675(v=exchg.150)">Remove-GlobalMonitoringOverride</a></p></td>
<td><p>Используется для удаления глобального переопределения.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ru-ru/library/jj218699(v=exchg.150)">Set-ServerComponentState</a></p></td>
<td><p>Используется для настройки состояния одного или нескольких серверных компонентов.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ru-ru/library/jj218713(v=exchg.150)">Get-ServerComponentState</a></p></td>
<td><p>Используется для просмотра состояния одного или нескольких серверных компонентов.</p></td>
</tr>
</tbody>
</table>

