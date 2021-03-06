---
title: Неизвестная служба (вход в систему) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: e9b35cb5-d8ae-42ea-b59e-deedc99c4823
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 686eb039660efb6e3596b9dac88fc0d24deacaee
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771836"
---
# <a name="unknown-service-log-on-tab"></a>Неизвестная служба (вкладка «Вход в систему»)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не удается идентифицировать эту службу.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] получает служебные данные от поставщика инструментария WMI на компьютере, где запущена служба. Произошла ошибка при считывании свойств службы или свойства службы являются неполными. Чтобы разрешить проблему, попытайтесь закрыть и заново открыть диспетчер конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или проверьте поставщика инструментария WMI на компьютере, где запущена служба.  
  
 Поставщик WMI является компонентом Windows. Сведения о том, как проверить разрешения на поставщика WMI, см. в разделе «Как настроить инструментарий WMI для отображения состояния сервера в инструментальных средствах SQL Server» электронной документации по SQL Server.  
  
 Если вы уверены, что просматриваете правильную службу, то для указания учетной записи, используемой службой, а также для запуска и остановки службы используйте вкладку **Вход** в диалоговом окне **Свойства неизвестной службы** .  
  
## <a name="options"></a>Параметры  
 **Локальная системная учетная запись**  
 Укажите локальную системную учетную запись, для которой не требуется пароль. Однако локальная системная учетная запись может препятствовать взаимодействию служб с другими серверами, в зависимости от прав доступа, предоставленных этой учетной записи.  
  
 **Эта учетная запись**  
 Укажите локальную или доменную учетную запись, использующую аутентификацию Windows. Для служб рекомендуется использовать доменную учетную запись с минимальными правами. Дополнительные сведения о выборе учетной записи см. в разделе «Настройка учетных записей служб Windows» электронной документации по SQL Server.  
  
 **Имя учетной записи**  
 Укажите имя локальной или доменной учетной записи.  
  
 **Пароль**  
 Введите пароль для учетной записи.  
  
 **Подтверждение пароля**  
 Введите пароль для учетной записи еще раз.  
  
 **Запуск**  
 Запускает службу.  
  
 **Остановить**  
 Остановить службу.  
  
 **Приостановить**  
 Приостановить службу.  
  
 **Возобновить**  
 Возобновить приостановленную работу службы.  
  
  
