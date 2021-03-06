---
title: sp_replmonitorhelpsubscription (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpsubscription_TSQL
- sp_replmonitorhelpsubscription
helpviewer_keywords:
- sp_replmonitorhelpsubscription
ms.assetid: a681b2db-c82d-4624-a10c-396afb0ac42f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9ac45c3b25e1a13366ae273b8d21d7e41e768251
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748315"
---
# <a name="spreplmonitorhelpsubscription-transact-sql"></a>Хранимая процедура sp_replmonitorhelpsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Возвращает сведения о текущем состоянии подписок, относящихся к одной или нескольким публикациям на издателе, и одну строку для каждой возвращенной подписки. Эта хранимая процедура, используемая для наблюдения за репликацией, выполняется на распространителе в базе данных распространителя.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_replmonitorhelpsubscription [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @mode = ] mode ]  
    [ , [ @topnum = ] topnum ]   
    [ , [ @exclude_anonymous = ] exclude_anonymous ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>Аргументы  
 [ **@publisher** =] **"***издателя***"**  
 Имя издателя, состояние которого отслеживается. *издатель* — **sysname**, со значением по умолчанию NULL. Если **null**, возвращаются сведения обо всех издателях, использующих распространитель.  
  
 [ **@publisher_db** =] **"***publisher_db***"**  
 Имя опубликованной базы данных. *publisher_db* — **sysname**, со значением по умолчанию NULL. Если значение равно NULL, возвращаются сведения для всех баз данных, публикуемых данным издателем.  
  
 [ **@publication** =] **"***публикации***"**  
 Имя отслеживаемой публикации. *Публикация* — **sysname**, со значением по умолчанию NULL.  
  
 [ **@publication_type** =] *publication_type*  
 Тип публикации. *publication_type* — **int**, и может принимать одно из следующих значений.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**0**|Публикация транзакций.|  
|**1**|Публикация моментальных снимков.|  
|**2**|Публикация слиянием.|  
|NULL (по умолчанию)|Репликация пытается определить тип публикации.|  
  
 [ **@mode** =] *режим*  
 Режим фильтрации возвращаемых сведений о подписках. *режим* — **int**, и может принимать одно из следующих значений.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**0** (по умолчанию)|Возвращать все подписки.|  
|**1**|Возвращать подписки с ошибками.|  
|**2**|Возвращать подписки с предупреждениями о нарушениях пороговых показателей.|  
|**3**|Возвращать подписки с ошибками или предупреждениями о нарушениях пороговых показателей.|  
|**4**|Возвращает верхний 25 подписок худшей производительностью.|  
|**5**|Возвращать 50 подписок с худшей производительностью.|  
|**6**|Возвращать подписки, синхронизируемые в данный момент.|  
|**7**|Возвращать подписки, не синхронизируемые в данный момент.|  
  
 [ **@topnum** =] *topnum*  
 Ограничивает результирующий набор указанным числом подписок, которые берутся с начала списка подписок. *topnum* — **int**, не имеет значения по умолчанию.  
  
 [ **@exclude_anonymous** =] *exclude_anonymous*  
 Указывает, исключать ли из результирующего набора анонимные подписки по запросу. *exclude_anonymous* — **бит**, значение по умолчанию **0**; значение **1** подразумевает, что анонимные подписки исключаются, а значение из **0**  означает, что они включаются.  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 Только для внутреннего применения.  
  
## <a name="result-sets"></a>Результирующие наборы  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**status**|**int**|Проверяет состояние всех агентов репликации, связанных с публикацией, и возвращает самое высокое состояние из обнаруженных с учетом следующего порядка:<br /><br /> **6** = ошибка<br /><br /> **5** = Повтор<br /><br /> **2** = остановлена<br /><br /> **4** = бездействует<br /><br /> **3** = выполняется<br /><br /> **1** = запущен|  
|**Предупреждение**|**int**|Максимальный уровень предупреждений, выдаваемых подпиской, принадлежащей публикации; это значение может быть результатом операции логического OR над одним или несколькими из следующих значений:<br /><br /> **1** = expiration — подписка на публикацию транзакций не была синхронизирована пороговым сроком хранения.<br /><br /> **2** = latency — время, необходимое для репликации данных транзакционного издателя на подписчик, превысило пороговое значение, в секундах.<br /><br /> **4** = mergeexpiration — подписка на публикацию слиянием не была синхронизирована пороговым сроком хранения.<br /><br /> **8** = mergefastrunduration — время, затраченное на завершение синхронизации подписки слиянием, превысило пороговое значение, в секундах, быстрое сетевое подключение.<br /><br /> **16** = mergeslowrunduration — время, затраченное на завершение синхронизации подписки слиянием через медленное или коммутируемое сетевое подключение превышает пороговое значение, в секундах.<br /><br /> **32** = mergefastrunspeed — скорость доставки строк во время синхронизации подписки слиянием не для поддержки пороговой, в строках в секунду, через быстрое сетевое подключение.<br /><br /> **64** = mergeslowrunspeed — скорость доставки строк во время синхронизации подписки слиянием не поддерживать пороговой, в строках в секунду, через медленное или коммутируемое сетевое подключение.|  
|**подписчик**|**sysname**|Имя подписчика.|  
|**subscriber_db**|**sysname**|Имя базы данных, использующейся подпиской.|  
|**publisher_db**|**sysname**|Имя базы данных публикации.|  
|**публикации**|**sysname**|Имя публикации.|  
|**publication_type**|**int**|Тип публикации, может принимать одно из следующих значений:<br /><br /> **0** = публикация транзакций<br /><br /> **1** = публикация моментальных снимков<br /><br /> **2** = публикация слиянием|  
|**Подтип**|**int**|Тип подписки может принимать одно из следующих значений:<br /><br /> **0** = Принудительная<br /><br /> **1** = по запросу<br /><br /> **2** = анонимная|  
|**Задержка**|**int**|Наибольшая задержка (в секундах) при изменении данных, зафиксированная для публикации транзакций агентом чтения журнала или агентом распространителя.|  
|**latencythreshold**|**int**|Максимальная задержка для публикации транзакций, при превышении которой создается предупреждение.|  
|**agentnotrunning**|**int**|Время в часах, в течение которого агент не был запущен.|  
|**agentnotrunningthreshold**|**int**|Время в часах, в течение которого агент может не быть запущен, но предупреждения не последует.|  
|**timetoexpiration**|**int**|Время в часах, после которого срок действия подписки истекает, если она не будет синхронизирована.|  
|**expirationthreshold**|**int**|Время в часах, после которого срок действия подписки истекает, и создается предупреждение.|  
|**last_distsync**|**datetime**|Дата и время последнего запуска агента распространителя.|  
|**distribution_agentname**|**sysname**|Имя задания агента распространителя для подписки на публикацию транзакций.|  
|**mergeagentname**|**sysname**|Имя задания агента слияния для подписки на публикацию слиянием.|  
|**mergesubscriptionfriendlyname**|**sysname**|Понятное имя подписки.|  
|**mergeagentlocation**|**sysname**|Имя сервера, на котором запущен агент слияния.|  
|**mergeconnectiontype**|**int**|Соединение, использующееся для синхронизации подписки на публикацию слиянием, может быть одного из следующих типов:<br /><br /> **1** = локальная сеть (LAN)<br /><br /> **2** = коммутируемое сетевое соединение<br /><br /> **3** = веб-синхронизации.|  
|**mergePerformance**|**int**|Производительность последней синхронизации по сравнению со всеми синхронизациями для данной подписки. Вычисляется как скорость доставки последней синхронизации, поделенная на среднее арифметическое скоростей доставки для всех предыдущих синхронизаций.|  
|**mergerunspeed**|**float**|Скорость доставки последней синхронизации подписки.|  
|**mergerunduration**|**int**|Время, затраченное на последнюю синхронизацию подписки.|  
|**monitorranking**|**int**|Ранжирующее значение для упорядочивания подписок в результирующем наборе может быть одним из следующих.<br /><br /> Для публикаций транзакций.<br /><br /> **60** = ошибка<br /><br /> **56** = предупреждение: критическое для производительности<br /><br /> **52** = предупреждение: срок действия скоро истекает или истек срок действия<br /><br /> **50** = предупреждение: подписка не инициализирована<br /><br /> **40** = Повтор сбойной команды<br /><br /> **30** = не выполняется (завершено успешно)<br /><br /> **20** = выполняется (запуск, выполнение или бездействие)<br /><br /> Для публикаций слиянием.<br /><br /> **60** = ошибка<br /><br /> **56** = предупреждение: критическое для производительности<br /><br /> **54** = предупреждение: длительное слияние<br /><br /> **52** = предупреждение: срок действия скоро истекает<br /><br /> **50** = предупреждение: подписка не инициализирована<br /><br /> **40** = Повтор сбойной команды<br /><br /> **30** = выполняется (запуск, выполнение или бездействие)<br /><br /> **20** = не выполняется (завершено успешно)|  
|**distributionagentjobid**|**binary(16)**|Идентификатор задания агента распространителя для подписки на публикацию транзакций.|  
|**mergeagentjobid**|**binary(16)**|Идентификатор задания агента слияния для подписки на публикацию слиянием.|  
|**distributionagentid**|**int**|Идентификатор задания агента распространителя для подписки.|  
|**distributionagentprofileid**|**int**|Идентификатор профиля агента распространителя.|  
|**mergeagentid**|**int**|Идентификатор задания агента слияния для подписки.|  
|**mergeagentprofileid**|**int**|Идентификатор профиля агента слияния.|  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **0** (успешное завершение) или **1** (неуспешное завершение)  
  
## <a name="remarks"></a>Примечания  
 **sp_replmonitorhelpsubscription** используется со всеми типами репликации.  
  
 **sp_replmonitorhelpsubscription** упорядочивает результирующий набор, в зависимости от серьезности состояния подписки, которая определяется по значению *monitorranking*. Например, строки всех подписок в состоянии ошибки находятся выше строк подписок с предупреждениями.  
  
## <a name="permissions"></a>Разрешения  
 Только члены **db_owner** или **replmonitor** предопределенной роли базы данных в базе данных распространителя могут выполнять процедуру **sp_replmonitorhelpsubscription**.  
  
## <a name="see-also"></a>См. также  
 [Наблюдение за репликацией программным образом](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
