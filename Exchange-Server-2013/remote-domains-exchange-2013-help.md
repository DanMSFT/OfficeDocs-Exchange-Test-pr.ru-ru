﻿---
title: 'Удаленные домены: Exchange 2013 Help'
TOCTitle: Удаленные домены
ms:assetid: 10fb7d62-4d78-40a3-82db-d62bcd27ba42
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Aa996309(v=EXCHG.150)
ms:contentKeyID: 50487455
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Удаленные домены

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2015-04-07_

Для определения параметров передачи сообщений между организацией Microsoft Exchange Server 2013 и доменами вне организации Exchange можно создавать записи удаленных доменов. Создание записи удаленного домена позволяет управлять типами сообщений, отправляемых на этот домен. К сообщениям, отправляемым пользователями организации на удаленный домен, можно также применять политики форматов сообщений и допустимые наборы знаков. Параметры удаленных доменов являются глобальными параметрами конфигурации для организации Exchange.

Параметры удаленного домена применяются к сообщениям во время их классификации в транспортной службе на серверах почтовых ящиков. При выполнении разрешения получателя домен получателя сопоставляется с настроенными удаленными доменами. Если конфигурация удаленного домена блокирует отправку сообщений определенного типа получателям в этом домене, сообщение удаляется. Если для удаленного домена указывается определенный формат сообщений, заголовки и содержимое сообщений изменяются. Эти параметры применяются ко всем сообщениям, обрабатываемым в организации Exchange.

> [!NOTE]  
> Если параметры сообщений настраиваются для пользователей индивидуально, параметры для пользователя переопределяют параметры для организации.


По умолчанию существует одна запись удаленного домена. Адресное пространство домена настраивается как (\*). Это является представлением всех удаленных доменов. Если дополнительные записи удаленных доменов не создаются, ко всем сообщениям, отправляемым всем получателям во всех удаленных доменах, применяются одни и те же параметры.

При настройке удаленных доменов можно запретить отправку определенных типов сообщений на соответствующий домен. К этим типам сообщений относятся сообщения об отсутствии на работе, сообщения автоматического ответа, отчеты о недоставке и уведомления о переадресации собрания. В среде с несколькими лесами может потребоваться разрешить отправку сообщений данных типов в эти домены. Однако если указаны домены, являющиеся источником нежелательной почты, может возникнуть необходимость блокировки отправки сообщений данных типов в эти удаленные домены.

**Содержание**

формат сообщений;

Параметры автоматических ответов

Управление информацией об отчетах о недоставке

## формат сообщений;

Можно указать формат сообщений и набор знаков, которые должны использоваться для сообщений электронной почты, отправляемых в удаленные домены. Эти параметры можно использовать для обеспечения совместимости электронной почты, отправляемой пользователями из вашего домена в удаленный домен, с принимающей почтовой системой. Например, если известно, что в качестве системы обмена сообщениями удаленного домена выбрана программа Exchange, можно указать, чтобы в Exchange всегда использовался текстовый формат RTF. Дополнительные сведения см. в разделе [Преобразование содержимого](content-conversion-exchange-2013-help.md).

## Параметры автоматических ответов

Пользователи Exchange 2013 могут указать разные автоматические ответы для внутренних и внешних получателей. Кроме того, типы автоматических сообщений, которые доступны в организации, также зависят от используемой версии Microsoft Outlook.

В Exchange 2013 существует два типа автоматических ответов.

  - **Внешние**   Поддерживаются системами Exchange 2013 и Exchange 2010. Могут устанавливаться только в Outlook 2010 или Office Outlook 2007, или с помощью Microsoft Office Outlook Web App.

  - **Внутренние**   Поддерживаются системами Exchange 2013 и Exchange 2010. Могут устанавливаться только в Outlook 2010 или Outlook 2007, или с помощью Outlook Web App.

В следующей таблице описываются различные комбинации клиентов и серверов и типы автоматических ответов, которые используются в каждом сценарии.

**Клиенты и серверы, поддерживающие автоматические ответы**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Версия клиента</th>
<th>Версия сервера Exchange Server</th>
<th>Поддерживаемые автоматические ответы</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2010 или Outlook 2007</p></td>
<td><p>Exchange 2013Exchange 2010Exchange 2007</p></td>
<td><p>Внутренние, внешние</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013Exchange 2010Exchange 2007</p></td>
<td><p>Внутренние, внешние</p></td>
</tr>
</tbody>
</table>


## Управление информацией об отчетах о недоставке

Как говорилось в начале раздела, отправку отчетов о недоставке на удаленный домен можно предотвратить. Заблокировав отправку отчетов о недоставке на удаленный домен, вы можете предотвратить распространение информации из сообщения отчета о недоставке за пределы организации, ограничив таким образом тот объем сведений, который может получить о вашей организации пользователь-злоумышленник. Однако при этом законные отправители также не будут получать отчеты о недоставке, что приведет к путанице и снижению производительности.

Exchange 2013 обеспечивает точный контроль над содержимым отчета о недоставке, предназначенного для удаленного домена. С помощью Exchange 2013 можно разрешить отправку отчетов о недоставке на удаленный домен, при этом удалив из них все данные диагностики. Таким образом, можно предотвратить утечку сведений о развертывании Exchange из организации, обеспечивая в то же время отправку отчетов о недоставке внешним отправителям.

Данная возможность управляется с помощью параметра *NDRDiagnosticInfoEnabled* в командлете **Set-RemoteDomain**. Он позволяет настроить для каждого удаленного домена разные параметры в соответствии с потребностями организации. Например, можно исключить диагностическую информацию из отчета о недоставке для удаленного домена по умолчанию, но при этом предоставить ее в полном размере для удаленных доменов партнеров.

Для получения дополнительных сведений об этом новом параметре см. раздел [Set-RemoteDomain](https://technet.microsoft.com/ru-ru/library/aa997857\(v=exchg.150\)).
