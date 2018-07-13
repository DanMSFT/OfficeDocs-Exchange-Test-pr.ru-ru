﻿---
title: 'Цифровые сертификаты и протокол SSL: Exchange 2013 Help'
TOCTitle: Цифровые сертификаты и протокол SSL
ms:assetid: a9e2e08c-d46a-4135-a387-eb653212b676
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd351044(v=EXCHG.150)
ms:contentKeyID: 51408063
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Цифровые сертификаты и протокол SSL

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2013-08-26_

Протокол Secure Sockets Layer (SSL) обеспечивает безопасность взаимодействия между клиентом и сервером. Для Exchange Server 2013 протокол SSL используется для защиты обмена данными между сервером и клиентами. К клиентам относятся мобильные телефоны, компьютеры в сети организации и за ее пределами.

В конфигурации сервера Exchange 2013 по умолчанию связь с клиентами шифруется по протоколу SSL при использовании Outlook Web App, Exchange ActiveSync и мобильного Outlook.

Для протокола SSL требуется применение цифровых сертификатов. В данном разделе приведены сводные сведения о различных типах цифровых сертификатов и настройке Exchange 2013 для использования этих сертификатов.

**Содержание**

Обзор цифровых сертификатов

Цифровые сертификаты и использование прокси-сервера

Рекомендации по использованию цифровых сертификатов

## Обзор цифровых сертификатов

Цифровые сертификаты — это файлы, которые используются аналогично паролям для подтверждения подлинности пользователя или компьютера. Они используются для создания зашифрованного канала SSL, по которому осуществляется взаимодействие с клиентами. Сертификат — это цифровой документ, который выпускается центром сертификации; он подтверждает подлинность держателя сертификата и позволяет сторонам взаимодействовать безопасным способом, используя шифрование.

Цифровые сертификаты выполняют следующие функции:

  - проверка того, что их владельцы — физические лица, веб-сайты и даже сетевые ресурсы, например маршрутизаторы — действительно являются теми, за кого себя выдают;

  - защита передаваемых по сети данных от похищения или изменения.

Цифровые сертификаты могут выдаваться доверенным сторонним центром сертификации или инфраструктурой открытых ключей Windows с использованием служб сертификации. Кроме того, цифровые сертификаты могут быть самозаверяющими. У каждого типа сертификатов есть свои преимущества и недостатки, однако в любом случае цифровые сертификаты защищены от изменения и подделки.

Сертификаты могут выдаваться для выполнения различных задач, в том числе для проверки подлинности веб-пользователей и веб-серверов, для использования расширений S/MIME, протоколов IPsec и TLS, а также для подписывания кода.

Сертификат содержит открытый ключ, который он связывает с удостоверением владельца (пользователя, компьютера или службы) соответствующего закрытого ключа. Открытый и закрытый ключи используются клиентом и сервером для шифрования данных перед их передачей. Для пользователей, компьютеров и служб Windows доверие в центре сертификации устанавливается, если в доверенном корневом хранилище сертификатов существует копия корневого сертификата, а сертификат содержит допустимый путь сертификации. Сертификат считается допустимым, если он не был отозван, и не истек срок его действия.

## Типы сертификатов

Существует три основных типа цифровых сертификатов: самозаверяющие сертификаты, сертификаты, создаваемые инфраструктурой открытых ключей Windows, и сертификаты сторонних центров сертификации.

## Самозаверяющие сертификаты

При установке Exchange 2013 на серверах почтовых ящиков автоматически настраивается самозаверяющий сертификат. Самозаверяющий сертификат подписывается приложением, которое создает его. Получатель и имя сертификата совпадают. Кроме субъекта, в сертификате указывается его издатель. Этот самозаверяющий сертификат используется для шифрования данных, передаваемых между серверами клиентского доступа и почтовых ящиков. Сервер клиентского доступа автоматически доверяет самозаверяющему сертификату на сервере почтовых ящиков, поэтому на сервере почтовых ящиков сертификат стороннего поставщика не нужен. При установке Exchange 2013 на сервере клиентского доступа также создается самозаверяющий сертификат. Данный самозаверяющий сертификат позволяет некоторым клиентским протоколам использовать при передаче данных протокол SSL. Exchange ActiveSync и Outlook Web App могут устанавливать подключения SSL с помощью самозаверяющего сертификата. Мобильный Outlook не сможет работать с самозаверяющим сертификатом на сервере клиентского доступа. Самозаверяющие сертификаты необходимо вручную копировать в доверенное корневое хранилище сертификатов на клиентском компьютере или мобильном устройстве. Когда клиент подключается к серверу по протоколу SSL и сервер предъявляет самозаверяющий сертификат, у клиента запрашивается подтверждение того, что сертификат был выдан доверенным центром сертификации. Клиент должен явно выразить доверие этому центру сертификации. Если клиент подтверждает доверие, взаимодействие по протоколу SSL может быть продолжено.

> [!NOTE]  
> На серверах почтовых ящиков по умолчанию устанавливает самозаверяющий сертификат. Нет необходимости заменять самозаверяющий сертификат на серверах клиентского доступа в вашей организации сторонним доверенным сертификатом. Сервер клиентского доступа автоматически доверяет самозаверяющему сертификату на сервере почтовых ящиков и для сертификатов на сервере почтовых ящиков не нужны другие настройки.


На малых предприятиях часто принимается решение не использовать сторонние сертификаты или не устанавливать инфраструктуру открытых ключей для выпуска собственных сертификатов. Этом может происходить по экономическим соображениям, из-за отсутствия у администраторов необходимого опыта и знаний для создания собственной иерархии сертификатов или по обеим указанным причинам. При использовании самозаверяющих сертификатов затраты минимальны, а установка проста. Однако в таком случае гораздо труднее создать инфраструктуру для управления жизненным циклом сертификатов, их обновления, управления доверием и отзыва сертификатов.

## Сертификаты, создаваемые инфраструктурой открытых ключей Windows

Второй тип сертификатов — сертификаты, создаваемые инфраструктурой открытых ключей Windows. Инфраструктура открытых ключей представляет собой систему цифровых сертификатов, центров сертификации и центров регистрации, которые проверяют допустимость каждого компонента, участвующего в электронной транзакции, с использованием шифрования с открытым ключом. При создании инфраструктуры открытых ключей в организации, использующей службу каталогов Active Directory, необходимо обеспечить инфраструктуру для управления жизненным циклом сертификатов, их обновления, управления отношениями доверия и отзыва сертификатов. Однако для создания сертификатов инфраструктуры открытых ключей Windows и управления ими необходимо выделить дополнительные средства на развертывание серверов и инфраструктуры.

Для развертывания инфраструктуры открытых ключей Windows необходимы службы сертификации, которые можно установить с помощью компонента **Установка и удаление программ** панели управления. Службы сертификации можно установить на любом сервере в домене.

Если сертификаты выдает центр сертификации, подключенный к домену Windows, можно использовать его для запроса и подписи сертификатов, выдаваемых серверам или компьютерам в сети. Это позволяет использовать инфраструктуру открытых ключей, аналогичную той, которую используют сторонние поставщики сертификатов, но менее дорогую. В отличие от сертификатов других типов такие сертификаты инфраструктуры открытых ключей невозможно развернуть для общего использования. Тем не менее, когда центр сертификации инфраструктуры открытых ключей подписывает сертификат запросившей стороны с помощью закрытого ключа, выполняется проверка запросившей стороны. Открытый ключ такого центра сертификации является частью сертификата. Сервер, имеющий такой сертификат в хранилище доверенных корневых сертификатов, может использовать этот открытый ключ для расшифровки сертификата запросившей стороны и проверки ее подлинности.

Процедура развертывания сертификата, созданного инфраструктурой открытых ключей, мало чем отличается от развертывания самозаверяющего сертификата. При этом также необходимо установить копию доверенного корневого сертификата, полученного от инфраструктуры открытых ключей, в доверенном корневом хранилище сертификатов на компьютерах или мобильных устройствах, которым требуется устанавливать SSL-соединение с Microsoft Exchange.

Инфраструктура открытых ключей Windows позволяет организациям публиковать собственные сертификаты. Клиенты могут запрашивать и получать сертификаты от инфраструктуры открытых ключей Windows во внутренней сети. Инфраструктура открытых ключей Windows может обновлять и отзывать сертификаты.

## Доверенные сторонние сертификаты

Сторонние или коммерческие сертификаты — это сертификаты, которые создаются сторонними или коммерческими центрами сертификации и затем приобретаются их клиентами для использования на своих сетевых серверах. Одна из проблем при использовании самозаверяющих сертификатов и сертификатов на основе инфраструктуры открытых ключей состоит в том, что, поскольку клиентский компьютер или мобильное устройство не доверяют такому сертификату автоматически, необходимо импортировать сертификат в доверенное корневое хранилище сертификатов на клиентских компьютерах и устройствах. При использовании сторонних или коммерческих сертификатов такой проблемы не возникает. Большинство сертификатов коммерческих центров сертификации уже являются доверенными, потому что такой сертификат уже находится в доверенном корневом хранилище сертификатов. Так как издатель является доверенным, сертификат также оказывается доверенным. Использование сторонних сертификатов во многом упрощает развертывание.

Для крупных организаций или для организаций, которым необходимо развертывать сертификаты для общего использования, применение сторонних (коммерческих) сертификатов является наилучшим решением, несмотря на связанные с этим расходы. Коммерческие сертификаты могут оказаться не лучшим решением для малых и средних организаций, поэтому вместо них целесообразно использовать сертификаты других типов.

В начало

## Выбор типа сертификата

При выборе типа устанавливаемого сертификата следует учесть несколько факторов. Чтобы сертификат был допустимым, он должен быть подписан. Он может быть самозаверяющим или же подписанным центром сертификации. Самозаверяющий сертификат имеет ограничения. Например, не на всех мобильных устройствах пользователь может установить цифровой сертификат в доверенное корневое хранилище сертификатов. Поддержка установки сертификатов на мобильном устройстве зависит от изготовителя устройства и оператора мобильной связи. Некоторые изготовители и операторы мобильной связи отключают доступ к доверенному корневому хранилищу сертификатов. В этом случае на мобильном устройстве нельзя установить ни самозаверяющий сертификат, ни сертификат, полученный от центра сертификации инфраструктуры открытых ключей Windows.

## Сертификаты Exchange по умолчанию

По умолчанию Exchange устанавливает самозаверяющий сертификат как на сервер клиентского доступа, так и на сервер почтовых ящиков для шифрования всех передаваемых по сети данных. Для этого необходимо, чтобы у каждого сервера Exchange был сертификат X.509, который он может использовать. Следует заменить этот самозаверяющий сертификат на сервере клиентского доступа на сертификат, который автоматически является доверенным для ваших клиентов.

Термин "Самозаверяющий" означает, что сертификат был создан и подписан только самим сервером Exchange. Поскольку он не был создан и подписан доверенным центром сертификации, самозаверяющий сертификат по умолчанию не будет доверенным для любого программного обеспечения, кроме других серверов Exchange из той же организации. Сертификат по умолчанию используется для всех служб Exchange. У этого сертификата есть дополнительное имя субъекта, соответствующее имени сервера Exchange, на котором он установлен. Кроме того, у него есть список дополнительных имен субъектов, которые включают в себя имя сервера и полное доменное имя сервера.

Хотя другие серверы Exchange в организации Exchange автоматически доверяют этому сертификату, этого не происходит для таких клиентов, как веб-браузеры, клиенты Outlook, мобильные телефоны и другие клиенты электронной почты в дополнение к внешним серверам электронной почты. Поэтому рекомендуется заменить этот сертификат на доверенный сторонний сертификат на серверах клиентского доступа Exchange. Если имеется собственная внутренняя инфраструктура открытых ключей, которая является доверенной для всех клиентов, можно также использовать собственные сертификаты.

## Требования к сертификатам для различных служб

Сертификаты используются для нескольких задач в Exchange. Большинство клиентов также используют сертификаты на нескольких серверах Exchange. Как правило, чем меньше используется сертификатов, тем проще ими управлять.

## Службы IIS

Все следующие службы Exchange используют один и тот же сертификат на отдельном сервере клиентского доступа Exchange:

  - Outlook Web App

  - центр администрирования Exchange (EAC)

  - Веб-службы Exchange

  - Exchange ActiveSync

  - Мобильный Outlook

  - Автообнаружение

  - Распространения адресной книги Outlook

Поскольку с веб-сайтом может быть сопоставлен только один сертификат, а все эти службы по умолчанию предоставляются через один веб-сайт, все имена, используемые клиентами этих служб, должны быть указаны в этом сертификате (или соответствовать имени из подстановочных знаков в этом сертификате).

## POP/IMAP

Сертификаты, используемые для POP или IMAP, можно задавать отдельно от сертификата для служб IIS. Однако для упрощения администрирования рекомендуется включить имя службы POP или IMAP в сертификат для служб IIS и использовать для всех этих служб только один сертификат.

## SMTP

Отдельный сертификат можно использовать для каждого соединителя настраиваемого получения. Этот сертификат должен содержать имя, используемое SMTP-клиентами (или другими SMTP-серверами) для доступа к соединителю получения. Чтобы упростить управление сертификатами, рекомендуется включить все имена, для которых требуется поддержка трафика TLS, в один сертификат.

## Цифровые сертификаты и использование прокси-сервера

Прокси-сервер используется, когда один сервер отправляет клиентские подключения другому. В случае Exchange 2013 это происходит, когда сервер клиентского доступа передает входящий клиентский запрос на сервер почтовых ящиков, который содержит активную копию клиентского почтового ящика.

Когда серверы клиентского доступа передают запросы, протокол SSL используется для шифрования, но не для проверки подлинности. Самозаверяющий сертификат на сервере почтовых ящиков шифрует трафик между сервером клиентского доступа и сервером почтовых ящиков.

## Обратные прокси-серверы и сертификаты

Во многих развертываниях Exchange для публикации служб Exchange в Интернете используются обратные прокси-серверы. Обратные прокси-серверы можно настроить для остановки шифрования SSL, изучения трафика на сервере в незашифрованном виде и последующего открытия нового канала шифрования SSL с обратных прокси-серверов на расположенные за ними серверы Exchange. Это называется мостом SSL. Другой способ настройки обратных прокси-серверов заключается в том, чтобы разрешить передачу подключений SSL непосредственно на серверы Exchange, расположенные за обратными прокси-серверами. При любой из моделей развертывания клиенты в Интернете подключаются к обратному прокси-серверу с использованием имени узла для доступа к Exchange, например mail.contoso.com. После этого обратный прокси-сервер подключается к Exchange с использованием другого имени узла, например имени компьютера сервера клиентского доступа Exchange. Вам не требуется включать это имя компьютера сервера клиентского доступа Exchange в сертификат, поскольку наиболее распространенные обратные прокси-серверы могут сопоставлять исходное имя узла, использованное клиентом, с внутренним именем узла сервера клиентского доступа Exchange.

## SSL и разделенная DNS

Разделенная DNS — это технология, которая позволяет настраивать для одного имени узла различные IP-адреса в зависимости от того, откуда поступил исходный DNS-запрос. Это также называется DNS с "расщеплением горизонта", комбинированным режимом DNS или расщепленной DNS. Разделенная служба DNS может помочь снизить количество имен узлов, которыми необходимо управлять в Exchange, позволяя клиентам использовать одно и то же имя узла для подключения к Exchange как из Интернета, так и из интрасети. Разделенная служба DNS позволяет запросам, исходящим из интрасети, получать IP-адрес, отличный от адреса запросов из Интернета.

Использование разделенной DNS обычно не требуется в небольших развертываниях Exchange, поскольку пользователи могут получить доступ к одной конечной точке DNS как из интрасети, так и из Интернета. Однако для более крупных развертываний такая конфигурация приводит к слишком высокой нагрузке на прокси-сервер исходящих подключений к Интернету и обратный прокси-сервер. Для крупных развертываний следует настроить разделенную DNS таким образом, чтобы внешние пользователи обращались к mail.contoso.com, а внутренние пользователи обращались к internal.contoso.com. При использовании разделенной DNS для данной конфигурации пользователям не требуется помнить об использовании различных имен узлов в зависимости от расположения.

## Удаленная оболочка Windows PowerShell

Проверка подлинности Kerberos и шифрование Kerberos используются для удаленного доступа к Windows PowerShell как из центра администрирования Exchange, так и из командной консоли Exchange. Благодаря этому не требуется настраивать сертификаты SSL для удаленного Windows PowerShell.

В начало

## Рекомендации по использованию цифровых сертификатов

Хотя конфигурация цифровых сертификатов в организации изменяется в зависимости от текущих потребностей, эти рекомендации помогут вам подобрать оптимальную конфигурацию цифровых сертификатов.

## Рекомендация: используйте сертификаты доверенных сторонних поставщиков

Чтобы предотвратить получение клиентами ошибок, связанных с недоверенными сертификатами, используемый сервером Exchange сертификат должен быть выдан объектом, которому клиент доверяет. Хотя для большинства клиентов можно настроить доверие к любому сертификату или издателю сертификата, проще использовать на сервере Exchange доверенный сторонний сертификат. Причиной этого является то, что большинство клиентов уже доверяют своим корневым сертификатам. Существует несколько сторонних издателей сертификатов, которые предлагают сертификаты, настроенные специально для Exchange. С помощью Центра администрирования Exchange можно создавать запросы сертификатов, совместимые с большинством издателей сертификатов.

## Выбор центра сертификации

Центр сертификации является компанией, которая выдает сертификаты и обеспечивает их допустимость. Клиентское программное обеспечение (например, браузеры, такие как Майкрософт Internet Explorer, или операционные системы, такие как Windows или Mac OS) имеет встроенные списки доверенных центров сертификации. Обычно этот список можно настраивать для добавления и удаления центров сертификации, но часто это требует значительных усилий. Используйте следующие критерии выбора центра сертификации для приобретения сертификатов.

  - Убедитесь, что центр сертификации является доверенным для клиентского программного обеспечения (операционных систем, браузеров и мобильных телефонов), которое будет осуществлять подключение к серверам Exchange.

  - Выбирайте центр сертификации, для которого заявлена поддержка сертификатов единой системы обмена сообщениями для серверов Exchange.

  - Убедитесь, что центр сертификации поддерживает те типы сертификатов, которые планируется использовать. Рекомендуется использовать сертификаты с дополнительными именами субъектов. Такие сертификаты поддерживаются не всеми центрами сертификации; кроме того, некоторые центры сертификации могут не поддерживать требуемое количество имен узлов.

  - Убедитесь, что приобретаемая лицензия на сертификаты позволяет разместить сертификаты на том количестве серверов, которое планируется использовать. Некоторые центры сертификации позволяют разместить сертификат только на одном сервере.

  - Сравните цены на сертификаты в разных центрах сертификации.

## Рекомендация: Использование сертификатов с дополнительными именами субъектов

В зависимости от параметров имен служб в развертывании Exchange сервер Exchange может нуждаться в сертификате, содержащем несколько доменных имен. Несмотря на возможность использования группового сертификата для разрешения этой трудности, например \*.contoso.com, многим клиентам не нравится поддерживать сертификат, который охватывает любой дочерний домен. Более безопасным вариантом является перечисление в сертификате необходимых доменов в качестве дополнительных имен субъектов. При создании запросов сертификатов в Exchange по умолчанию применяется именно этот метод.

## Рекомендация: Использование мастера сертификатов Exchange для запроса сертификатов

Существует несколько служб Exchange, использующих сертификаты. Распространенной ошибкой при запросе сертификатов является создание запроса без включения в него нужного набора имен служб. Мастер сертификатов в центре управления Exchange поможет вам включить правильный список имен в запрос сертификата. Это мастер позволяет указать, с какими службами должен работать данный сертификат, и в зависимости от выбранных служб он включает требуемые имена в сертификат, чтобы его можно было использовать для этих служб. Запустите мастер сертификатов после того, как выполнено развертывание начального набора серверов Exchange 2013 и определено, какие имена узлов требуется использовать для различных служб данного развертывания. В идеальном случае мастер сертификатов требуется запустить только один раз для каждого из сайтов Active Directory, на которых развертывается Exchange.

Вместо того, чтобы тщательно следить за указанием всех имен узлов в списке дополнительных имен субъектов приобретаемого сертификата, можно использовать центр сертификации, который предлагает бесплатный льготный период, в течение которого можно вернуть сертификат и запросить такой же сертификат с несколькими дополнительными именами узлов.

## Рекомендация: используйте минимальное количество имен узлов

Кроме использования минимального количества сертификатов, следует стремиться к предельно возможному сокращению количества имен узлов. Такой подход позволяет экономить средства. Размер счета у многих поставщиков сертификатов зависит от числа имен узлов, добавляемых в сертификат.

Наиболее эффективное решение по снижению требуемого количества имен узлов и упрощению управления сертификатами заключается в том, чтобы не включать в дополнительные имена субъектов сертификата имена узлов для отдельных серверов.

В сертификаты Exchange необходимо включить те имена узлов, которые используются клиентскими приложениями для подключения к Exchange. Ниже приведен список типичных имен узлов, которые потребуются компании под названием Contoso:

  - **Mail.contoso.com**   Это имя узла охватывает большинство подключений к Exchange, включая МайкрософтOutlook, Outlook Web App, мобильный Outlook, автономную адресную книгу, веб-службы Exchange, POP3, IMAP4, SMTP, панель управления Exchange и ActiveSync.

  - **Autodiscover.contoso.com**   Это имя узла используется клиентами, у которых включена поддержка автообнаружения, включая Майкрософт Office Outlook 2007 и более поздних версий, клиенты веб-служб Exchange ActiveSync и Exchange.

  - **Legacy.contoso.com**  Это имя узла требуется при сосуществовании с Exchange 2007 или Exchange 2013. Если имеются клиенты с почтовыми ящиками как в Exchange 2007, так и в Exchange 2013, настройка устаревшего имени узла не позволит пользователям узнать второй URL-адрес во время обновления.

## Общие сведения о групповых сертификатах

Групповой сертификат предназначен для поддержки домена и нескольких поддоменов. Например, результатом настройки группового сертификата для \*.contoso.com является сертификат, действующий для mail.contoso.com, web.contoso.com и autodiscover.contoso.com.

В начало
