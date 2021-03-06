﻿---
title: 'Включение и отключение поддержки почты для общедоступной папки: Exchange 2013 Help'
TOCTitle: Включение и отключение поддержки почты для общедоступной папки
ms:assetid: 3d69f76d-ff3c-46c1-b962-6a1baa425d8a
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Aa997560(v=EXCHG.150)
ms:contentKeyID: 50487860
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Включение и отключение поддержки почты для общедоступной папки

 

_**Применимо к:**Exchange Online, Exchange Server 2013_

_**Последнее изменение раздела:**2016-06-15_

Общие папки предназначены для осуществления общего доступа к файлам. Это простой и эффективный способ сбора, организации и использования информации внутри рабочей группы или в масштабах всей организации. Включение почты для общедоступной папки позволяет пользователям помещать в нее файлы, отправляя сообщения электронной почты. Если для общедоступной папки включена поддержка почты, в Центре администрирования Exchange для нее становятся доступны дополнительные параметры, например адреса электронной почты и почтовые квоты. Если поддержка почты не включена, для управления параметрами общедоступной папки в командной консоли используется командлет **Set-PublicFolder**. Если же она включена, для этого используются командлеты **Set-PublicFolder** и **Set-MailPublicFolder**.

Чтобы пользователи могли по Интернету отправлять сообщения в общедоступную папку с включенной поддержкой почты, необходимо задать дополнительные разрешения с помощью командлета **Add-PublicFolderClientPermission**.

Дополнительные сведения о задачах, связанных с управлением общедоступными папками, см. в разделе [Процедуры с общедоступными папками](public-folder-procedures-exchange-2013-help.md).

Дополнительные сведения о задачах управления, связанных с общедоступными папками, см. в разделе [Процедуры с общедоступными папками в Office 365 и Exchange Online](https://technet.microsoft.com/ru-ru/library/jj966272\(v=exchg.150\)).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: 5 минут.

  - Чтобы пользователи могли по Интернету отправлять сообщения электронной почты в общедоступную папку с включенной поддержкой почты, общедоступная папка должна иметь по крайней мере право доступа *CreateItems*, предоставленное анонимной учетной записи. Подробнее см. в разделе Предоставление анонимным пользователям разрешения на отправку сообщений в общедоступную папку с включенной поддержкой почты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "Общедоступные папки" в разделе [Разрешения на общий доступ и совместную работу](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="Совет" alt="Совет" />Совет.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Что необходимо сделать?

## Включение или отключение поддержки почты для общедоступной папки с помощью Центра администрирования Exchange

1.  Последовательно выберите пункты **Общедоступные папки** \> **Общедоступные папки**.

2.  В представлении списка выберите общедоступную папку, для которой нужно включить или отключить поддержку почты.

3.  В области сведений в разделе **Настройки почты** щелкните **Включить** или **Отключить**.

4.  Появится предупреждение с запросом на подтверждение действия. Чтобы продолжить, нажмите кнопку **Да**.

Чтобы внешние пользователи могли отправлять сообщения в эту общедоступную папку, обязательно выполните действия, приведенные в разделе Предоставление анонимным пользователям разрешения на отправку сообщений в общедоступную папку с включенной поддержкой почты.

## Включение поддержки почты для общедоступной папки с помощью командной консоли

В этом примере включается поддержка почты для общедоступной папки Help Desk.

    Enable-MailPublicFolder -Identity "\Help Desk"

В этом примере включается поддержка почты для общедоступной папки Reports в родительской папке Marketing, но папка скрывается в списках адресов.

    Enable-MailPublicFolder -Identity "\Marketing\Reports" -HiddenFromAddressListsEnabled $True

Чтобы внешние пользователи могли отправлять сообщения в эту общедоступную папку, обязательно выполните действия, приведенные в разделе Предоставление анонимным пользователям разрешения на отправку сообщений в общедоступную папку с включенной поддержкой почты.

Подробные сведения о синтаксисе и параметрах см. в разделе [Enable-MailPublicFolder](https://technet.microsoft.com/ru-ru/library/aa998824\(v=exchg.150\)).

## Отключение поддержки почты для общедоступной папки с помощью командной консоли

В этом примере отключается поддержка почты для общедоступной папки Marketing\\Reports.

    Disable-MailPublicFolder -Identity "\Marketing\Reports"

Подробные сведения о синтаксисе и параметрах см. в разделе [Disable-MailPublicFolder](https://technet.microsoft.com/ru-ru/library/bb123781\(v=exchg.150\)).

## Предоставление анонимным пользователям разрешения на отправку сообщений в общедоступную папку с включенной поддержкой почты

Задать разрешения для анонимной учетной записи общедоступной папки можно с помощью Outlook или командной консоли. Задать разрешения для анонимной учетной записи с помощью Центра администрирования Exchange нельзя.

**Задание разрешений для анонимной учетной записи с помощью Outlook**

1.  Откройте Outlook с учетной записи, которой предоставлены разрешения владельца для общедоступной папки с включенной поддержкой электронной почты, в которую будут отправлять сообщения анонимные пользователи.

2.  Перейдите к разделу **Общедоступные папки — \<имя\_пользователя\>**.

3.  Перейдите в общедоступную папку, которую требуется изменить.

4.  Щелкните общедоступную папку правой кнопкой мыши, нажмите кнопку **Свойства**, а затем выберите вкладку **Разрешения**.

5.  Выберите **анонимную** учетную запись, щелкните **Создание элементов** в разделе **Запись**, а затем нажмите кнопку **ОК**.

**Задание разрешений для анонимной учетной записи с помощью командной консоли**

В этом примере устанавливается разрешение `CreateItems` для анонимной учетной записи в общедоступной папке с включенной поддержкой почты "Отзывы клиентов".

    Add-PublicFolderClientPermission "\Customer Feedback" -AccessRights CreateItems -User Anonymous

Дополнительные сведения о синтаксисе и параметрах см. в разделе [Add-PublicFolderClientPermission](https://technet.microsoft.com/ru-ru/library/bb124743\(v=exchg.150\)).

