---
title: '- (вычитание) (выражение служб SSIS) | Документы Майкрософт'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
ms.assetid: b48da086-37dd-460a-8a4b-912f52c9b158
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e544a284cca78a48835af719fe881a995ee87580
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506123"
---
# <a name="--subtract-ssis-expression"></a>- (вычитание) (выражение служб SSIS)
  Вычитает второе числовое выражение из первого.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
numeric_expression1 - numeric_expression2  
  
```  
  
## <a name="arguments"></a>Аргументы  
 *numeric_expression1, numeric_expression2*  
 Любое допустимое выражение числовых типов данных. Дополнительные сведения см. в разделе [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Типы результата  
 Определяется типом данных двух аргументов. Дополнительные сведения см. в разделе [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Remarks  
 Заключите унарное отрицательное выражение в скобки для того, чтобы выражение было вычислено в правильном порядке.  
  
## <a name="remarks"></a>Remarks  
 Если один из операндов равен NULL, то результатом является значение NULL.  
  
## <a name="expression-examples"></a>Примеры выражений  
 Этот пример вычитает числовые литералы.  
  
```  
5 - 6.09  
```  
  
 Этот пример вычитает значение столбца **StandardCost** из значения столбца **ListPrice** .  
  
```  
ListPrice - StandardCost  
```  
  
 Этот пример вычитает вычисленное значение из значения столбца **ListPrice** . Переменная **Discount%** должна быть заключена в квадратные скобки, поскольку имя включает символ %. Дополнительные сведения см. в разделе [Идентификаторы (службы SSIS)](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>См. также:  
 [Очередность и ассоциативность операторов](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Операторы (выражение служб SSIS)](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
