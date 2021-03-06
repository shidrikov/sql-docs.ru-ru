---
title: Вкладки перекрестной проверки (представление диаграммы точности интеллектуального анализа данных) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.crossvalidation.f1
ms.assetid: bd215a68-1ad7-4046-9c44-ec8e2be13a64
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d49e80d01a83f2ffad43178fa987010cd4f76b01
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48188214"
---
# <a name="cross-validation-tab-mining-accuracy-chart-view"></a>Вкладка «Перекрестная проверка» (просмотр диаграммы точности интеллектуального анализа данных)
  Перекрестная проверка позволяет секционировать структуру интеллектуального анализа данных на разрезы, после чего — выполнить итеративное обучение и проверку моделей по каждому разрезу. Необходимо указать количество сверток, на которые разделяются данные, и каждая свертка, в свою очередь, играет роль проверочных данных, тогда как остальные данные используются для обучения новой модели. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Создает набор стандартных показателей точности для каждой модели. Сравнивая показатели моделей, созданных для каждого разреза, можно получить хорошее представление о том, насколько верна модель интеллектуального анализа для всего набора данных.  
  
 Дополнительные сведения см. в разделе [Cross-Validation &#40;Analysis Services - Data Mining&#41;](data-mining/cross-validation-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Перекрестная проверка не может использоваться с моделями, построенными с помощью алгоритма временных рядов [!INCLUDE[msCoName](../includes/msconame-md.md)] или алгоритма кластеризации последовательностей [!INCLUDE[msCoName](../includes/msconame-md.md)] . При составлении отчета по структуре интеллектуального анализа данных, в которой содержатся модели таких типов, эти модели не будут включены в отчет.  
  
## <a name="task-list"></a>Список задач  
  
-   Укажите число сверток.  
  
-   Укажите максимальное число вариантов, используемых в перекрестной проверке.  
  
-   Укажите прогнозируемый столбец.  
  
-   (Необязательно) Укажите прогнозируемое состояние.  
  
-   (Необязательно) Задайте параметры, управляющие оценкой точности прогноза.  
  
-   Нажмите кнопку **Получить результаты** , чтобы отобразить результаты перекрестной проверки.  
  
## <a name="uielement-list"></a>Список элементов пользовательского интерфейса  
 **Количество сверток**  
 Укажите количество создаваемых сверток или секций. Минимальное значение равно 2, то есть одна половина набора данных используется для проверки, другая — для обучения.  
  
 Максимальное значение составляет 10 для структур интеллектуального анализа данных сеансов.  
  
 Если структура интеллектуального анализа данных хранится в экземпляре служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], максимальное значение составляет 256.  
  
> [!NOTE]  
>  По мере увеличения количества сверток соответствующим образом увеличивается время, необходимое для выполнения перекрестной проверки. Большое количество вариантов и большее значение параметра **Количество сверток** может привести к снижению производительности.  
  
 **Максимальное число вариантов**  
 Укажите максимальное число вариантов, используемых в перекрестной проверке. Количество вариантов в любой отдельной свертке можно вычислить как отношение значения **Максимальное количество вариантов** к значению **Количество сверток** .  
  
 При значении **0**для перекрестной проверки используются все варианты исходных данных.  
  
 Значение по умолчанию отсутствует.  
  
> [!NOTE]  
>  По мере увеличения количества вариантов увеличивается и время обработки.  
  
 **Целевой атрибут**  
 Выберите столбец из списка прогнозируемых столбцов, обнаруженных во всех моделях. Каждый раз при выполнении перекрестной проверки можно выбрать только один прогнозируемый столбец.  
  
 Чтобы проверить только модели кластеризации, выберите **Кластер**.  
  
 **Целевое состояние**  
 Введите значение или выберите целевое значение из раскрывающегося списка значений.  
  
 Значением по умолчанию является `null`, обозначающее проверку всех состояний.  
  
 Отключено для моделей кластеризации.  
  
 **Целевой**  **порог**  
 Укажите значение в диапазоне от 0 до 1, обозначающее вероятность прогноза, прогнозируемое состояние выше которой считается верным. Задать это значение можно с шагом 0,1.  
  
 Значением по умолчанию является `null`, обозначающее, что верным считается прогноз с наивысшей вероятностью.  
  
> [!NOTE]  
>  Значение 0,0 присвоить этому параметру можно, но это приведет к увеличению времени обработки и не даст значительных результатов.  
  
 **Получение результатов**  
 Нажмите, чтобы запустить перекрестную проверку модели с указанными параметрами.  
  
 Модель секционируется на указанное количество сверток, и для каждой свертки выполняется проверка отдельной модели. Поэтому, чтобы получить результаты перекрестной проверки, необходимо некоторое время.  
  
 Дополнительные сведения об интерпретации результатов отчета перекрестной проверки см. в разделе [Меры в отчете перекрестной проверки](data-mining/measures-in-the-cross-validation-report.md).  
  
## <a name="setting-the-accuracy-threshold"></a>Задание порога точности  
 Управлять стандартом измерения точности прогнозов можно с помощью значения **Целевой** **порог**. Порог представляет собой разновидность диаграммы точности. Каждому прогнозу присваивается вероятность достоверности прогнозируемого значения. Таким образом, если значение **Целевой** **порог** близко к 1, вероятность в любых конкретных прогнозах должна быть довольно высокой, чтобы прогноз считался хорошим. И наоборот, если значение параметра **Целевой** **порог** близко к 0, то хорошими будут считаться даже прогнозы с невысокими значениями вероятности.  
  
 Рекомендованных значений порога нет, поскольку вероятность в любом прогнозе зависит от объема данных и типа составляемого прогноза. Чтобы построить диаграмму точности для своих данных, изучите несколько прогнозов с разными уровнями вероятности. Данный этап важен, поскольку значение, заданное для параметра **Целевой** **порог** , влияет на измеряемую точность модели.  
  
 Например, имеется три прогноза, составленных для определенного целевого состояния, с вероятностями 0,05, 0,15 и 0,8. Если порогу задано значение 0,5, правильным будет считаться только один прогноз. Если параметру **Целевой** **порог** присвоено значение 0,10, то верными будут считаться два прогноза.  
  
 Когда **целевой** **пороговое значение** присваивается `null`, который является значением по умолчанию, то самый вероятный прогноз для каждого случая будет считаться правильным. В только что приведенном примере вероятности 0,05, 0,15 и 0,8 являются прогнозами в трех различных вариантах. Несмотря на большую разницу в вероятностях, каждый из прогнозов будет считаться верным, поскольку в каждом варианте формируется только один прогноз, и указанные прогнозы являются лучшими в данных вариантах.  
  
## <a name="see-also"></a>См. также  
 [Тестирование и проверка &#40;интеллектуального анализа данных&#41;](data-mining/testing-and-validation-data-mining.md)   
 [Перекрестная проверка &#40;службы Analysis Services — Интеллектуальный анализ данных&#41;](data-mining/cross-validation-analysis-services-data-mining.md)   
 [Меры в отчете перекрестной проверки](data-mining/measures-in-the-cross-validation-report.md)   
 [Хранимые процедуры интеллектуального анализа данных &#40;службы Analysis Services — Интеллектуальный анализ данных&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
  
