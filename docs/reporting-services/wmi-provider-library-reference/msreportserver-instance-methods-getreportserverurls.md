---
title: Método GetReportServerUrls (WMI MSReportServer_Instance) | Microsoft Docs
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
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620056"
---
# <a name="msreportserverinstance-methods---getreportserverurls"></a>Métodos de MSReportServer_Instance – GetReportServerUrls
  Retorna uma lista de URLs que os usuários podem usar para acessar o servidor de relatório e o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub GetReportServerUrls (ByRef ApplicationName() As String, ByRef URLs()_  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetReportServerUrls(out string[] applicationName,   
    out string[] URLs, out int length, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *ApplicationName[]*  
 Uma matriz que contém os aplicativos que estão instalados. Os valores são **ReportServerWebService** ou **ReportServerWebApp**.  
  
 *URLs[]*  
 Uma matriz que contém as Urls registradas com êxito.  
  
 *Comprimento*  
 Um valor de inteiro que contém o tamanho das matrizes retornadas.  
  
 *HRESULT*  
 Um valor que indica êxito ou um código de erro.  
  
## <a name="return-values"></a>Valores de retorno  
  
## <a name="remarks"></a>Remarks  
 Os métodos expostos pelos objetos de gerenciamento de WMI são chamados pela função InvokeMethod. Para obter mais informações, consulte "Executando Métodos em Objetos de Gerenciamento" na documentação da WMI do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
