---
title: Увеличение или отключение порога заблокированных процессов | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 71db8ef6-341b-4465-99db-5c63e48d4c7d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: f06eee678ed7088c20edde7d9f5d44ca0ba7cf02
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512115"
---
# <a name="increase-or-disable-blocked-process-threshold"></a>Увеличение или отключение порога заблокированных процессов
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Это правило проверяет, имеет ли параметр «blocked process threshold» значение 0 (отключен) или значение, большее или равное 5 (секундам). Присвоение параметру «blocked process threshold» значения от 1 до 4 может привести к постоянной работе монитора взаимоблокировок. Эти значения следует использовать только для устранения неполадок. Их нельзя устанавливать на долгое время или в рабочей среде без участия представителей службы поддержки пользователей [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Рекомендации  
 Чтобы решить эту проблему, присвойте параметру «blocked process threshold» значение 5 (секунд) или больше либо отключите порог блокировки процессов, присвоив этому параметру значение 0. Чтобы присвоить параметру «blocked process threshold» значение `5` секунд, выполните следующую инструкцию:  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 5 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="for-more-information"></a>Дополнительные сведения см. в разделе  
 [Параметр конфигурации сервера «blocked process threshold»](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md)  
  
## <a name="see-also"></a>См. также:  
 [Наблюдение с помощью управления на основе политик и принудительное применение рекомендаций с помощью управления на основе политик](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
