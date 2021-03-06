﻿---
title: 'Требуется компонент расширяемости .NET для IIS 7_LonghornIIS7NetExt: Exchange 2013 Help'
TOCTitle: Требуется компонент расширяемости .NET для IIS 7_LonghornIIS7NetExt
ms:assetid: 8b481626-b68a-4fba-b66e-a02c03856bfd
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/ms.exch.setupreadiness.longhorniis7netext(v=EXCHG.150)
ms:contentKeyID: 50488591
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Требуется компонент расширяемости .NET для IIS 7\_LonghornIIS7NetExt

 

_**Применимо к:**Exchange Server_

_**Последнее изменение раздела:**2012-06-05_

Содержимое этой статьи не обновлялось для Microsoft Exchange Server 2013. Несмотря на отсутствие обновления, оно может быть применимо для Exchange 2013. Если вам все еще нужна помощь, ознакомьтесь с указанными ниже ресурсами сообщества.

Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) или [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Майкрософт® Невозможно продолжить установку сервера Microsoft Exchange Server 2010, поскольку на целевом сервере не установлен компонент расширяемости .NET для IIS 7.

Прежде чем использовать удаленное взаимодействие Windows PowerShell в Exchange 2010, на целевом сервере сначала должен быть установлен компонент расширяемости .NET для IIS 7

Чтобы устранить эту проблему, с помощью диспетчера сервера установите на этот сервер компонент расширяемости .NET для IIS 7 и повторно запустите программу установки Exchange 2010.

Установка компонента расширяемости .NET для IIS 7 на Windows Server 2008 или Windows Server 2008 R2 с помощью диспетчера сервера

1.  Нажмите кнопку **Пуск** и выберите пункт **Администрирование**, а затем — **Диспетчер сервера**.

2.  На левой панели переходов разверните **Роли**, затем щелкните правой кнопкой мыши **Веб-сервер (IIS)** и выберите **Добавить службы ролей**.

3.  В области **Выбор служб ролей** прокрутите список вниз до раздела **Разработка приложений**.

4.  Установите флажок **Расширяемость .NET**.

5.  В области **Выбор служб ролей** нажмите кнопку **Далее**, а затем в области **Подтверждение установки выбранных компонентов** нажмите кнопку **Установить**.

6.  Нажмите кнопку **Закрыть**, чтобы завершить работу мастера добавления служб ролей.

