---
title: Разрешение применения репликации для базы данных (среда SQL Server Management Studio) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f31471aceef4937ee34d6492605e3a98dbcd973b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2018
ms.locfileid: "52776416"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>разрешить для базы данных применение репликации (среда SQL Server Management Studio)
  Применение репликации для базы данных неявно разрешается, когда член предопределенной роли сервера **sysadmin** создает публикацию с помощью мастера создания публикаций. Член предопределенной роли сервера **sysadmin** может также явно разрешить применение репликации для базы данных, чтобы член предопределенной роли базы данных **db_owner** мог создать в этой базе данных одну или несколько публикаций. Чтобы в явном виде включить репликацию базы данных, используйте страницу **Базы данных публикации** диалогового окна **Свойства издателя — \<издатель>**. Дополнительные сведения о доступе к этому диалоговому окну см. в разделе [Create a Publication](publish/create-a-publication.md).  
  
### <a name="to-enable-a-database-for-replication"></a>Разрешение применения репликации для базы данных  
  
1.  На странице **Базы данных публикации** диалогового окна **Свойства издателя — \<издатель>** установите флажки **Транзакционная** и (или) **Слиянием** для каждой базы данных, которую требуется реплицировать. Установите флажок **Транзакционная** , чтобы разрешить для базы данных репликацию моментальных снимков.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
