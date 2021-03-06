﻿---
title: 'Политики адресов электронной почты: Exchange 2013 Help'
TOCTitle: Политики адресов электронной почты
ms:assetid: b63b63bb-6faf-4337-8441-50bc64b49bb8
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb232171(v=EXCHG.150)
ms:contentKeyID: 50488978
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Политики адресов электронной почты

 

_**Применимо к:**Exchange Server 2013_

_**Последнее изменение раздела:**2016-07-21_

Получатели (к которым относятся пользователи, ресурсы, контакты и группы) представляют собой объекты с включенной поддержкой почты в службе Active Directory, которым сервер Microsoft Exchange может доставлять или маршрутизировать сообщения. Чтобы получатель мог принимать или отправлять сообщения электронной почты, он должен иметь адрес электронной почты. Политики адресов электронной почты создают для ваших получателей основные и дополнительные адреса электронной почты, чтобы они могли получать и отправлять электронную почту.

По умолчанию сервер Exchange содержит политику адресов электронной почты для каждого пользователя с включенной поддержкой почты. Эта политика, используемая по умолчанию, задает псевдоним получателя в качестве локальной части адреса электронной почты и использует обслуживаемый домен по умолчанию. Локальная часть адреса электронной почты — это имя перед знаком @. Однако, способ отображения адресов электронной почты получателей можно изменить. Например, для адресов электронной почты можно задать вид *firstname*.*lastname*@contoso.com.

Более того, если необходимо указать дополнительные адреса электронной почты для всех получателей или только для подмножества, можно изменить политику по умолчанию или создать дополнительные политики. Например, почтовый ящик пользователя Владимира Егорова может получать сообщения электронной почты по адресу evladimir@mail.contoso.com и egorov.vladimir@mail.contoso.com.

Необходимы сведения о других задачах управления, связанных с политиками адресов электронной почты? См. раздел [Процедуры политики адресов электронной почты](email-address-policy-procedures-exchange-2013-help.md).

## Поведение политик получателей

Сервер Exchange применяет политику ко всем получателям, которые соответствуют критериям фильтрации получателей.

  - Политики получателей применяются в порядке убывания приоритета. В случае противоречий между политиками применяется политика с наивысшим приоритетом. Политика получателя по умолчанию имеет самый низкий приоритет и применяется, если другие политики не подходят.
    
    Если вы не укажете приоритет для политики получателя, ей будет присвоен наивысший приоритет. Если вы укажете приоритет, связанный с существующей политикой, ее приоритет и приоритет всех менее важных политик будет снижен. Новой политике будет присвоен указанный приоритет.
    
    Функция политики получателей разделена на две функции: обслуживаемые домены и политики адресов электронной почты. Дополнительные сведения об обслуживаемых доменах см. в разделе [Обслуживаемые домены](accepted-domains-exchange-2013-help.md).

  - При выполнении командлета **Update-EmailAddressPolicy** в командной консоли Exchange объект получателя обновляется вместе с политикой адресов электронной почты.

  - При каждом изменении и сохранении объекта получателя сервер Exchange выполняет принудительное применение правильных критериев и параметров адреса электронной почты. При изменении и сохранении политики адресов электронной почты выполняется обновление всех сопоставленных получателей. Кроме того, при изменении объекта получателя членство этого получателя в политике адресов электронной почты повторно оценивается и применяется.

## Создание политик адресов электронной почты

При создании политики адресов электронной почты используются следующие типы адресов электронной почты:

  - **Предустановленный адрес электронной почты SMTP**. *Предустановленные* SMTP-адреса электронной почты являются обычными адресами электронной почты, предоставляемыми пользователю.

  - **Настраиваемый адрес электронной почты SMTP**. Если пользователь не желает использовать предустановленные SMTP-адреса электронной почты, можно задать настраиваемый SMTP-адрес электронной почты.
    
    Переменные, перечисленные в приведенной ниже таблице, могут быть использованы для задания альтернативных значений для локальной части адреса при создании настраиваемого SMTP-адреса электронной почты.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Переменная</th>
    <th>Значение</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>Имя</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>Буква отчества</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>Фамилия</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>Краткое имя</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Псевдоним Exchange</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>Использование первых <em>x</em> букв фамилии. Например, если <em>x</em> = 2, используются первые две буквы фамилии.</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>Использование первых <em>x</em> букв имени. Например, если <em>x</em> = 2, используются первые две буквы имени.</p></td>
    </tr>
    </tbody>
    </table>


  - **Адрес электронной почты, не являющийся SMTP-адресом**. Поддерживаются следующие типы адресов электронной почты, которые не являются SMTP-адресами:
    
      - EX (устаревшее краткое имя префикса адреса прокси-сервера различающегося имени)
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - Lotus Notes
    
      - Novell GroupWise
    
      - Адрес прокси-сервера единой системы обмена сообщениями Exchange (адрес прокси-сервера EUM)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dd876857.important(EXCHG.150).gif" title="Важно" alt="Важно" />Важно!</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>На сервере Exchange все адреса электронной почты, не являющиеся SMTP-адресами, считаются настраиваемыми адресами. Сервер Exchange не предоставляет отдельных диалоговых окон или страниц свойств для типов адресов электронной почты X.400, GroupWise или Lotus Notes. При добавлении настраиваемого адреса электронной почты, не являющегося SMTP-адресом, необходимо иметь соответствующие файлы динамических библиотек (DLL-файлы). Если соответствующие DLL-файлы не предоставлены, то создать настраиваемую политику адресов электронной почты не удастся. В средстве просмотра событий будет зарегистрирована следующая ошибка: «Не найден объект описания адреса электронной почты в каталоге Microsoft Exchange для типа адреса &quot;SADF&quot; на компьютерах &quot;i386&quot;.»</td>
    </tr>
    </tbody>
    </table>


Подробные инструкции о том, как создать политику адреса электронной почты, см. в следующих разделах:

[Создание политики адресов электронной почты](create-an-email-address-policy-exchange-2013-help.md)

[Создание политики адресов электронной почты с помощью фильтров получателей](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)

