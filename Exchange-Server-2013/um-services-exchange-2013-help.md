﻿---
title: 'Службы единой системы обмена сообщениями: Exchange 2013 Help'
TOCTitle: Службы единой системы обмена сообщениями
ms:assetid: f36835f2-1e5f-4e5a-88bc-0672af1e3498
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb125191(v=EXCHG.150)
ms:contentKeyID: 50556507
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Службы единой системы обмена сообщениями

 

_**Применимо к:** Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2012-11-18_

Серверы клиентского доступа со службой маршрутизатора вызовов единой системы обмена сообщениями Microsoft Exchange и серверы почтовых ящиков со службой единой системы обмена сообщениями Microsoft Exchange обеспечивают развертывание функций голосовой почты и единой системы обмена сообщениями для пользователей в организации.

Необходимы сведения о других задачах управления, связанных со службами единой системы обмена сообщениями? См. раздел [Процедуры служб единой системы обмена СООБЩЕНИЯМИ](um-services-procedures-exchange-2013-help.md).

**Содержание**

Сервер клиентского доступа и сервер почтовых ящиков

Параметры конфигурации сервера

Работа сервера

## Сервер клиентского доступа и сервер почтовых ящиков

В Exchange 2013 роли серверов Exchange 2007 и Exchange 2010 объединяются в двух типах серверов. Все компоненты и службы этих ролей сервера запускаются на одном или двух отдельных физических серверах — сервере клиентского доступа и сервере почтовых ящиков.

В новой модели сервер клиентского доступа отвечает за автообнаружение, протокол SSL, проверку подлинности, перенаправление и прокси-связь. Сервер клиентского доступа — это точка входа для запросов протокола SIP и всех входящих вызовов единой системы обмена сообщениями. Логика маршрутизации и переадресации SIP реализована в виде службы, которая автоматически включается в сервер клиентского доступа. Данная услуга, называется Маршрутизатор вызовов единой системы обмена сообщениями Microsoft Exchange Служба. Она выполняется на каждом сервере клиентского доступа в организации.

Когда сервер клиентского доступа, получающий SIP INVITE для входящего вызова, то маршрутизатор вызовов единой системы обмена сообщениями Microsoft Exchange Службы перенаправляет входящий вызов к серверу почтовых ящиков. Затем медиа-канал (RTP или SRTP) создается между шлюзом VoIP, IP-УАТС или пограничным контроллером сеансов (SBC) и сервером почтовых ящиков. Несмотря на то, что сервер клиентского доступа работает как SIP передиректор, это обрабатывает только запросы SIP от шлюзов VoIP, IP PBX, или DBCS. Он не получает никаких Медиатрафик. Трафик медиаданных, который использует RTP или SRTP, передается только между сервером почтовых ящиков и кэширующими узлами SIP — шлюзами VoIP, IP-УАТС или SBC. При развертывании единой системы обмена сообщениями и Exchange 2013, необходимо настроить VoIP-шлюзы, IP-АТС, или SBCS для указывания на серверы клиентского доступа, которые были установлены таким образом, что входящие вызовы для единой системы обмена сообщениями будут направляться правильно.

В Exchange 2013 сервер почтовых ящиков выполняет те же процедуры, что и роль сервера единой системы обмена сообщениями в Exchange 2007 и Exchange 2010. Сервер почтовых ящиков выполняет как служба единой системы обмена сообщениями Microsoft Exchange и рабочих процессов единой системы обмена сообщениями.

При установке и развертывании серверов клиентского доступа и почтовых ящиков единой системы обмена сообщениями вам не придется связывать или добавлять эти серверы в абонентские группы единой системы обмена сообщениями. Серверы клиентского доступа и почтовых ящиков отвечают на все входящие вызовы и используют абонентские группы единой системы обмена сообщениями для поиска пользователей.

Однако если вы занимаетесь интеграцией единой системы обмена сообщениями и Office Communications Server 2007 R2 или Lync Server или, медиа-каналы SIP, RTP и SRTP для входящих вызовов обрабатываются серверами Lync и сервером почтовых ящиков. В Lync интегрированная среда, необязательно шлюзы VoIP, IP PBX, или DBCS. Для Lync, сервер почтовых ящиков, на котором запущен служба единой системы обмена сообщениями Microsoft Exchange Exchange 2010 очень похожа на одну сервера единой системы обмена сообщениями. Сервер почтовых ящиков и сервер клиентского доступа считаются доверенными узлами, поскольку оба сервера должны быть добавлены к абонентской группе SIP. Lync перенаправляет входящий звонок с помощью Компонент Маршрутизация входящих пакетов, который используется для обмена данными с SIP сервер клиентского доступа и маршрутизации вызова на сервер почтовых ящиков.

Сервер клиентского доступа и сервер почтовых ящиков

## Параметры конфигурации сервера

В Exchange 2013 все компоненты и параметры конфигурации единой системы обмена сообщениями, применяемые на одном компьютере с ролью сервера единой системы обмена сообщениями в Exchange 2010, по-прежнему доступны. Тем не менее, некоторые из этих компонентов и параметров конфигурации находятся на сервере клиентского доступа, а другие доступны на сервере почтовых ящиков. В некоторых случаях, те же параметр доступен на обоих. В следующем списке перечислены параметры и настройки, которые доступны как на сервере клиентского доступа и сервером почтовых ящиков.

  - \[-DialPlans \<MultiValuedProperty\>\]

  - \[-MaxCallsAllowed \<Int32\>\]

  - \[-SipTcpListeningPort \<Int32\>\]

  - \[-SipTlsListeningPort \<Int32\>\]

  - \[-Status \<Enabled | Disabled | NoNewCalls\>\]

  - \[-UMStartupMode \<TCP | TLS | Dual\>\]

Для сервера почтовых ящиков будут использоваться командлеты **Set-UMService**, **Get-UMService**, **Enable-UMService** и **Disable-UMService**, которые служат для просмотра и настройки свойств службы единой системы обмена сообщениями Microsoft Exchange. Другой набор командлетов, **Set-UMCallRouterSettings** и **Get-UMCallRouterSettings**, используется для просмотра или настройки свойств службы маршрутизатора вызовов единой системы обмена сообщениями Microsoft Exchange на серверах клиентского доступа. Это гарантирует, что существующие **Get-UMServer** , **Set-UMServer** , **Enable-UMServer** , и **Disable-UMServer** командлеты из Exchange 2007 и Exchange 2010 будет работать в топологии с сосуществованием Exchange 2013 серверов почтовых ящиков. Это также гарантирует, что командлеты будут работать, если серверы почтовых ящиков и серверы клиентского доступа установлены на одном или разных компьютерах.

Сервер клиентского доступа и сервер почтовых ящиков

## Работа сервера

Когда серверы клиентского доступа и почтовых ящиков установлены, они включаются автоматически, чтобы отвечать на входящие и исходящие голосовые вызовы и выполнять маршрутизацию сообщений голосовой почты получателям в организации Exchange.

Вы можете разрешить или запретить службе единой системы обмена сообщениями Microsoft Exchange на сервере почтовых ящиков или службе маршрутизатора вызовов единой системы обмена сообщениями Microsoft Exchange на сервере клиентского доступа отвечать на новые вызовы. По умолчанию сервер клиентского доступа и сервер почтовых ящиков находится в активированном состоянии после установки. Когда вы настраиваете сервер клиентского доступа или почтовых ящиков для приема входящих вызовов голосовой и факсимильной связи, автосекретаря и голосового доступа к Outlook, используется командлет **Set-ServerComponentState**.

Настройка режима обслуживания для сервера клиентского доступа или почтовых ящиков Exchange 2013 позволяет вывести сервер из эксплуатации. Для сервера почтовых ящиков это означает, что сервер не будет размещать никаких активных баз данных, все очереди транспорта пусты, и сервер не будет принимать какие-либо входящие вызовы от серверов клиентского доступа, шлюзов VoIP, IP-УАТС, SIP-УАТС или SBC. Для сервера клиентского доступа это означает, что сервер не будет принимать входящие вызовы со шлюзов VoIP, IP-УАТС, SIP-УАТС или пограничных контроллеров сеансов (SBC).

В Exchange 2007 и Exchange 2010 был параметр состояния, который можно было использовать для управления рабочим состоянием сервера единой системы обмена сообщениями. В Exchange 2013 такой параметр статуса у командлета **Set-UMCallRouterSettings** на серверах клиентского доступа и командлета **Set-UMService** на серверах почтовых ящиков отсутствует.

Хотя серверы клиентского доступа и почтовых ящиков включаются при установке, ни один сервер не сможет может корректно обрабатывать и маршрутизировать входящие вызовы пользователям единой системы обмена сообщениями, пока абонентская группа единой системы обмена сообщениями не будет связана хотя бы с одним шлюзом IP единой системы обмена сообщениями.

Когда связь установлена, серверы клиентского доступа и почтовых ящиков находят все IP-шлюзы, связанные с абонентской группой единой системы обмена сообщениями, а также шлюзы VoIP, IP-УАТС и пограничные контроллеры сеансов. Для обнаружения любых изменений конфигурации в абонентских группах или IP-шлюзах единой системы обмена сообщениями серверы клиентского доступа и почтовых ящиков проверяют конфигурацию каждые 10 минут.

Если IP-шлюз единой системы обмена сообщениями находит изменения конфигурации, сервер почтовых ящиков или сервер клиентского доступа реагирует соответственно и начинает или прекращает использовать соответствующие шлюзы VoIP, IP-УАТС и пограничные контроллеры сеансов. После того, как серверы клиентского доступа и серверы почтовых ящиков отвечают на входящие вызовы для пользователей, связанных с абонентской группой единой системы обмена сообщениями, правильно общаясь со шлюзами VoIP, IP-УАТС и SBC, можно запустить набор диагностических операций, чтобы убедиться, что они работают правильно и что подключение между серверами Exchange и шлюзами VoIP, IP-УАТС и SBCS работает правильно.

Сервер клиентского доступа и сервер почтовых ящиков
