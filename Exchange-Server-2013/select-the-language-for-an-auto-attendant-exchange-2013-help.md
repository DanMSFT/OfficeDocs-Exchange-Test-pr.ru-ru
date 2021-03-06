﻿---
title: 'Выберите язык для автосекретарю.: Exchange 2013 Help'
TOCTitle: Выберите язык для автосекретарю.
ms:assetid: 3a1c1ec0-c726-41fb-a294-59faab205609
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Aa997306(v=EXCHG.150)
ms:contentKeyID: 50556361
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Выберите язык для автосекретарю.

 

_**Применимо к:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:**2016-12-09_

Можно настроить параметр языка приглашений по умолчанию в автосекретаре единой системы обмена сообщениями. Параметр языка, доступный в автосекретаре единой системы обмена сообщениями, позволяет задавать для автосекретаря язык приглашений по умолчанию. При использовании для автосекретаря системных приглашений по умолчанию они воспроизводятся на языке, который слышит звонящий абонент, когда автосекретарь отвечает на входящий вызов. Этот параметр языка применяется только к системным приглашениям по умолчанию, которые воспроизводятся после установки сервера почтовых ящиков, работающего под управлением единой системы обмена сообщениями Microsoft Exchange. Однако данный параметр не оказывает влияния на настраиваемые приглашения, заданные в автосекретаре. Набор доступных языков зависит от языковых пакетов единой системы обмена сообщениями, которые установлены на сервере почтовых ящиков.

Каждый автосекретарь, создаваемых изначально будет использовать английский (en US) языком по умолчанию. Языковой пакет английский (en US) устанавливается по умолчанию во всех версиях Майкрософт Exchange 2013 и не может быть удалена. Если вы хотите выбрать другой язык, например, немецкий (de-DE), необходимо загрузить немецкого единой системы обмена СООБЩЕНИЯМИ языковой пакет .exe файл из [Exchange Server 2013 единой системы обмена СООБЩЕНИЯМИ языковые пакеты](https://go.microsoft.com/fwlink/?linkid=266542) и установите языковой пакет единой системы обмена СООБЩЕНИЯМИ на сервере почтовых ящиков с помощью файла установки UMLanguagePack.de de.exe. После установки языкового пакета единой системы обмена СООБЩЕНИЯМИ можно задать язык по умолчанию для языка, отличного от английского (en US) на Автосекретари единой системы обмена СООБЩЕНИЯМИ.

Дополнительные сведения о языках единой системы обмена сообщениями см. в статье [Языки, приглашения и приветствий процедуры единой системы обмена СООБЩЕНИЯМИ](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: менее 1 минуты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Автосекретари единой системы обмена сообщениями» в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что абонентская группа единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание абонентской группы единой системы обмена сообщениями](create-a-um-dial-plan-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что автосекретарь единой системы обмена сообщениями создан. Дополнительные сведения см. в разделе [Создание автосекретаря единой системы обмена сообщениями](create-a-um-auto-attendant-exchange-2013-help.md).

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

## Использование Центра администрирования Exchange для настройки параметра языка по умолчанию

1.  В Центре администрирования Exchange последовательно выберите пункты **Единая система обмена сообщениями** \> **Абонентские группы единой системы обмена сообщениями**.

2.  Выберите из списка абонентскую группу единой системы обмена сообщениями, которую необходимо изменить, а затем на панели инструментов нажмите кнопку **Изменить**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.  На странице **Абонентская группа единой системы обмена сообщениями** в разделе **Автосекретари единой системы обмена сообщениями** выберите автосекретаря единой системы обмена сообщениями, который необходимо изменить, а затем нажмите кнопку **Изменить**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

4.  На странице **Общие** в разделе **Язык для автоматического голосового интерфейса** выберите необходимый язык в раскрывающемся списке.

5.  Нажмите кнопку **Сохранить**, чтобы сохранить изменения.

## Использование командной консоли для настройки параметра языка по умолчанию

В этом примере в качестве языка по умолчанию для автосекретаря единой службы обмена сообщениями используется английский язык `MyUMAutoAttendant` (Великобритания).

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language en-GB

В этом примере в качестве языка по умолчанию для автосекретаря `MyUMAutoAttendant` единой службы обмена сообщениями устанавливается немецкий язык.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language de-DE

