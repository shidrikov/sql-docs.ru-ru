---
title: Parse (тип данных geography) | Документы Майкрософт
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Parse method
- Parse (geography Data Type)
ms.assetid: 21c402fa-fd0f-4d09-a097-49cee0316d4e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0b2e42f61e3926845930b1bd0d3429f2f83c9685
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710902"
---
# <a name="parse-geography-data-type"></a>Parse (тип данных geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Возвращает экземпляр **geography** из WKT-представления консорциума OGC. Функция Parse() эквивалентна функции [STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md), за исключением того, что ожидает в качестве параметра идентификатор пространственной ссылки (SRID) значение 4326. Входные данные могут дополнительно содержать значения Z (высота) и M (мера).
  
Этот метод типа данных **geography** поддерживает экземпляры **FullGlobe** или пространственные экземпляры, размер которых больше полушария.
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
## <a name="arguments"></a>Аргументы  
 *geography_tagged_text*  
 WKT-представление возвращаемого экземпляра **geography**. *geography_tagged_text* является выражением типа **nvarchar**.  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 Тип возвращаемых данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Тип возвращаемых данных CLR: **SqlGeography**  
  
## <a name="remarks"></a>Примечания  
 Тип OGC экземпляра **geography**, возвращаемый методом `Parse()`, получает значение в зависимости от соответствующих входных данных WKT.  
  
 Строка "Null" будет интерпретирована как экземпляр **geography** со значением NULL.  
  
 Этот метод вызывает исключение **ArgumentException**, если входные данные содержат противоположную границу.  
  
## <a name="examples"></a>Примеры  
 В следующем примере метод `Parse()` применяется для создания экземпляра `geography`.  
  
```  
DECLARE @g geography;   
SET @g = geography::Parse('LINESTRING(-122.360 47.656, -122.343 47.656)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>См. также  
 [Расширенные статические географические методы](../../t-sql/spatial-geography/extended-static-geography-methods.md)   
 [STGeomFromText (тип данных geography)](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  
