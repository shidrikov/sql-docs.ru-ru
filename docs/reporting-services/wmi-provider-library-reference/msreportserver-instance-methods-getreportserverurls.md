---
title: Метод GetReportServerUrls (WMI MSReportServer_Instance) | Документы Майкрософт
ms.date: 06/09/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f8749f8b10855154efd7e676f5ee57fae2dd042e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620075"
---
# <a name="msreportserverinstance-methods---getreportserverurls"></a>Методы MSReportServer_Instance — GetReportServerUrls
  Возвращает список URL-адресов, которые пользователи могут использовать для доступа к серверу отчетов и [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)].  
  
## <a name="syntax"></a>Синтаксис  
  
```vb  
Public Sub GetReportServerUrls (ByRef ApplicationName() As String, ByRef URLs()_  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetReportServerUrls(out string[] applicationName,   
    out string[] URLs, out int length, out int HRESULT);  
```  
  
## <a name="parameters"></a>Параметры  
 *ApplicationName[]*  
 Массив, который содержит установленные приложения. Значения: либо **ReportServerWebService** либо **ReportServerWebApp**.  
  
 *URLs[]*  
 Массив, который содержит успешно зарегистрированные URL-адреса.  
  
 *Длина*  
 Целое значение, представляющее длину возвращенных массивов.  
  
 *HRESULT*  
 Значение, показывающее успешное завершение или код ошибки.  
  
## <a name="return-values"></a>Возвращаемые значения  
  
## <a name="remarks"></a>Remarks  
 Методы, доступные в управляющих объектах WMI, вызываются с помощью функции InvokeMethod. Дополнительные сведения см. в разделе «Выполнение методов в управляющих объектах» документации по инструментарию WMI платформы [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
## <a name="requirements"></a>Требования  
 **Пространство имен:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>См. также:  
 [Элементы MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
