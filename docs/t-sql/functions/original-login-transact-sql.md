---
title: ORIGINAL_LOGIN (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ORIGINAL_LOGIN_TSQL
- ORIGINAL_LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], context switches
- context switching [SQL Server], login names
- original login names [SQL Server]
- ORIGINAL_LOGIN function
- names [SQL Server], logins
ms.assetid: ddfb0991-cde3-4b97-a5b7-ee450133f160
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 640a4b22ca8bec9f12778cae94d31de77c9cbe7f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789142"
---
# <a name="originallogin-transact-sql"></a>ORIGINAL_LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Возвращает имя входа, которое используется для подключения к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Можно использовать эту функцию для возврата идентификатора исходного имени входа в сеансах, содержащих множество явных и неявных переключений контекста.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
ORIGINAL_LOGIN( )  
```  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 **sysname**  
  
## <a name="remarks"></a>Remarks  
 Эта функция может быть полезной для аудита идентификатора исходного контекста подключения. Так как остальные функции, такие как [SESSION_USER](../../t-sql/functions/session-user-transact-sql.md) и [CURRENT_USER](../../t-sql/functions/current-user-transact-sql.md), возвращают текущий исполняющий контекст, ORIGINAL_LOGIN возвращает идентификатор имени входа, которое первым подключилось к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в данном сеансе.  
  
 Возвращает значение NULL для [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
## <a name="examples"></a>Примеры  
 Следующий пример переключает исполняющий контекст текущего сеанса от того, кто вызвал данные инструкции, на `login1`. Функции `SUSER_SNAME` и `ORIGINAL_LOGIN` используются для возврата пользователя текущего сеанса (пользователя, на которого переключается контекст) и исходной учетной записи имени входа.  
  
```  
USE AdventureWorks2012;  
GO  
--Create a temporary login and user.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE USER user1 FOR LOGIN login1;  
GO  
--Execute a context switch to the temporary login account.  
DECLARE @original_login sysname;  
DECLARE @current_context sysname;  
EXECUTE AS LOGIN = 'login1';  
SET @original_login = ORIGINAL_LOGIN();  
SET @current_context = SUSER_SNAME();  
SELECT 'The current executing context is: '+ @current_context;  
SELECT 'The original login in this session was: '+ @original_login  
GO  
-- Return to the original execution context  
-- and remove the temporary principal.  
REVERT;  
GO  
DROP LOGIN login1;  
DROP USER user1;  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [EXECUTE AS (Transact-SQL)](../../t-sql/statements/execute-as-transact-sql.md)   
 [REVERT (Transact-SQL)](../../t-sql/statements/revert-transact-sql.md)  
  
  
