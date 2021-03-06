﻿---
title: 'Отключение, отправка и прием факсов для группы пользователей: Exchange 2013 Help'
TOCTitle: Отключение, отправка и прием факсов для группы пользователей
ms:assetid: 1c57c3ba-2b0e-43dd-9b28-43bada1592c5
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ650864(v=EXCHG.150)
ms:contentKeyID: 52059111
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Отключение, отправка и прием факсов для группы пользователей

 

_**Применимо к:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:**2016-12-09_

Для пользователей, связанных с политикой почтовых ящиков единой системы обмена сообщениями, можно выключить функцию приема факсов. По умолчанию, когда вы включаете для пользователей поддержку единой системы обмена сообщениями, они не могут получать факсовые сообщения, пока вы не укажете универсальный код ресурса (URI) для факс-сервера, развернете факс-сервер для своей организации и включите передачу факсов в политике почтовых ящиков единой системы обмена сообщениями. Если параметр разрешения входящих факсов отключен в абонентской группе единой системы обмена сообщениями, пользователи, связанные с политикой почтовых ящиков единой системы обмена сообщениями, по-прежнему не смогут получать факсы. Подобно этому, если параметр включения входящих факсов отключен для определенного пользователя, он не сможет получать факсы.

Дополнительные сведения о факсов партнеров [Microsoft точно указать для партнеров факсов](https://go.microsoft.com/fwlink/?linkid=190238)см.

Дополнительные сведения об управленческих задачах, связанных с факсами, см. в разделе [Отправка и прием факсов процедур](faxing-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: менее 1 минуты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Политики почтовых ящиков единой системы обмена сообщениями» в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что абонентская группа единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание абонентской группы единой системы обмена сообщениями](create-a-um-dial-plan-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что политика почтовых ящиков единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание политики почтовых ящиков единой системы обмена сообщениями](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="Совет" alt="Совет" />Совет.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Что необходимо сделать?

## Использование Центра администрирования Exchange для отключения возможности приема факсов

1.  В Центре администрирования Exchange последовательно выберите пункты **Единая система обмена сообщениями** \> **Абонентские группы единой системы обмена сообщениями**. Выберите из списка абонентскую группу единой системы обмена сообщениями, которую необходимо изменить, и нажмите кнопку **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

2.  На странице **Абонентская группа единой системы обмена сообщениями** в разделе **Политики почтовых ящиков единой системы обмена сообщениями** выберите изменяемую политику и нажмите кнопку **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.  На странице **Политика почтовых ящиков единой системы обмена сообщениями** \> **Общие** снимите флажок рядом с пунктом **Разрешить получение факсов**.

4.  Нажмите кнопку **Сохранить**, чтобы сохранить изменения.

## Использование командной консоли для отключения возможности приема факсов

В этом примере пользователям, связанным с политикой почтовых ящиков единой системы обмена сообщениями `MyUMMailboxPolicy`, запрещается принимать факсы.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowFax $false

