---
title: Параметры запуска службы ядра СУБД | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- single-user mode [SQL Server], startup option
- overriding default startup options
- minimal configuration mode [SQL Server], startup option
- default startup options
- temporarily override default startup options [SQL Server]
- startup options [SQL Server]
- starting SQL Server, options
ms.assetid: d373298b-f6cf-458a-849d-7083ecb54ef5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 29984a52d711ef02c3c3b640ef8d59323806c2bd
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/30/2018
ms.locfileid: "52641345"
---
# <a name="database-engine-service-startup-options"></a>Параметры запуска службы Database Engine
  Параметры запуска задают определенное расположение файлов, необходимых для запуска, а также некоторые условия для сервера. Большинству пользователей не нужно задавать параметры запуска за исключением случаев, когда устраняются проблемы служб [!INCLUDE[ssDE](../../includes/ssde-md.md)] , либо если возникла неожиданная проблема и необходимо использовать параметр запуска по указанию поддержки пользователей служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!WARNING]  
>  Неправильное использование параметров запуска может повлиять на производительность сервера или помешать запуску [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="about-startup-options"></a>О параметрах запуска  
 При установке [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]программа установки сохраняет набор параметров запуска в реестр [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. С помощью этих параметров можно указать альтернативный файл базы данных master, файл журнала базы данных master и файл журнала ошибок. Если компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] не удается найти необходимые файлы, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на запустится.  
  
 Параметры запуска можно задать в диспетчере конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения см. в статье [Настройка параметров запуска сервера (диспетчер конфигурации SQL Server)](scm-services-configure-server-startup-options.md).  
  
## <a name="list-of-startup-options"></a>Список параметров запуска  
  
|Параметры запуска по умолчанию|Описание|  
|-----------------------------|-----------------|  
|**-d**  *master_file_path*|Полный путь к файлу базы данных master (обычно это "C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\Master.mdf"). Если этот параметр не задан, используются параметры из реестра.|  
|**-e**  *error_log_path*|Полный путь к файлу журнала ошибок (обычно это "C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Log\Errorlog"). Если этот параметр не задан, используются параметры из реестра.|  
|**-l**  *master_log_path*|Полный путь к файлу журнала базы данных master (обычно это "C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\mastlog.ldf"). Если данный параметр не указан, будут использованы параметры из реестра.|  
  
|Дополнительные параметры запуска|Описание|  
|---------------------------|-----------------|  
|**-c**|Ускоряет запуск [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] из командной строки. Обычно компонент [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] запускается в виде службы путем вызова диспетчера управления службами. Так как [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] не запускается как служба при запуске из командной строки, используйте параметр **-c** , чтобы пропустить этот шаг.|  
|**-f**|Запускает экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с минимальной конфигурацией. Эта функция полезна в случае, если установленные значения конфигурации (например, слишком большой объем выделяемой памяти) не позволяют выполнить запуск сервера. При запуске [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в режиме минимальной конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] переходит в однопользовательский режим. Дополнительные сведения см. в описании параметра **-m** далее.|  
|**-g**  *memory_to_reserve*|Определяет объем памяти в мегабайтах (МБ), которую [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] будет оставлять другим приложениям внутри процесса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , но за пределами пула памяти [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Память за пределами пула памяти является областью, используемой [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для загрузки элементов, например DLL-файлов расширенных процедур, поставщиков OLE DB, на которые ссылаются распределенные запросы, и объектов автоматизации, на которые ссылаются инструкции [!INCLUDE[tsql](../../includes/tsql-md.md)] . По умолчанию установлено значение 256 МБ.<br /><br /> Этот параметр может помочь при настройке выделения памяти, но только в том случае, если объем физической памяти превышает предел, установленный операционной системой для виртуальной памяти, доступной для приложений. Использование данного параметра может быть целесообразным в конфигурациях с большим объемом памяти, в которых требования [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] к использованию памяти являются нетипичными и виртуальное адресное пространство процесса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] используется в полной мере. Неверное использование этого параметра может привести к появлению условий, при которых экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не будет запущен или может вызвать ошибки времени выполнения.<br /><br /> Используйте значение параметра **-g** по умолчанию, только если в файле журнала ошибок [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не присутствуют следующие предупреждения:<br /><br /> -«Ошибка виртуального выделения байтов: FAIL_VIRTUAL_RESERVE \<размер >»<br /><br /> -«Ошибка виртуального выделения байтов: FAIL_VIRTUAL_COMMIT \<размер >»<br /><br /> Эти сообщения могут свидетельствовать о попытках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] освободить часть пула памяти [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , чтобы выделить пространство для таких элементов, как DLL-файлы расширенных хранимых процедур или объекты автоматизации. В этом случае рассмотрите возможность увеличения размера памяти, зарезервированной с помощью параметра **-g** .<br /><br /> Если используемое значение меньше значения по умолчанию, объем памяти, доступной пулу ресурсов, управляемому диспетчером памяти SQL Server, и стекам потоков, увеличивается. В свою очередь увеличивается производительность требовательных к памяти рабочих нагрузок в системах, не использующих большое количество расширенных хранимых процедур, распределенных запросов и объектов автоматизации.|  
|**-m**|Запускает экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в однопользовательском режиме. В этом режиме к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может подключиться только один пользователь, и процесс CHECKPOINT не запускается. Процесс CHECKPOINT гарантирует, что завершенные транзакции будут периодически переписываться из кэша диска на устройство базы данных. Этот параметр применяется обычно при возникновении проблем с системными базами данных, которые необходимо исправить. При использовании этого параметра включается параметр sp_configure. По умолчанию параметр allow updates отключен. После запуска [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в однопользовательском режиме каждый член локальной группы администраторов на компьютере сможет подключаться к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] от имени члена предопределенной роли сервера sysadmin. Дополнительные сведения см. в статье [Подключение к SQL Server в случае, если доступ системных администраторов заблокирован](connect-to-sql-server-when-system-administrators-are-locked-out.md). Дополнительные сведения об однопользовательском режиме см. в статье [Запуск SQL Server в однопользовательском режиме](start-sql-server-in-single-user-mode.md).|  
|**-m «Имя клиентского приложения»**|Ограничивает соединения с заданным клиентским приложением, если параметр **-m** используется с **SQLCMD** или [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Например, **-m"SQLCMD"** разрешает только одно подключение, которое должно идентифицироваться как клиентская программа **SQLCMD**. Этот параметр следует использовать, когда [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] запускается в однопользовательском режиме, а единственное доступное соединение занято неизвестным клиентским приложением. Чтобы подключиться с помощью редактора запросов в [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], используйте **-m"Microsoft SQL Server Management Studio - Query"**.<br /><br /> В имени клиентского приложения учитывается регистр символов.<br /><br /> **\*\* Примечание по безопасности \*\*** . Не используйте этот параметр как средство безопасности. Клиентское приложение предоставляет имя клиентского приложения и может указать ложное имя в составе строки подключения.|  
|**-n**|Указывает, что не нужно использовать журнал приложений Windows для регистрации событий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Если экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] запускается с параметром **-n**, рекомендуется также использовать параметр запуска **-e** . В противном случае события [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не регистрируются в журнале.|  
|**-s**|Позволяет запустить именованный экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Если параметр **-s** не задан, будет выполнена попытка запустить экземпляр по умолчанию. Перед запуском программы **sqlservr.exe**в командной строке необходимо перейти в каталог BINN соответствующего экземпляра. Например, если экземпляр Instance1 должен использовать \mssql$Instance1 для своих двоичных файлов, для запуска **sqlservr.exe -s instance1**пользователь должен быть в каталоге \mssql$Instance1\binn.|  
|**-T**  *trace#*|Указывает, что экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] фактически должен запускаться с установленным флагом трассировки (*trace#*). Флаги трассировки используются для запуска сервера в нестандартном режиме. Дополнительные сведения см. в разделе [Флаги трассировки (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).<br /><br /> **\*\* Важно! \*\*** Если задается флаг трассировки с помощью параметра **-T** , используйте заглавную букву T для передачи номера флага трассировки. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]принимает и строчную букву «t», но в этом случае устанавливаются другие внутренние флаги трассировки, которые необходимы только инженерам службы поддержки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . (Параметры, установленные в окне запуска в области управления, не считываются.)|  
|**-x**|Отключает следующие функции наблюдения.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Поддержку статистики времени ЦП и коэффициента попадания в кэш.<br /><br /> Сбор данных для команды DBCC SQLPERF.<br /><br /> Сбор данных для некоторых динамических административных представлений.<br /><br /> Многие точки событий расширенных событий.<br /><br /> <br /><br /> **\*\* Предупреждение \* \***  при использовании **- x** параметр запуска, раздел, которая доступна для диагностики проблем производительности и функциональных проблем [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] значительно сокращается.|  
|**-E**|Увеличивает число экстентов, выделяемых для каждого файла в файловой группе. Данный параметр может быть полезен для приложений с хранилищами данных, имеющих ограниченное число пользователей, которые запускают индексы или просматривают данные. Его нельзя использовать в других приложениях, так как он может неблагоприятно повлиять на производительность. Данный параметр не поддерживается 32-разрядными выпусками [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="using-startup-options-for-troubleshooting"></a>Использование параметров запуска для устранения неполадок  
 Некоторые параметры запуска (например, однопользовательский режим или режим минимальной конфигурации) применяются, главным образом, во время устранения неполадок. Запустить сервер для устранения неполадок с параметром **-m** или **-f** проще всего из командной строки, вручную запустив sqlservr.exe.  
  
> [!NOTE]  
>  Если [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] запускается с помощью **net start**, в параметрах запуска используется косая черта (/), а не дефис (-).  
  
## <a name="using-startup-options-during-normal-operations"></a>Использование параметров запуска в обычной работе  
 Возможно, некоторые параметры потребуется использовать при каждом запуске [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Если требуется запуск с такими параметрами, как **-g**, или с флагом трассировки, лучше всего задать параметры запуска с помощью диспетчера конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Это средство сохраняет параметры запуска в разделе реестра, после чего [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] всегда запускается с этими параметрами.  
  
## <a name="compatibility-support"></a>Поддержка совместимости  
 Параметр **-h**  не поддерживается в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Этот параметр использовался в более ранних версиях 32-битных экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для резервирования виртуального адресного пространства для метаданных памяти с «горячей» заменой при включенных расширениях AWE. Дополнительные сведения см. в разделе [Discontinued SQL Server Features in SQL Server 2014](../../getting-started/discontinued-sql-server-features-in-sql-server-2014.md).  
  
## <a name="related-tasks"></a>Связанные задачи  
 [Настройка параметра конфигураци и сервера scan for startup procs](configure-the-scan-for-startup-procs-server-configuration-option.md)  
  
 [Запуск, остановка, приостановка, возобновление и перезапуск компонента Database Engine, агента SQL и службы браузера SQL Server](start-stop-pause-resume-restart-sql-server-services.md)  
  
## <a name="see-also"></a>См. также  
 [CHECKPOINT (Transact-SQL)](/sql/t-sql/language-elements/checkpoint-transact-sql)   
 [Приложение sqlservr](../../tools/sqlservr-application.md)  
  
  
