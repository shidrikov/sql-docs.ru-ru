---
title: Добавление в диаграмму разрывов шкалы (построитель отчетов и службы SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 84d66436-ed62-4967-bbbd-b457593ee787
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 85c1849cb2fb5fdfda78a147880d9c39003b8257
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358816"
---
# <a name="add-scale-breaks-to-a-chart-report-builder-and-ssrs"></a>Добавление в диаграмму разрывов шкалы (построитель отчетов и службы SSRS)
  Разрыв шкалы представляет собой полосу, нарисованную в области построения диаграммы, обозначающую нарушение непрерывной последовательности изменения значений от малых к большим на оси значений (обычно это вертикальная ось, или ось Y). Разрыв шкалы используется, чтобы отобразить два разных диапазона в одной и той же области диаграммы.  
  
 ![Диаграмма с разрывом шкалы](../media/rs-multipledatarangeschart-scalebreak.gif "Диаграмма с разрывом шкалы")  
  
> [!NOTE]  
>  Положение разрыва шкалы указать на диаграмме нельзя. Диаграмма на основе значений набора данных самостоятельно вычисляет, где имеется значительный разрыв между диапазонами данных, чтобы поместить разрыв шкалы на оси значений (оси Y) во время выполнения.  
  
 Пример диаграммы с разрывами шкалы доступен в виде образца отчета. Дополнительные сведения о скачивании этого и других примеров отчетов см. в статье [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][Report Builder and Report Designer sample reports](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-enable-scale-breaks-on-the-chart"></a>Включение разрывов шкалы на диаграмме  
  
1.  Щелкните правой кнопкой мыши вертикальную ось и выберите пункт **Свойства оси**. Откроется диалоговое окно **Свойства вертикальной оси** .  
  
2.  Установите флажок **Включить разрывы шкалы** .  
  
### <a name="to-change-the-style-of-the-scale-break"></a>Изменение стиля разрыва шкалы  
  
1.  Откройте панель «Свойства».  
  
2.  В области конструктора щелкните правой кнопкой мыши ось Y диаграммы. На панели «Свойства» будут отображены свойства объекта оси Y (по умолчанию называемой «Ось диаграммы»).  
  
3.  В разделе **Шкала** раскройте свойство ScaleBreakStyle.  
  
4.  Измените значения свойства ScaleBreakStyle, такие как BreakLineType и Spacing. Дополнительные сведения о свойствах разрыва шкалы см. в разделе [Отображение на диаграмме ряда с несколькими диапазонами данных (построитель отчетов и службы SSRS)](displaying-a-series-with-multiple-data-ranges-on-a-chart.md).  
  
## <a name="see-also"></a>См. также  
 [Диаграммы (построитель отчетов и службы SSRS)](charts-report-builder-and-ssrs.md)   
 [Форматирование диаграммы (построитель отчетов и службы SSRS)](formatting-a-chart-report-builder-and-ssrs.md)   
 [Диалоговое окно "Свойства оси" — "Параметры оси" (построитель отчетов и службы SSRS)](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)  
  
  
