---
title: Администрирование группы доступности (SQL Server) | Документы Майкрософт
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], managing
ms.assetid: 0b7542fa-235e-413d-81bf-3eff9ee07480
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4896c9219632d816565fdd30c11aa82ccbf7fef1
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/13/2018
ms.locfileid: "53355361"
---
# <a name="administration-of-an-availability-group-sql-server"></a>Администрирование группы доступности (SQL Server)
  Управление существующей группой доступности AlwaysOn в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] включает в себя одну или несколько следующих задач.  
  
-   Изменение свойств существующей реплики доступности, например для изменения клиентского доступа к соединению (для настройки вторичных реплик, доступных для чтения), изменение режима отработки отказа, режима доступности или задание времени ожидания сеанса.  
  
-   Добавление или удаление вторичных реплик.  
  
-   Добавление или удаление базы данных.  
  
-   Приостановка или возобновление работы базы данных.  
  
-   Выполнение запланированной отработки отказа вручную ( *отработка отказа вручную*) или принудительной отработки отказа вручную ( *принудительная отработка отказа*).  
  
-   Создание или настройка прослушивателя группы доступности.  
  
-   Управление [доступными для чтения вторичными репликами](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) для данной группы доступности. Необходимо настроить доступ для чтения для одной или нескольких реплик, выполняемых под вторичной ролью, и настроить маршрутизацию только для чтения.  
  
-   Управление [резервными копиями вторичных реплик](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md) определенной группы доступности. Необходимо настроить место выполнения задач по созданию резервных копий и написать скрипты для этих задач. необходимо создать скрипты заданий резервного копирования для каждой базы данных в группе доступности на каждом экземпляре [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , на котором размещается реплика доступности.  
  
-   Удаление группы доступности.  
  
-   Миграция между кластерами групп доступности AlwaysOn для обновления ОС  
  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
 **Настройка существующей группы доступности**  
  
-   [Добавление вторичной реплики к группе доступности (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Удаление вторичной реплики из группы доступности (SQL Server)](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Добавление базы данных в группу доступности (SQL Server)](availability-group-add-a-database.md)  
  
-   [Удаление базы данных-получателя из группы доступности (SQL Server)](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Удаление базы данных-источника из группы доступности (SQL Server)](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [Настройка гибкой политики отработки отказа для обеспечения контроля над для автоматической отработки отказа &#40;группы доступности AlwaysOn&#41;](configure-flexible-automatic-failover-policy.md)  
  
 **Управление группой доступности**  
  
-   [Настройка резервного копирования в репликах доступности (SQL Server)](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Выполнение запланированного перехода на другой ресурс вручную для группы доступности (SQL Server)](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Выполнение принудительного перехода на другой ресурс вручную для группы доступности (SQL Server)](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Удаление группы доступности (SQL Server)](remove-an-availability-group-sql-server.md)  
  
 **Управление репликой доступности**  
  
-   [Добавление вторичной реплики к группе доступности (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Присоединение вторичной реплики к группе доступности (SQL Server)](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Удаление вторичной реплики из группы доступности (SQL Server)](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Смена режима доступности для реплики доступности (SQL Server)](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Смена режима отработки отказа для реплики доступности (SQL Server)](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Настройка резервного копирования в репликах доступности (SQL Server)](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Настройка доступа только для чтения в реплике доступности (SQL Server)](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Настройка маршрутизации только для чтения в группе доступности (SQL Server)](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Изменение периода ожидания сеанса для реплики доступности (SQL Server)](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **Управление базой данных доступности**  
  
-   [Добавление базы данных в группу доступности (SQL Server)](availability-group-add-a-database.md)  
  
-   [Присоединение базы данных-получателя к группе доступности (SQL Server)](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Удаление базы данных-источника из группы доступности (SQL Server)](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [Удаление базы данных-получателя из группы доступности (SQL Server)](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Приостановка базы данных доступности (SQL Server)](suspend-an-availability-database-sql-server.md)  
  
-   [Возобновление базы данных доступности (SQL Server)](resume-an-availability-database-sql-server.md)  
  
 **Наблюдение за группой доступности**  
  
-   [Отслеживание групп доступности (SQL Server)](monitoring-of-availability-groups-sql-server.md)  
  
 **Поддержка миграции групп доступности на новый кластер WSFC (миграция с одного кластера на другой)**  
  
-   [Смена контекста кластера HADR для экземпляра сервера (SQL Server)](change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
-   [Перевод группы доступности в режим "вне сети" (SQL Server)](../../take-an-availability-group-offline-sql-server.md)  
  
  
##  <a name="RelatedContent"></a> См. также  
  
-   **Блоги**  
  
     [Блоги группы AlwaysOn SQL Server: Официальный блог по SQL Server AlwaysOn Team](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Блоги инженеров CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Видеоролики**  
  
     [Серия Microsoft SQL Server с кодовым названием «Denali» AlwaysOn, часть 1: Представляем решение высокого уровня доступности следующего поколения](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Серия Microsoft SQL Server с кодовым названием «Denali» AlwaysOn, часть 2: Создание решения критически важных высокого уровня доступности с помощью AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Технические документы**  
  
     [Технические документы Майкрософт Microsoft по SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Технические документы группы консультантов по SQL Server](http://sqlcat.com/)  
  
  
## <a name="see-also"></a>См. также  
 [Группы доступности AlwaysOn &#40;SQL Server&#41;](always-on-availability-groups-sql-server.md)   
 [Обзор групп доступности AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Настройка экземпляра сервера для групп доступности AlwaysOn &#40;SQL Server&#41;](configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)  
 [Создание и настройка групп доступности (SQL Server)](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Активные вторичные реплики. Вторичные реплики для чтения &#40;группы доступности AlwaysOn&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Активные вторичные реплики. Резервного копирования во вторичных репликах &#40;группы доступности AlwaysOn&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
 [Прослушиватели групп доступности, возможность подключения клиентов и отработка отказа приложений (SQL Server)](../../listeners-client-connectivity-application-failover.md)   
 [Политики AlwaysOn на случай проблем в работе с группами доступности AlwaysOn &#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)   
 [Отслеживание групп доступности (SQL Server)](monitoring-of-availability-groups-sql-server.md)   
 [Группы доступности AlwaysOn: Взаимодействие &#40;SQL Server&#41;](always-on-availability-groups-interoperability-sql-server.md)   
 [Общие сведения об инструкциях Transact-SQL для групп доступности AlwaysOn &#40;SQL Server&#41;](transact-sql-statements-for-always-on-availability-groups.md)   
 [Обзор командлетов PowerShell для групп доступности AlwaysOn &#40;SQL Server&#41;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  
