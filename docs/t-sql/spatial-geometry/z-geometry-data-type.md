---
title: Z (тип данных geometry) | Документы Майкрософт
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Z (geometry Data Type)
- Z_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Z (geometry Data Type)
ms.assetid: a62ed736-44df-4591-9109-ce90e1df9bd3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f48bfcf74a53cec829dba8171c9c66abc3c0254b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47607686"
---
# <a name="z-geometry-data-type"></a>Z (тип данных geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Значение Z (высота) экземпляра. Семантика значения высоты определяется пользователем.
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
.Z  
```  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 Тип [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Тип CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 Значение этого свойства будет NULL, если экземпляр geometry не является точкой, а также для любого экземпляра **Point**, для которого оно не задано.  
  
 Это свойство доступно только для чтения.  
  
 Координаты по оси Z не используются ни в каких вычислениях, выполненных библиотекой, и не проходят ни через какие библиотечные изменения.  
  
## <a name="examples"></a>Примеры  
 В следующем примере создается экземпляр `Point` со значениями Z (высота) и M (мера) и методом `Z` производится получение для него значения Z.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>См. также:  
 [M (тип данных geometry)](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [AsTextZM (тип данных geometry)](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)   
 [Расширенные методы экземпляров Geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

