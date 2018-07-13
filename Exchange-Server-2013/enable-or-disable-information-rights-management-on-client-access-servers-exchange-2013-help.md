﻿---
title: 'Включение и отключение управления правами на доступ к данным на серверах клиентского доступа: Exchange 2013 Help'
TOCTitle: Включение и отключение управления правами на доступ к данным на серверах клиентского доступа
ms:assetid: c7ce069b-a572-4755-90a3-7105472e4c83
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd876938(v=EXCHG.150)
ms:contentKeyID: 50489141
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Включение и отключение управления правами на доступ к данным на серверах клиентского доступа

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2016-12-09_

При включении системы управления правами на доступ к данным (IRM) на серверах клиентского доступа будут включены следующие компоненты:

  - Microsoft Office Outlook Web App

  - IRM в Microsoft Exchange ActiveSync

Если на серверах клиентского доступа включена служба управления правами на доступ к данным, пользователи Outlook Web App могут установить защиту сообщений с помощью применения шаблона [Службы управления правами Active Directory (AD RMS)](https://technet.microsoft.com/ru-ru/library/hh831364.aspx), созданного на кластере службы AD RMS. Пользователи Outlook Web App также могут просматривать сообщения с установленной защитой службы управления правами на доступ к данным и включенной службой поддержки вложений. Перед включением службы управления правами на доступ к данным на серверах клиентского доступа необходимо добавить федеративный почтовый ящик к группе суперпользователей на кластере службы AD RMS.

> [!IMPORTANT]  
> Участникам группы суперпользователей предоставляется лицензия на частное использование при запросе лицензии из кластера AD RMS. Это позволит им расшифровывать все содержимое, защищенное RMS в этом кластере.


Дополнительные сведения об управленческих задачах, связанных с IRM, см. в разделе [Сведения о процедуры управления правами](information-rights-management-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы?

  - Предполагаемое время выполнения: 1 минута.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "Конфигурация службы управления информационными правами (IRM)" в разделе [Политика обмена сообщениями и разрешения для соответствия требованиям](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Кластер службы управления правами Active Directory нужно установить в лесу Active Directory.

  - Почтовый ящик федерации добавлен в группу суперпользователей AD RMS. Подробные инструкции см. в разделе [Добавление федеративного почтового ящика в группу суперпользователей службы управления правами Active Directory](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Функции IRM в организации должны быть включены. Подробные инструкции см. в разделе [Включение или отключение управления правами на доступ к данным для внутренних сообщений](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - Командлет **Set-IRMConfiguration** позволяет включать или выключать систему IRM в Outlook Web App и IRM в Exchange ActiveSync для всей организации Exchange или на определенных уровнях.
    
    Можно управлять IRM в Outlook Web App на следующих уровнях:
    
      - **По виртуальному каталогу Outlook Web App**   Чтобы включить или отключить управление правами на доступ к данным в Outlook Web App для виртуального каталога Outlook Web App, используйте командлет **Set-OWAVirtualDirectory**, установив для параметра *IRMEnabled* значение `$false` или `$true` (по умолчанию). Это позволяет отключить управление правами на доступ к данным в Outlook Web App для одного виртуального каталога на сервере клиентского доступа Exchange 2013, оставив эту функцию включенной для другого виртуального каталога на другом сервере клиентского доступа.
    
      - **По политике почтовых ящиков Outlook Web App**   Чтобы включить или отключить управление правами на доступ к данным в Outlook Web App для политики почтовых ящиков Outlook Web App, используйте командлет **Set-OWAMailboxPolicy**, установив для параметра *IRMEnabled* значение `$false` или `$true` (по умолчанию). Это позволяет включить управление правами на доступ к данным в Outlook Web App для одного набора пользователей и отключить для другого, назначив им другую политику почтовых ящиков Outlook Web App.
    
    Систему управления правами на доступ к данным в Exchange ActiveSync можно настраивать отдельно для политик почтовых ящиков Exchange ActiveSync. Чтобы отключить или включить IRM в Exchange ActiveSync для политики почтовых ящиков Exchange ActiveSync, используйте командлет **Set-ActiveSyncMailboxPolicy** и установите параметр *IRMEnabled* в значение `$false` или `$true` (по умолчанию). Это позволяет включить управление правами на доступ к данным в Exchange ActiveSync для одного набора пользователей и отключить для другого, назначив им другую политику почтовых ящиков Exchange ActiveSync.

  - Для включения или выключения управления правами на доступ к данным на серверах клиентского доступа невозможно использовать Центр администрирования Exchange. Необходимо использовать командную консоль.

## Что необходимо сделать?

## Использование командной строки для включения IRM на серверах клиентского доступа

В этом примере выполняется включение IRM на сервере клиентского доступа для организации Exchange.

    Set-IRMConfiguration -ClientAccessServerEnabled $true

Дополнительные сведения о синтаксисе и параметрах см. в разделе [Set-IRMConfiguration](https://technet.microsoft.com/ru-ru/library/dd979792\(v=exchg.150\)).

## Использование командной строки для отключения IRM на серверах клиентского доступа

В этом примере выполняется отключение IRM на сервере клиентского доступа для организации Exchange.

    Set-IRMConfiguration -ClientAccessServerEnabled $false

Дополнительные сведения о синтаксисе и параметрах см. в разделе [Set-IRMConfiguration](https://technet.microsoft.com/ru-ru/library/dd979792\(v=exchg.150\)).

## Как проверить, что все получилось?

Чтобы убедиться, что IRM успешно включена или отключена на серверах клиентского доступа, выполните такие действия:

  - Выполните командлет **Get-IRMConfiguration** и проверьте значение свойства *ClientAccessServerEnabled*.
    
    Пример извлечения информации IRM см. в разделе [Examples](https://technet.microsoft.com/ru-ru/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) в описании командлета **Get-IRMConfiguration**.

  - Для создания или чтения сообщений с установленной защитой IRM используется Outlook Web App .
