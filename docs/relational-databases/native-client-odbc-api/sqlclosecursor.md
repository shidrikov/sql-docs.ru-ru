---
title: SQLCloseCursor | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a9d8ddeb530c4b42f44e58aeea364956fa40bf6a
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2018
ms.locfileid: "51668986"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLCloseCursor** заменяет [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) с *параметр* значение SQL_CLOSE. По получении функции **SQLCloseCursor**драйвер собственного клиента ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] отбрасывает строки ожидающих результирующих наборов. Обратите внимание, что содержащиеся в инструкции привязки параметров и столбцов (если они существуют) **SQLCloseCursor**оставляет без изменений.  
  
## <a name="see-also"></a>См. также  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [Подробные сведения о реализации API-интерфейсов ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
