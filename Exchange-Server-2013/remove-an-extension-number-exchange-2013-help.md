﻿---
title: 'Удалить добавочный номер: Exchange 2013 Help'
TOCTitle: Удалить добавочный номер
ms:assetid: c2b896cf-21f7-4453-a4e6-b23d236a6dd3
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd351124(v=EXCHG.150)
ms:contentKeyID: 50556451
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Удалить добавочный номер

 

_**Применимо к:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:**2016-07-21_

При включении единой системы обмена сообщениями для пользователя и его связывания с абонентской группой добавочных телефонных номеров создается прокси-адрес единой системы обмена сообщениями, содержащий пользовательский добавочный номер. Необходимо определить по крайней мере один добавочный номер, который будет использоваться единой системой обмена сообщениями для отправки голосовой почты в почтовый ящик пользователя. Добавочный номер также используется, когда пользователь вызывает номер голосового доступа к Outlook.

Можно удалить основной добавочный номер, добавленный при включении поддержки единой системы обмена сообщениями, или дополнительный, который был добавлен позже, а также связанные с пользователем прокси-адреса EUM. Основной добавочный номер, добавленныйй при включении поддержки единой системы обмена сообщениями, будет указан как основной прокси-адрес EUM. Любые дополнительные добавочные номера, добавленные вами, будут указаны как дополнительные прокси-адреса EUM. Когда удаляется добавочный номер, абоненты не cмогут оставить сообщение голосовой почты для пользователя через добавочный номер, который был удален.

При удалении основного добавочного номера единая система обмена сообщениями не сможет отправлять сообщения голосовой почты в почтовый ящик пользователя, и правила автоответчика не будут обрабатываться. Когда основной первичный добавочный номер удален, прокси-адрес единой системы обмена сообщениями для пользователя будет отображаться как **NULL** в почтовом ящике пользователя в EAC и при выполнении командлета **Get-Mailbox** в командной консоли Exchange. Кроме того, при выполнении командлета **Get-UMMailbox** параметры *Extensions*, *PhoneNumber* и *CallAnsweringRulesExtensions* будут пустыми или равными NULL.

Можно использовать EAC или командную консоль Exchange, чтобы удалить основной или дополнительный добавочный номер. Можно использовать страницу **Адрес электронной почты** в почтовом ящике пользователя в EAC, чтобы удалить основной или дополнительный добавочный номер. Нельзя использовать страницу **Почтовый ящик единой системы обмена сообщениями** в EAC, чтобы удалить основной добавочный номер, но ее можно использовать для удаления дополнительных добавочных номеров.

Можно просмотреть основной и дополнительный добавочные номера пользователя с помощью командлета **Get-UMMailbox** или **Get-Mailbox** в командной консоли Exchange.

Дополнительные задачи управления, связанные с пользователями, задействованными для голосовой почты, см. в разделе [Процедуры пользователя голосовой почты](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы?

  - Осталось времени до завершения: 3 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Почтовые ящики единой системы обмена сообщениями» в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Перед выполнением этой процедуры убедитесь, что абонентская группа единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание абонентской группы единой системы обмена сообщениями](create-a-um-dial-plan-exchange-2013-help.md).

  - Перед выполнением этой процедуры убедитесь, что политика почтовых ящиков единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание политики почтовых ящиков единой системы обмена сообщениями](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Прежде чем выполнить эти процедуры, убедитесь, что для почтового ящика этого пользователя включена поддержка единой системы обмена сообщениями, и он связан с абонентской группой, использующей добавочные номера. Дополнительные сведения см. в разделе [Включение для пользователя поддержки голосовой почты](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Прежде чем выполнить эти процедуры, убедитесь, что основной и дополнительные добавочные номера для пользователя настроены.

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

## Использование EAC для удаления основного или дополнительного добавочного номера

1.  В центре администрирования Exchange перейдите к разделу **Получатели** \> **Почтовые ящики**.

2.  Выберите из списка почтовый ящик, номер которого необходимо удалить, и нажмите кнопку **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.  На странице **Почтовый ящик пользователя** в разделе **Адрес электронной почты** выберите удаляемый номер и нажмите кнопку **Правка**![Значок удаления](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Значок удаления"). Основной прокси-адрес единой системы обмена сообщениями или добавочный номер указан полужирным шрифтом.

4.  Нажмите кнопку **Сохранить**.

## Использование EAC для удаления дополнительного добавочного номера

1.  В центре администрирования Exchange перейдите к разделу **Получатели** \> **Почтовые ящики**.

2.  В представлении списка выберите пользователя, в почтовом ящике которого необходимо удалить добавочный номер.

3.  В области сведений откройте раздел **Телефонные и голосовые функции** \> **Единая системы обмена сообщениями** и нажмите кнопку **Показать сведения**.

4.  На странице **Другие добавочные номера** в поле **Добавочный номер** выберите удаляемый номер и нажмите кнопку **Удалить**![Значок удаления](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Значок удаления").

5.  Нажмите кнопку **Сохранить**.

## Использование командной консоли для удаления добавочного номера

В данном примере удаляется добавочный номер 12345 из почтового ящика пользователя единой системы обмена сообщениями Tony Smith.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Прежде чем удалить добавочный номер с помощью командной консоли, необходимо определить положение прокси-адреса, который требуется изменить. Чтобы определить позицию, используйте команду <strong>$mbx.EmailAddresses</strong>. Первый в списке прокси-адрес имеет значение 0.</td>
</tr>
</tbody>
</table>


    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.remove("eum:22222;phone-context=MyDialPlan.contoso.com") 
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

