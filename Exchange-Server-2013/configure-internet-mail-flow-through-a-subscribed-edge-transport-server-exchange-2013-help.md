﻿---
title: 'Настройка потока почты Интернета через подписанный пограничный транспортный сервер: Exchange 2013 Help'
TOCTitle: Настройка потока обработки почты Интернета через пограничный транспортный сервер с подпиской
ms:assetid: d12ea770-99ce-4ab4-a373-96f2554641fa
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb738158(v=EXCHG.150)
ms:contentKeyID: 61183384
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Настройка потока почты Интернета через подписанный пограничный транспортный сервер

 

_**Применимо к:**Exchange Server 2013_

_**Последнее изменение раздела:**2015-04-08_

Чтобы обеспечить поток почты Интернета через пограничный транспортный сервер, необходимо подписать пограничный транспортный сервер на сайт Active Directory. При этом автоматически создаются два необходимые для потока почты Интернета соединители отправки:

  - соединитель отправки, настроенный для отправки сообщений электронной почты во все домены Интернета;

  - соединитель отправки, настроенный для отправки сообщений электронной почты с пограничного транспортного сервера на сервер почтовых ящиков Exchange 2013.

Если не нужно подписывать пограничный транспортный сервер на сайт Active Directory, можно создать соединители отправки, необходимые для организации потока почты между сервером почтовых ящиков и пограничным транспортным сервером. Дополнительные сведения см. в разделе [Настройка потока обработки почты через пограничный транспортный сервер без использования EdgeSync](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md). Однако рекомендуется подписывать пограничный транспортный сервер на сайт Active Directory всегда, когда это возможно.

## Приступая к работе

  - Предполагаемое время для завершения: 20 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "EdgeSync" и "Пограничные транспортные серверы" в разделе [Разрешения потока обработки почты](mail-flow-permissions-exchange-2013-help.md).

  - Прежде чем подписывать пограничный транспортный сервер, необходимо настроить доверенные домены и политики адресов электронной почты для своей организации Exchange.

  - Обеспечьте использование защищенного порта LDAP 50636/TCP через брандмауэр, отделяющего сеть периметра от организации Exchange. Пограничный транспортный сервер должен обмениваться данными со всеми серверами почтовых ящиков Exchange 2013 на подписанном сайте Active Directory.

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


## Настройка потока почты Интернета через подписанный пограничный транспортный сервер

1.  На пограничном транспортном сервере создайте файл пограничной подписки, используя следующий синтаксис.
    
        New-EdgeSubscription -FileName <FileName>.xml [-Force]
    
    В этом примере создается файл пограничной подписки с именем EdgeSubscriptionInfo.xml в папке C:\\My Documents. Параметр *Force* отклоняет запросы на подтверждение отключения команд и предупреждения о перезаписи данных конфигурации на пограничном транспортном сервере.
    
        New-EdgeSubscription -FileName "C:\My Documents\EdgeSubscriptionInfo.xml" -Force

2.  Скопируйте созданный файл пограничной подписки на сервер почтовых ящиков на сайте Active Directory, на который будет подписан пограничный транспортный сервер.

3.  На сервере почтовых ящиков используйте следующий синтаксис, чтобы импортировать файл пограничной подписки.
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "<FileName>.xml" -Encoding Byte -ReadCount 0)) -Site <SiteName>
    
    В этом примере файл пограничной подписки с именем EdgeSubscriptionInfo.xml импортируется с папки D:\\Data и пограничный транспортный сервер подписывается на сайт Active Directory с именем "Default-First-Site-Name".
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "D:\Data\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -Site "Default-First-Site-Name"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Чтобы предотвратить автоматическое создание одного или обоих соединителей отправки, используйте параметры <em>CreateInternetSendConnector</em> или <em>CreateInboundSendConnector</em>. Дополнительные сведения см. в разделе <a href="edge-subscriptions-exchange-2013-help.md">Пограничные подписки</a>.</td>
    </tr>
    </tbody>
    </table>


4.  На сервере почтовых ящиков запустите следующую команду, чтобы начать первую синхронизацию EdgeSync.
    
        Start-EdgeSynchronization

5.  По завершении настоятельно рекомендуется удалить файл пограничной подписки с пограничного транспортного сервера и с сервера почтовых ящиков. Файл пограничной подписки содержит сведения об учетных данных, используемых в процессе взаимодействия LDAP.

