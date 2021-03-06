---
title: Запрос интеллектуального анализа данных | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquery.f1
ms.assetid: 948e358a-6245-429f-82c7-4cedc5e048fd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c0d4295ba75c18ea6b3331317bb38a6fadf26256
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811672"
---
# <a name="data-mining-query"></a>Запрос интеллектуального анализа данных
  Панель конструктора содержит построитель прогнозирующих запросов интеллектуального анализа данных, который можно использовать для построения прогнозирующих запросов интеллектуального анализа данных. Можно строить либо прогнозирующие запросы на основании входных таблиц, либо одноэлементные прогнозирующие запросы. Переключитесь в просмотр результата, чтобы запустить запрос и просмотреть результаты. Просмотр запроса отображает запрос расширения интеллектуального анализа данных, созданный построителем прогнозирующих запросов.  
  
## <a name="options"></a>Параметры  
 Кнопка переключения представлений  
 Для переключения между панелями конструирования и запросов щелкните значок. По умолчанию открыта панель конструирования.  
  
 Для переключения на панель конструктора щелкните значок ![значок конструктора](../../integration-services/control-flow/media/ssis-designicon.gif "значок конструктора").  
  
 Для переключения на панель запросов щелкните значок ![значок SQL](../../integration-services/control-flow/media/ssis-queryicon.gif "значок SQL").  
  
 **Модель интеллектуального анализа данных**  
 Отображает выбранную модель интеллектуального анализа данных, на основе которой будет производиться прогнозирование.  
  
 **Выбрать модель**  
 Открывает диалоговое окно **Выбор модели интеллектуального анализа данных** .  
  
 **Входные столбцы**  
 Отображает выбранные входные столбцы, используемые при формировании прогноза.  
  
 **Source**  
 Из раскрывающегося списка выберите источник, содержащий поле, которое надо использовать для столбца. Можно использовать либо модель интеллектуального анализа данных, выбранную в таблице **Модель интеллектуального анализа данных** , входные таблицы, выбранные в таблице **Выбор входных таблиц** , либо функцию предсказания, либо пользовательское выражение.  
  
 В ячейку можно перетаскивать столбцы из таблиц, содержащих модели интеллектуального анализа данных, а также входные столбцы.  
  
 **Поле**  
 Выберите столбец из списка столбцов, полученного из исходной таблицы. Если в поле **Источник** была выбрана **Прогнозирующая функция**, данная ячейка будет содержать раскрывающийся список функций прогнозирования, доступных для выбранной модели интеллектуального анализа данных.  
  
 **Псевдоним**  
 Имя столбца, возвращаемое сервером.  
  
 **Показать**  
 Выберите, чтобы возвратить столбец или только использовать столбец в предложении WHERE.  
  
 **Группирование**  
 Используйте со столбцом **И/ИЛИ** для группирования выражений. Например (выражение1 ИЛИ выражение2) И выражение3.  
  
 **И/ИЛИ**  
 Используйте для создания логического запроса. Например (выражение1 ИЛИ выражение2) И выражение3.  
  
 **Критерий или аргумент**  
 Задайте условие или пользовательское выражение, применимое к столбцу. В ячейку можно перетаскивать столбцы из таблиц, содержащих модели интеллектуального анализа данных, а также входные столбцы.  
  
## <a name="see-also"></a>См. также:  
 [Средства запросов интеллектуального анализа данных](../../analysis-services/data-mining/data-mining-query-tools.md)   
 [Справочник по расширениям интеллектуального анализа данных (расширения интеллектуального анализа данных)](../../dmx/data-mining-extensions-dmx-statements.md)  
  
  
