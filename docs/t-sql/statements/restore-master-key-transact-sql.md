---
title: RESTORE MASTER KEY (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RESTORE_MASTER_KEY_TSQL
- RESTORE MASTER KEY
- LOAD_MASTER_KEY_TSQL
- LOAD MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- database master key [SQL Server], importing
- encryption [SQL Server], Database Master Key
- copying Database Master Keys
- importing Database Master Keys
- cryptography [SQL Server], Database Master Key
- transferring Database Master Keys
- RESTORE MASTER KEY statement
ms.assetid: 70ceb951-31a2-4fc4-a0c1-e6c18eeb3ae7
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ef8810837eeb9f5d63b9c01579f7c291fde924f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620632"
---
# <a name="restore-master-key-transact-sql"></a>RESTORE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Импортирует главный ключ базы данных из файла резервной копии.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
RESTORE MASTER KEY FROM FILE = 'path_to_file'   
    DECRYPTION BY PASSWORD = 'password'  
    ENCRYPTION BY PASSWORD = 'password'  
    [ FORCE ]  
```  
  
## <a name="arguments"></a>Аргументы  
 FILE ='*path_to_file*'  
 Указывает полный путь с именем файла к главному ключу хранимой процедуры. *path_to_file* может быть локальным путем или UNC-путем к расположению в сети.  
  
 DECRYPTION BY PASSWORD ='*password*'  
 Указывает пароль для дешифрования главного ключа базы данных, импортируемого из файла.  
  
 ENCRYPTION BY PASSWORD ='*password*'  
 Указывает пароль для шифрования главного ключа базы данных после его загрузки в базу данных.  
  
 FORCE  
 Указывает на то, что процесс RESTORE должен продолжаться, даже если текущий главный ключ базы данных не открыт или если [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не может дешифровать некоторые зашифрованные им закрытые ключи.  
  
## <a name="remarks"></a>Примечания  
 Когда главный ключ восстановлен, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] дешифрует все ключи, зашифрованные текущим активным главным ключом, и затем шифрует эти ключи с помощью восстановленного главного ключа. Данную ресурсоемкую операцию следует планировать на то время, когда количество обращений к серверу минимальное. Если текущий главный ключ базы данных не открыт или не может быть открыт, или если какой-либо зашифрованный им ключ не может быть дешифрован, операция восстановления заканчивается неудачно.  
  
 Аргумент FORCE следует использовать только в случае, если главный ключ получить невозможно или при неудачной попытке расшифровки. Данные, зашифрованные только недоступным ключом, будут потеряны.  
  
 Если главный ключ был зашифрован главным сервисным ключом, восстановленный главный ключ также будет зашифрован главным сервисным ключом.  
  
 Если в текущей базе данных нет главного ключа, RESTORE MASTER KEY создает главный ключ. Новый главный ключ не будет автоматически шифроваться главным сервисным ключом.  
  
## <a name="permissions"></a>Разрешения  
 Требует разрешения CONTROL для базы данных.  
  
## <a name="examples"></a>Примеры  
 В следующем примере восстанавливается главный ключ базы данных для базы данных `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
RESTORE MASTER KEY   
    FROM FILE = 'c:\backups\keys\AdventureWorks2012_master_key'   
    DECRYPTION BY PASSWORD = '3dH85Hhk003#GHkf02597gheij04'   
    ENCRYPTION BY PASSWORD = '259087M#MyjkFkjhywiyedfgGDFD';  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [CREATE MASTER KEY (Transact-SQL)](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY (Transact-SQL)](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [Иерархия средств шифрования](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
