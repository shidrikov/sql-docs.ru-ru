---
title: Удаление несуществующих файловых групп (SQL Server) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], defunct filegroups
- defunct filegroups
- restoring filegroups [SQL Server]
- deferred transactions
- filegroups [SQL Server], defunct
- unrestored filegroups
ms.assetid: 055f9c6a-5c18-4942-98e7-ec918f0ff975
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 58ee1265918a96133ac0b25b9dd2ac516607b0fd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187044"
---
# <a name="remove-defunct-filegroups-sql-server"></a>Удаление уничтоженных файловых групп (SQL Server)
  В этом разделе описывается удаление уничтоженных файловых групп в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **В этом разделе**  
  
-   **Перед началом работы**  
  
     [Ограничения](#Restrictions)  
  
-   [Рекомендации](#Recommendations)  
  
     [безопасность](#Security)  
  
-   **Удаление уничтоженных файловых групп с использованием следующих средств:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Сведения в этом разделе относятся к базам данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , содержащим несколько файлов или файловых групп (а для простой модели восстановления — к файловым группам, доступным только для чтения).  
  
-   При удалении файловой группы вне сети все файлы группы помечаются удаленными.  
  
###  <a name="Recommendations"></a> Рекомендации  
  
-   Если восстановление невосстановленной файловой группы не предполагается, необходимо сделать ее *уничтоженной* , удалив из базы данных. Такая файловая группа не может быть восстановлена в данной базе данных, однако при этом сохраняются ее метаданные. После того как файловая группа стала уничтоженной, базу данных можно перезапустить, и в процессе восстановления будет восстановлена согласованность базы данных между восстановленными файловыми группами.  
  
     Например, объявление файловой группы как нефункционирующей позволяет разрешить отложенные транзакции, возникшие из-за файловой группы вне сети, которая больше не нужна в базе данных. Транзакции, отложенные из-за того, что файловая группа находилась в режиме «вне сети», выходят из отложенного состояния после того, как эта файловая группа перестанет функционировать. Дополнительные сведения см. в разделе [Отложенные транзакции (SQL Server)](deferred-transactions-sql-server.md).  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Необходимо разрешение ALTER на базу данных.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="to-remove-defunct-filegroups"></a>Удаление уничтоженных файловых групп  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] и разверните его.  
  
2.  Раскройте список **Базы данных**, щелкните правой кнопкой мыши базу данных, из которой удаляется файл, а затем выберите пункт **Свойства**.  
  
3.  Выберите страницу **Файлы** .  
  
4.  В списке **Файлы базы данных** выберите файлы для удаления, нажмите кнопку **Удалить**, а затем кнопку **ОК**.  
  
5.  Выберите страницу **Файловые группы** .  
  
6.  В списке **Строки** выберите файловую группу для удаления, нажмите кнопку **Удалить**, а затем кнопку **ОК**.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-remove-defunct-filegroups"></a>Удаление уничтоженных файловых групп  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. (**Примечание**. В этом примере предполагается, что файлы и файловая группа уже существуют. Для создания этих объектов см. пример Б в разделе [Параметры инструкции ALTER DATABASE для файлов и файловых групп](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options).) В первом примере удаляются файлы `test1dat3` и `test1dat4` из уничтоженной файловой группы с помощью инструкции `ALTER DATABASE` с предложением `REMOVE FILE`. Во втором примере удаляется уничтоженная файловая группа `Test1FG1`с помощью предложения `REMOVE FILEGROUP`.  
  
```tsql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat3 ;  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4 ;  
GO  
  
```  
  
```tsql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILEGROUP Test1FG1 ;  
GO  
  
```  
  
## <a name="see-also"></a>См. также  
 [Параметры инструкции ALTER DATABASE для файлов и файловых групп (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)   
 [Отложенные транзакции (SQL Server)](deferred-transactions-sql-server.md)   
 [Файлы из резервных копий (модель полного восстановления)](file-restores-full-recovery-model.md)   
 [Восстановление файлов (простая модель восстановления)](file-restores-simple-recovery-model.md)   
 [Восстановление в сети (SQL Server)](online-restore-sql-server.md)   
 [Восстановление страниц (SQL Server)](restore-pages-sql-server.md)   
 [Поэтапное восстановление (SQL Server)](piecemeal-restores-sql-server.md)  
  
  
