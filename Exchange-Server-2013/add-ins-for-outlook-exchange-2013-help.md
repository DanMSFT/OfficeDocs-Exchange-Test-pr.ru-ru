﻿---
title: 'Приложения для Outlook: Exchange 2013 Help'
TOCTitle: Приложения для Outlook
ms:assetid: 28b6f2a1-a235-4023-b561-6fd304962775
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ943753(v=EXCHG.150)
ms:contentKeyID: 52061211
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Приложения для Outlook

 

_**Применимо к:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2017-03-13_

**Сводка.** Обзор надстроек Outlook, работающих на компьютерах с Windows и Mac OS, на мобильных устройствах, а также в Outlook Web App и Outlook в Интернете.

Надстройки Outlook — это приложения, которые увеличивают эффективность клиентов Outlook, предоставляя пользователям сведения или инструменты, которые можно применять непосредственно в Outlook. Надстройки создаются сторонними разработчиками и могут быть установлены с помощью файла, URL-адреса либо Магазина Office. По умолчанию надстройки могут устанавливать все пользователи. Администраторы Exchange могут использовать роли для управления правами пользователей на установку надстроек.

> [!TIP]  
> Сведения о надстройках Outlook, предназначенные для пользователей, см. в разделе справки <a href="https://go.microsoft.com/fwlink/p/?linkid=2823">Установленные надстройки</a> на веб-сайте Office.com. В этом разделе приведен обзор надстроек, а также указаны некоторые надстройки Outlook, которые могут быть установлены по умолчанию. 


## Надстройки из Магазина Office и пользовательские надстройки

Клиенты Outlook поддерживают обширный набор надстроек, доступных в Магазине Office. Outlook также поддерживает пользовательские надстройки, которые можно создавать и распространять для пользователей в организации.

> [!NOTE]  
> Доступ к Магазину Office не поддерживается для почтовых ящиков или организаций в определенных регионах. Если после выбора элементов <strong>Центр администрирования Exchange</strong> &gt; <strong>Организация</strong> &gt; <strong>Надстройки</strong> &gt; <img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Значок добавления" alt="Значок добавления" /> вы не видите параметр <strong>Добавить из Магазина Office</strong>, попробуйте установить надстройку Outlook, используя URL-адрес или путь к файлу. За дополнительными сведениями обращайтесь к поставщику службы. 


> [!NOTE]  
> Некоторые надстройки Outlook устанавливаются по умолчанию. Такие надстройки активируются только для содержимого на английском языке. Например, надстройка &quot;Карты Bing&quot; не будет активироваться в случае немецких почтовых адресов в сообщении. 


## Доступ к надстройкам и их установка

По умолчанию надстройки могут устанавливать и удалять все пользователи. Администраторы Exchange могут управлять надстройками и доступом пользователей к ним. Администраторы могут запретить пользователям устанавливать надстройки, не скачанные из Магазина Office (использовать для этого файл или URL-адрес). Администраторы также могут запретить пользователям устанавливать надстройки из Магазина Office, а также устанавливать надстройки от имени других пользователей. Кроме того, можно назначать пользователям роли, позволяющие им устанавливать надстройки для организации или для подмножества пользователей в ней.

Чтобы запретить пользователям устанавливать надстройки не из Магазина Office, удалите для них роль **Мои пользовательские приложения**. Чтобы запретить пользователям устанавливать надстройки из Магазина Office, удалите для них роль **Мои приложения из Marketplace**. Дополнительные сведения см. в статье [Выбор администраторов и пользователей, которые могут устанавливать надстройки для Outlook и управлять ими](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

Сведения об установке надстроек для некоторых или всех пользователей в организации см. в статье [Установка и удаление приложений для Outlook в организации](install-or-remove-add-ins-for-outlook-for-your-organization-exchange-2013-help.md).

При необходимости можно ограничить доступ к надстройке для определенных пользователей в организации. Дополнительные сведения см. в статье [Управление доступом пользователей к приложениям для Outlook](manage-user-access-to-add-ins-for-outlook-exchange-online-help.md).

## Основные задачи администрирования надстроек для Outlook

Существует несколько основных сценариев, которыми управляют администраторы Exchange в своих организациях.

**Если вы хотите запретить пользователям устанавливать надстройки для Outlook на всех клиентах Outlook, внесите следующие изменения в Центре администрирования Exchange**:

  - Чтобы запретить пользователям устанавливать надстройки из Магазина Office, удалите роль **My Marketplace**.

  - Чтобы запретить пользователям загружать надстройки из других источников, удалите роль **My Custom Apps**.

  - Чтобы запретить пользователям устанавливать все надстройки, удалите обе указанные выше роли.

Дополнительные сведения см. в статье [Выбор администраторов и пользователей, которые могут устанавливать надстройки для Outlook и управлять ими](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

**Если вы хотите закрыть доступ к уже установленным надстройкам, используйте командлет `Get-App`, чтобы просмотреть список этих надстроек.**

После этого используйте командлет `Remove-App`, чтобы удалить их. 

Дополнительные сведения касательно Exchange 2013 см. в статьях [Get-App](https://technet.microsoft.com/ru-ru/library/jj218673\(v=exchg.150\)) и [Remove-App](https://technet.microsoft.com/ru-ru/library/jj218709\(v=exchg.150\)), касательно Exchange Online или Exchange 2016 — [здесь](https://go.microsoft.com/fwlink/p/?linkid=8447).

## Предоставление администраторам и пользователям возможности установки надстроек

Вы можете указать, кто из администраторов в организации сможет устанавливать надстройки Outlook и управлять ими. Кроме того, можно указать, кто из пользователей в организации сможет устанавливать надстройки для собственных нужд и управлять ими. Дополнительные сведения см. в статье [Выбор администраторов и пользователей, которые могут устанавливать надстройки для Outlook и управлять ими](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).
