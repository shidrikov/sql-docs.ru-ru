---
title: sp_articleview (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articleview
- sp_articleview_TSQL
helpviewer_keywords:
- sp_articleview
ms.assetid: a3d63fd6-f360-4a2f-8a82-a0dc15f650b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b06d348358a141771816230179ca7deae4e4353a
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132865"
---
# <a name="sparticleview-transact-sql"></a>sp_articleview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Создает представление, определяющее публикуемую статью, когда таблица фильтруется горизонтально или вертикально. Представление используется как фильтруемый источник схемы и данных для целевых таблиц. Эта хранимая процедура может изменять только те статьи, на которые нет подписки. Эта хранимая процедура выполняется на издателе в базе данных публикации.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_articleview [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @view_name = ] 'view_name']  
    [ , [ @filter_clause = ] 'filter_clause']  
    [ , [ @change_active = ] change_active ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @refreshsynctranprocs = ] refreshsynctranprocs ]  
    [ , [ @internal = ] internal ]  
```  
  
## <a name="arguments"></a>Аргументы  
 [  **@publication=**] **"**_публикации_**"**  
 Имя публикации, которая содержит статью. *Публикация* — **sysname**, не имеет значения по умолчанию.  
  
 [  **@article=**] **"**_статье_**"**  
 Имя статьи. *статья* — **sysname**, не имеет значения по умолчанию.  
  
 [  **@view_name=**] **"**_view_name_**"**  
 Имя представления, определяющего опубликованную статью. *view_name* — **nvarchar(386)**, значение по умолчанию NULL.  
  
 [  **@filter_clause=**] **"**_filter_clause_**"**  
 Предложение ограничения (WHERE), которое задает горизонтальный фильтр. При вводе предложения ограничения опустите ключевое слово WHERE. *filter_clause* — **ntext**, значение по умолчанию NULL.  
  
 [  **@change_active =** ] *change_active*  
 Разрешает изменение столбцов в публикациях, на которые имеются подписки. *change_active* — **int**, значение по умолчанию **0**. Если **0**, столбцы не изменяются. Если **1**, представления может быть создано или повторно создан на активных статей, которые имеются подписки.  
  
 [  **@force_invalidate_snapshot =** ] *подписки потребуют*  
 Подтверждает, что действие, выполненное этой хранимой процедурой, может сделать недействительным существующий моментальный снимок. *подписки потребуют* — **бит**, значение по умолчанию **0**.  
  
 **0** означает, что изменения статьи не приводят к недействительности моментального снимка. Если хранимая процедура определяет, что изменение требует создания нового моментального снимка, возникает ошибка и изменения не выполняются.  
  
 **1** указывает, что изменения статьи может привести к недействительности моментального снимка и если существующие подписки потребуют нового моментального снимка, дается разрешение существующий моментальный снимок помечается как устаревшего и создание нового моментального снимка.  
  
 [  **@force_reinit_subscription =]** _этот_  
 Подтверждает, что действие, выполняемое данной хранимой процедурой, может сделать необходимой повторную инициализацию текущих подписок. *Этот* — **бит** значение по умолчанию **0**.  
  
 **0** указывает, что изменения статьи не вызывают повторной инициализации подписки. Если хранимая процедура определяет, что изменение потребует повторной инициализации подписки, то выдается сообщение об ошибке, и изменения не производится.  
  
 **1** указывает, что изменения статьи вызывает существующую подписку для повторной инициализации и дает разрешение произвести повторную инициализацию подписки.  
  
 [ **@publisher**=] **"**_издателя_**"**  
 Указывает, отличный от [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] издателя. *издатель* — **sysname**, значение по умолчанию NULL.  
  
> [!NOTE]  
>  *издатель* не должны использоваться при публикации из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] издателя.  
  
 [ **@refreshsynctranprocs** =] *refreshsynctranprocs*  
 Указывает, будут ли хранимые процедуры, используемые для синхронизации репликации, автоматически создаваться повторно. *refreshsynctranprocs* — **бит**, значение по умолчанию 1.  
  
 **1** означает, что хранимые процедуры будут создаваться повторно.  
  
 **0** означает, что хранимые процедуры не будут создаваться повторно.  
  
 [ **@internal**=] *внутренний*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **0** (успешное завершение) или **1** (неуспешное завершение)  
  
## <a name="remarks"></a>Примечания  
 **sp_articleview** создает представление, определяющее публикуемую статью, вставляет идентификатор этого представления в **sync_objid** столбец [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) таблицы и помещает текст ограничивающего предложения в **filter_clause** столбца. Если все столбцы реплицируются, а не **filter_clause**, **sync_objid** в [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) таблице присваивается идентификатор Базовая таблица, а также использование **sp_articleview** не является обязательным.  
  
 Для публикации вертикально фильтруемой таблицы (то есть для фильтрации столбцов) сначала запустите **sp_addarticle** нет *sync_object* параметра, запустите [sp_articlecolumn &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) один раз для каждого столбца, чтобы быть реплицированы (определяя вертикальный фильтр), а затем запустите **sp_articleview** для создания представления, определяющего опубликованную статью.  
  
 Для публикации горизонтально фильтруемой таблицы (т. е. для фильтрации строк), запустите [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) нет *фильтра* параметра. Запустите [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md), указав все аргументы, включая *filter_clause*. Затем запустите **sp_articleview**, указав все аргументы, включая тот же *filter_clause*.  
  
 Чтобы опубликовать таблицу, отфильтрованную по вертикали и горизонтали, выполнить [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) нет *sync_object* или *фильтра* параметров. Запустите [sp_articlecolumn &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) один раз для каждого реплицируемого столбца, а затем выполните [sp_articlefilter &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) и **sp_ articleview**.  
  
 Если статьи уже существовало представление, определяющее публикуемую статью, **sp_articleview** удалит существующее представление и автоматически создает новую. Если представление было создано вручную (**тип** в [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) — **5**), существующее представление не удаляется.  
  
 Если создается хранимая процедура пользовательского фильтра и представление, определяющее публикуемую статью вручную, не запускайте **sp_articleview**. Вместо этого указать их в качестве *фильтра* и *sync_object* параметров [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), а также соответствующие *тип* значение.  
  
## <a name="example"></a>Пример  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>Разрешения  
 Только члены **sysadmin** предопределенной роли сервера или **db_owner** предопределенной роли базы данных могут выполнять процедуру **sp_articleview**.  
  
## <a name="see-also"></a>См. также  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Определение и изменение статического строкового фильтра](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Хранимые процедуры репликации (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
