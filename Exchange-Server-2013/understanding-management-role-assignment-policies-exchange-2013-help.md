﻿---
title: 'Общие сведения о политиках назначения ролей управления: Exchange 2013 Help'
TOCTitle: Общие сведения о политиках назначения ролей управления
ms:assetid: 25913e43-326a-4371-90b5-021a35f100fe
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd638100(v=EXCHG.150)
ms:contentKeyID: 50487630
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Общие сведения о политиках назначения ролей управления

 

_**Применимо к:**Exchange Online, Exchange Server 2013_

_**Последнее изменение раздела:**2015-03-09_

*Политика назначения ролей управления* — это набор из одной или нескольких ролей управления конечного пользователя, которые позволяют конечным пользователям управлять конфигурацией их собственного почтового ящика Microsoft Exchange Server 2013 и группы рассылки. Политики назначения ролей, которые являются в Exchange 2013 частью модели разрешений управления доступом на основе ролей (RBAC), позволяют определять, какие параметры конфигурации почтового ящика и группы рассылки может изменять конечный пользователь. Политики назначения ролей можно определять для различных групп пользователей.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>В этом разделе рассматриваются расширенные возможности управления доступом на основе ролей (RBAC). Сведения об управлении базовыми разрешениями Exchange 2013, такими как использование Центра администрирования Exchange для добавления и удаления участников групп ролей, создания и изменения групп ролей, а также создания и изменения политик назначения ролей, см. в разделе <a href="permissions-exchange-2013-help.md">Разрешения</a>.</td>
</tr>
</tbody>
</table>


Дополнительные сведения об управлении доступом на основе ролей см. в разделе [Общие сведения об управлении доступом на основе ролей](understanding-role-based-access-control-exchange-2013-help.md).

**Содержание**

Уровни политики назначения ролей

Политики назначения явных ролей и ролей по умолчанию

Использование политик назначения ролей

Управление политикой назначения ролей

## Уровни политики назначения ролей

Ниже перечислены различные уровни, составляющие модель политики назначения ролей.

  - **Почтовый ящик**   Для почтовых ящиков назначается одна политика назначения ролей. Если для почтового ящика назначается политика назначения ролей, назначения между ролями управления и политикой назначения ролей применяются к этому почтовому ящику. Для данного почтового ящика будут предоставлены разрешения, предусмотренные ролями управления.

  - **Политика назначения ролей управления**. *Политика назначения ролей управления* является специальным объектом в Exchange 2013. Пользователям присваивается политика назначения ролей при создании почтовых ящиков или при изменении политики назначения ролей для почтового ящика. Она также назначается для ролей управления конечных пользователей. Сочетание всех ролей в политике назначения ролей определяет для пользователя все функции управления почтовым ящиком или группами рассылки.

  - **Назначение роли управления**   *Назначение роли управления* связывает роль управления с политикой назначения ролей. Назначение роли управления политике назначения ролей позволяет использовать командлеты и параметры, определенные в роли управления. При создании назначения ролей между политикой назначения ролей и ролью управления можно указать только определенную область. Область, применяемая назначением, зависит от роли управления и является `Self` или `MyGAL`. Дополнительные сведения см. в разделе [Общие сведения о назначениях ролей управления](understanding-management-role-assignments-exchange-2013-help.md).

  - **Роль управления**   *Роль управления* — это контейнер для группировки записей ролей управления. Роли позволяют указывать определенные задачи, которые пользователь может выполнять с почтовым ящиком или группами рассылки. *Запись роли управления* — это командлет, сценарий или специальное разрешение, которое позволяет выполнять определенную задачу, связанную с ролью управления. С политиками назначения ролей можно использовать только роли управления конечных пользователей. Дополнительные сведения см. в разделе [Общие сведения о ролях управления](understanding-management-roles-exchange-2013-help.md).

  - **Запись роли управления**   Записи роли управления — это отдельные записи в роли управления, определяющие командлеты и параметры, доступные для роли управления и группы ролей. Каждая запись роли включает в себя один командлет и параметры, доступ к которым можно получить с помощью роли управления.

На следующем рисунке изображены все вышеперечисленные уровни политики назначения ролей и взаимосвязи этих уровней.

**Модель политики назначения ролей управления**

![Связи модели назначения роли](images/Dd638100.7f7c11ca-0d61-464d-98a3-a9991ec811b5(EXCHG.150).jpg "Связи модели назначения роли")

Дополнительные сведения о ролях управления, назначениях ролей и областях см. в разделе [Общие сведения об управлении доступом на основе ролей](understanding-role-based-access-control-exchange-2013-help.md).

## Политики назначения явных ролей и ролей по умолчанию

В следующих разделах описаны два типа политик назначения ролей в Exchange 2013. 

## Политика назначения ролей по умолчанию

Политика назначения ролей по умолчанию — это политика, присваиваемая почтовому ящику при его создании или перемещении на сервер под управлением Exchange 2013. Политика назначения ролей не предоставляется с помощью параметра *RoleAssignmentPolicy* для командлетов **New-Mailbox** или **Enable-Mailbox**.

Exchange 2013 включает в себя политику назначения ролей по умолчанию, которая предоставляет конечным пользователям наиболее распространенные разрешения. Разрешения по умолчанию можно изменить в политике назначения ролей по умолчанию. Для этого необходимо добавить или удалить роли управления в политике назначения ролей.

Чтобы заменить встроенную политику назначения ролей по умолчанию на собственную политику, можно использовать командлет **Set-RoleAssignmentPolicy** для выбора новой политики назначения ролей по умолчанию. После этого политике назначения ролей будут назначены новые указанные по умолчанию почтовые ящики, если политика назначения ролей не была указана явно.

При изменении политики назначения ролей по умолчанию почтовые ящики, назначенные для политики назначения ролей по умолчанию, не назначаются автоматически новой политике назначения ролей по умолчанию. Чтобы обновить предварительно созданные почтовые ящики для использования установленной по умолчанию политикой назначения ролей, необходимо использовать командлет **Set-Mailbox**.

## Политика назначения явных ролей

Политика назначения явных ролей — это политика, назначенная пользователем почтовому ящику вручную с помощью параметра *RoleAssignmentPolicy* для командлетов **New-Mailbox**, **Set-Mailbox** или **Enable-Mailbox**. При назначении политики назначения явных ролей новая политика применяется немедленно и заменяет ранее назначенную политику назначения явных ролей.

## Использование политик назначения ролей

Политики назначения ролей позволяют настроить разрешения для пользователей, исходя из потребностей предприятия, которые необходимо настроить пользователям. Если политика назначения ролей по умолчанию соответствует требованиям предприятия, не требуется выполнять настройку. Тем не менее, при наличии различных групп пользователей с особыми потребностями можно создать политику назначения ролей для каждой их них.

Используемая политика назначения ролей по умолчанию должна содержать разрешения, применяемые для максимально широкого круга пользователей. Затем создайте политики назначения ролей для каждой из указанных групп пользователей, настройте эти политики назначения ролей и получите для них более или менее ограниченные разрешения. При такой организации политик назначения ролей упрощение достигается с помощью явного назначения политик указанным пользователям. При этом большинству пользователей присваиваются наиболее распространенные разрешения, предоставляемые политикой назначения ролей по умолчанию.

Почтовый ящик может иметь только одну политику назначения ролей. Все пользователи, включая администраторов и специалистов, получают по одной политике назначения ролей. Чтобы присвоить пользователю другой набор разрешений, для почтового ящика этого пользователя необходимо назначить другую политику назначения ролей, содержащую необходимые разрешения.

## Управление политикой назначения ролей

Чтобы добавить новую политику назначения ролей, ее необходимо создать и определить, будет ли она являться политикой назначения ролей по умолчанию. После создания политики назначения ролей необходимо назначить роли управления этой политике, а затем назначить политику назначения ролей почтовым ящикам. Затем можно добавлять или удалять роли управления, а также выбрать другую политику назначения ролей политикой по умолчанию.

В следующей таблице перечислены уровни политики назначения ролей и разделы с описанием процедур, позволяющих управлять каждым уровнем.

### Разделы по управлению политикой назначения ролей

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Уровень модели политики назначения ролей</th>
<th>Разделы по управлению</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Почтовый ящик</p></td>
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">Управление почтовыми ящиками пользователей</a></p>
<p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Изменение политики назначения для почтового ящика</a></p></td>
</tr>
<tr class="even">
<td><p>Политика назначения ролей</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Управление политиками назначения ролей</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Роли управления и их назначения</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Управление политиками назначения ролей</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Записи ролей управления</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">Добавьте запись роли в роли</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">Изменение записи роли</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">Удаление записи роли из роли</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Изменение записей ролей управления в ролях управления политики назначения ролей — это сложная задача, выполнение которой в большинстве случаев не требуется. Вместо этого можно использовать уже существующую роль управления, которая удовлетворяет требованиям пользователя. Дополнительные сведения см. в разделе <a href="built-in-role-groups-exchange-2013-help.md">Встроенные группы ролей</a>.</td>
</tr>
</tbody>
</table>

</td>
</tr>
</tbody>
</table>

