﻿---
title: 'Настройка свойств сети для группы обеспечения доступности баз данных: Exchange 2013 Help'
TOCTitle: Настройка свойств сети для группы обеспечения доступности баз данных
ms:assetid: 41197639-988f-476c-9788-51d5191a7dce
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd297927(v=EXCHG.150)
ms:contentKeyID: 50487952
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Настройка свойств сети для группы обеспечения доступности баз данных

 

_**Применимо к:**Exchange Server 2013_

_**Последнее изменение раздела:**2012-10-31_

Каждая сеть группы обеспечения доступности баз данных (DAG) обладает рядом настраиваемых свойств, включая имя, поле описания, список подсетей, которые используются этой сетью DAG, и значение, указывающее, включена ли для нее репликация.

Необходимы сведения о других задачах управления, связанных с группами доступности базы данных? см. в разделе [Управление группами доступности базы данных](managing-database-availability-groups-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: 1 минута.

  - Запись "Группы обеспечения доступности баз данных" Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье в разделе [Разрешения высокого уровня доступности и устойчивости сайта](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Вы можете настроить сеть DAG, только если для этой группы отключена автоматическая настройка сети. Подробные инструкции по отключению автоматической настройки сети для группы DAG см. в статье [Настройка свойств группы обеспечения доступности баз данных](configure-database-availability-group-properties-exchange-2013-help.md).

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

## Использование центра администрирования Exchange для настройки свойств сети группы обеспечения доступности баз данных

1.  В Центре администрирования Exchange последовательно выберите пункты **Серверы** \> **Группы обеспечения доступности баз данных**.

2.  Выберите группу обеспечения доступности баз данных, которую нужно настроить, а затем в области сведений выберите для сети следующие параметры.
    
      - **Отключить репликацию** или **Включить репликацию**. Настраивает параметры репликации для сети DAG.
    
      - **Удалить**. Удаляет сеть DAG. Прежде чем удалять сеть DAG, необходимо сначала удалить из нее все связанные подсети.
    
      - **Просмотреть сведения**. Настраивает параметры сети DAG, например имя, описание и связанные подсети. Кроме того, вы можете просмотреть сетевые интерфейсы, связанные с этими подсетями, а также включить или отключить репликацию для сети DAG.

## Использование командной консоли для настройки свойств сети группы доступности базы данных

В этом примере в сеть MapiDagNetwork группы обеспечения доступности баз данных DAG1 добавляются подсеть 10.0.0.0 и маска подсети 255.0.0.0.

    Set-DatabaseAvailabilityGroupNetwork -Subnets 10.0.0.0/8 -Identity DAG1\MapiDagNetwork

## Как проверить, что все получилось?

Чтобы проверить, успешно ли настроена сеть DAG, выполните указанные ниже действия.

  - Выполните в командной консоли приведенную ниже команду, чтобы просмотреть параметры настройки для сети DAG и убедиться, что сеть была настроена успешно.
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## Дополнительные сведения

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ru-ru/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ru-ru/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ru-ru/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ru-ru/library/dd298131\(v=exchg.150\))

