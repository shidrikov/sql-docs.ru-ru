---
title: Руководство по созданию, обучение и оценку моделей на основе секций в R - служб машинного обучения SQL Server
description: Узнайте, как модели, обучения и использования секционированных данных, которая динамически создается при использовании возможности моделирования на основе раздела машинного обучения SQL Server.
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/02/2018
ms.topic: tutorial
ms.author: heidist
author: HeidiSteen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4c60a50f5a0f1c1831a4831d1f93ddf7d81a11d9
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596465"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>Учебник. Создание моделей на основе секций на R в SQL Server
[!INCLUDE[appliesto-ssvnex-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

В 2019 SQL Server моделирования на основе раздела является возможность создания и обучения моделей по секционированных данных. Для стратифицированной данных, которые естественным образом сегменты в классификации схемы - например географических регионах, даты и времени, возраста или пола — вы можете выполнить скрипт по всему набору данных, с возможностью модели, обучение и Оценка секций, которые остаются без изменений за все эти операции. 

Моделирования на основе секции с включенной через два новых параметра [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql):

+ **input_data_1_partition_by_columns**, который указывает столбец для раздела.
+ **input_data_1_order_by_columns** указывает, какие столбцы для предложения order by. 

В этом руководстве сведения моделирования на основе раздела с помощью классической образец данных такси Нью-ЙОРКА и R-скрипт. Столбец секционирования является метод оплаты.

> [!div class="checklist"]
> * Разделы основаны на типах оплаты (5).
> * Создайте и обучения моделей в каждой секции и хранить объекты в базе данных.
> * Прогнозирования вероятности совет результаты по каждой секции модели, используя демонстрационные данные, зарезервированные для этой цели.

## <a name="prerequisites"></a>предварительные требования
 
Для работы с этим учебником необходимо иметь следующее:

+ Недостаточно системных ресурсов. Используется большой набор данных и операций обучения требуется много ресурсов. По возможности используйте системой, имеющей по крайней мере 8 ГБ ОЗУ. В качестве альтернативы можно использовать небольшие наборы данных, чтобы обойти ограничения ресурсов. Инструкции для уменьшения набора данных приведены в коде. 

+ Это средство для T-SQL "выполнение запроса", такие как [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

+ [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak), которую можно [Загрузите и восстановите](demo-data-nyctaxi-in-sql.md) на ваш локальный экземпляр ядра СУБД. Размер файла составляет около 90 МБ.

+ SQL Server 2019 предварительной версии экземпляр ядра СУБД, с помощью интеграции R и служб машинного обучения.

Проверьте версию, выполнив **`SELECT @@Version`** как запрос T-SQL в средстве запросов. Выходные данные должны быть «Microsoft SQL Server (CTP 2.0) - 2019 15.0.x».

Проверьте доступность пакетов R, возвращая неверный формат список всех пакетов R, установленные с помощью вашего экземпляра компонента database engine:

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

## <a name="connect-to-the-database"></a>Соединиться с базой данных

Запустите среду Management Studio и подключитесь к экземпляру ядра базы данных. В обозревателе объектов проверьте [базы данных NYCTaxi_Sample](demo-data-nyctaxi-in-sql.md) существует. 

## <a name="create-calculatedistance"></a>Создание CalculateDistance

Демонстрационная база данных в состав скалярной функции для расчета расстояния, но наши хранимая процедура работает лучше с помощью функции, возвращающие табличные значения. Выполните следующий сценарий для создания **CalculateDistance** функция, используемая в [шаг обучения](#training-step) позже.

Чтобы проверить, была создана функция, проверьте \Programmability\Functions\Table-valued функции в разделе **NYCTaxi_Sample** базы данных в обозревателе объектов.

```sql
USE NYCTaxi_sample
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[CalculateDistance] (
    @Lat1 FLOAT
    ,@Long1 FLOAT
    ,@Lat2 FLOAT
    ,@Long2 FLOAT
    )
    -- User-defined function calculates the direct distance between two geographical coordinates.
RETURNS TABLE
AS
RETURN

SELECT COALESCE(3958.75 * ATAN(SQRT(1 - POWER(t.distance, 2)) / nullif(t.distance, 0)), 0) AS direct_distance
FROM (
    VALUES (CAST((SIN(@Lat1 / 57.2958) * SIN(@Lat2 / 57.2958)) + (COS(@Lat1 / 57.2958) * COS(@Lat2 / 57.2958) * COS((@Long2 / 57.2958) - (@Long1 / 57.2958))) AS DECIMAL(28, 10)))
    ) AS t(distance)
GO
 ```

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>Определение процедуры для создания и обучения моделей каждого раздела

Этот учебник создает оболочку скрипт R в хранимой процедуре. На этом шаге вы создадите хранимую процедуру, которая использует R для создания набора входных данных, создадите модель классификации для прогнозирования результатов подсказки, а затем сохраняет ее в базе данных.

Между входными данными параметров, используемый этим скриптом, вы увидите **input_data_1_partition_by_columns** и **input_data_1_order_by_columns**. Вспомним, что эти параметры представляют собой механизм, по которому секционирована моделирования происходит. Параметры передаются в качестве входных данных для [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) для обработки секций с помощью внешнего скрипта выполняется один раз для каждой секции. 

Для этой хранимой процедуры, [использования параллелизма](#parallel) для сократить время до завершения.

После запуска этого скрипта вы увидите **train_rxLogIt_per_partition** в процедурах \Programmability\Stored под **NYCTaxi_Sample** базы данных в обозревателе объектов. Вы должны увидеть новую таблицу, которая используется для хранения моделей: **dbo.nyctaxi_models**.

```sql
USE NYCTaxi_Sample
GO

CREATE
    OR

ALTER PROCEDURE [dbo].[train_rxLogIt_per_partition] (@input_query NVARCHAR(max))
AS
BEGIN
    DECLARE @start DATETIME2 = SYSDATETIME()
        ,@model_generation_duration FLOAT
        ,@model VARBINARY(max)
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name();

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    # Make sure InputDataSet is not empty. In parallel mode, if one thread gets zero data, an error occurs
    if (nrow(InputDataSet) > 0) {
    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    
    # build classification model to predict a tip outcome
    duration <- system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet))[3];

    # First, serialize a model to and put it into a database table
    modelbin <- as.raw(serialize(logitObj, NULL));

    # Create the data source. To reduce data size, add rowsPerRead=500000 to cut the dataset by half.
    ds <- RxOdbcData(table="ml_models", connectionString=connStr);

    # Store the model in the database
    model_name <- paste0("nyctaxi.", InputDataSet[1,]$payment_type);
    
    rxWriteObject(ds, model_name, modelbin, version = "v1",
    keyName = "model_name", valueName = "model_object", versionName = "model_version", overwrite = TRUE, serialize = FALSE);
    } 
    
    '
        ,@input_data_1 = @input_query
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@input_data_1_order_by_columns = N'passenger_count'
        ,@parallel = 1
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS NONE
END;
GO
```

<a name="parallel"></a>

### <a name="parallel-execution"></a>Параллельное выполнение

Обратите внимание, что [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) входные данные включать  **@parallel= 1**, где можно включить параллельную обработку. В отличие от предыдущих выпусков, в SQL Server 2019, установка  **@parallel= 1** предоставляет более надежные подсказку оптимизатора запросов, что более вероятно, результат параллельного выполнения.

По умолчанию оптимизатор запросов, как правило, чтобы соблюдалась  **@parallel= 1** в таблицах, имеющих более 256 строки, но если можно обработать это явным образом задав  **@parallel= 1** как показано в следующем скрипт.

> [!Tip]
> Для обучения workoads, можно использовать **@parallel** для любого сценария произвольные обучения, даже те, с помощью алгоритмов Майкрософт rx. Как правило только алгоритмы RevoScaleR (с префикса rx) предлагают параллелизм в сценариях обучения в SQL Server. Но новый параметр, можно распараллеливать скрипт, который вызывает функции, включая функции R открытым исходным кодом, разработанная специально не с данной возможностью. Это работает, поскольку секции имеют сходства с определенными потоками, чтобы выполнить все операции, вызывается в скрипте на основе каждой секции, в данном потоке.

<a name="training-step"></a>

## <a name="run-the-procedure-and-train-the-model"></a>Выполните процедуру и обучения модели

В этом разделе сценарий обучает модель, вы создали и сохранили на предыдущем шаге. В приведенных ниже примерах демонстрируются два подхода для обучения модели: с помощью полного набора данных или части данных. 

Ожидается, что этот шаг, чтобы занять некоторое время. Обучение с большим объемом вычислений, выполнив несколько минут. Если системных ресурсов, особенно памяти недостаточно для нагрузки, используйте подмножество данных. Во втором примере содержит синтаксис.

```sql
--Example 1: train on entire dataset
EXEC train_rxLogIt_per_partition N'
SELECT payment_type, tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

```sql
--Example 2: Train on 20 percent of the dataset to expedite processing.
EXEC train_rxLogIt_per_partition N'
  SELECT tipped, payment_type, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample TABLESAMPLE (20 PERCENT) REPEATABLE (98074)
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

> [!NOTE]
> Если вы используете другие рабочие нагрузки, можно добавить `OPTION(MAXDOP 2)` в инструкцию SELECT, если вы хотите ограничить обработку запросов только 2 ядра.

## <a name="check-results"></a>Результаты проверки

В таблице модели должно быть пять различных моделей, в зависимости от пять секций, сегментированных по пять оплаты типы. Модели находятся в **ml_models** источника данных.

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>Определение процедуры для прогнозирования результатов

Те же параметры можно использовать для оценки. Следующий пример содержит сценарий R, будет оценки с помощью подходящей модели для секции, которую в настоящее время обрабатывается.

Как и раньше создайте хранимую процедуру программы-оболочки для кода R.

```sql
USE NYCTaxi_Sample
GO

-- Stored procedure that scores per partition. 
-- Depending on the partition being processed, a model specific to that partition will be used
CREATE
    OR

ALTER PROCEDURE [dbo].[predict_per_partition]
AS
BEGIN
    DECLARE @predict_duration FLOAT
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name()
        ,@input_query NVARCHAR(max);

    SET @input_query = 'SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance, payment_type
                          FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)
                          CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d'

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    if (nrow(InputDataSet) > 0) {

    #Get the partition that is currently being processed
    current_partition <- InputDataSet[1,]$payment_type;

    #Create the SQL query to select the right model
    query_getModel <- paste0("select model_object from ml_models where model_name = ", "''", "nyctaxi.",InputDataSet[1,]$payment_type,"''", ";")
    

    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
        
    #Define data source to use for getting the model
    ds <- RxOdbcData(sqlQuery = query_getModel, connectionString = connStr)

    # Load the model
    modelbin <- rxReadObject(ds, deserialize = FALSE)
    # unserialize model
    logitObj <- unserialize(modelbin);

    # predict tipped or not based on model
    predictions <- rxPredict(logitObj, data = InputDataSet, overwrite = TRUE, type = "response", writeModelVars = TRUE
        , extraVarsToWrite = c("payment_type"));        
    OutputDataSet <- predictions
    
    } else {
        OutputDataSet <- data.frame(integer(), InputDataSet[,]);        
    }
    '
        ,@input_data_1 = @input_query
        ,@parallel = 1
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS((
                tipped_Pred INT
                ,payment_type VARCHAR(5)
                ,tipped INT
                ,passenger_count INT
                ,trip_distance FLOAT
                ,trip_time_in_secs INT
                ,direct_distance FLOAT
                ));
END;
GO
```

## <a name="create-a-table-to-store-predictions"></a>Создание таблицы для хранения прогнозов

```sql
CREATE TABLE prediction_results (
    tipped_Pred INT
    ,payment_type VARCHAR(5)
    ,tipped INT
    ,passenger_count INT
    ,trip_distance FLOAT
    ,trip_time_in_secs INT
    ,direct_distance FLOAT
    );

TRUNCATE TABLE prediction_results
GO
```

## <a name="run-the-procedure-and-save-predictions"></a>Выполните процедуру и сохранить прогнозов

```sql
INSERT INTO prediction_results (
    tipped_Pred
    ,payment_type
    ,tipped
    ,passenger_count
    ,trip_distance
    ,trip_time_in_secs
    ,direct_distance
    )
EXECUTE [predict_per_partition]
GO
```

## <a name="view-predictions"></a>Представление прогнозов

Поскольку хранятся прогнозов, можно выполнить простой запрос для возврата результирующего набора.

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>Следующие шаги

В этом руководстве вы использовали [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) для перебора секционированных данных операций. Для ближе рассмотрим вызов внешних скриптов в хранимых процедурах и помощью функций RevoScaleR, перейдите к следующему учебнику.

> [!div class="nextstepaction"]
> [Пошаговое руководство по R и SQL Server](walkthrough-data-science-end-to-end-walkthrough.md)

<!--
## Old intro

**(Not for production workloads)**

One of the more common approaches for executing R or Python code on SQL data is providing script as an input parameter to the [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure. In this CTP release, SQL Server 2019 adds new parameters to `sp_execute_external_script` to process partitions with the external script executing once for every partition:

| Parameter | Usage |
|-----------|-------|
| **input_data_1_partition_by_columns** | Specifies which columns to partition by. |
| **input_data_1_order_by_columns** | Specifies which columns to order by.  |

Partitions are an organizational mechanism for stratified data that naturally segments into a given classification scheme. Common examples include partitioning by geographic region, by date and time, by age or gender, and so forth. Given the existence of partitioned data, you might want to execute script over the entire data set, with the ability to model, train, and score partitions that remain intact over all these operations. Calling `sp_execute_external_script` with the new parameters allows you to do just that.

You can run this operation in parallel by combining `partition_by` with `@parallel`. If the input query can be parallelized, set `@parallel=1` as part of your arguments to `sp_execute_external_script`. By default, the query optimizer operates under `@parallel=1` on tables having more than 256 rows.

When the scenario is training, one advantage is that any arbitrary training script, even those using non-Microsoft-rx algorithms, can be parallelized by also using the @parallel parameter. Typically, you would have to use RevoScaleR algorithms (with the rx prefix) to obtain parallelism in training scenarios in SQL Server. But with the new parameter, you can parallelize a script that calls functions not specifically engineered with that capability.
-->
