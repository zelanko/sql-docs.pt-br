---
title: Método GetReportServerUrls (WMI MSReportServer_Instance) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 148e0ece44e97bd4c559bbed9cc95aa97092dffb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171038"
---
# <a name="getreportserverurls-method-wmi-msreportserverinstance"></a>Método GetReportServerUrls (WMI MSReportServer_Instance)
  Retorna uma lista de URLs que os usuários podem usar para acessar o servidor de relatório e o gerenciador de relatórios.  
  
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
 Uma matriz que contém os aplicativos que estão instalados. Os valores são `ReportServerWebService` ou `ReportManager`.  
  
 *URLs[]*  
 Uma matriz que contém as Urls registradas com êxito.  
  
 *Comprimento*  
 Um valor de inteiro que contém o tamanho das matrizes retornadas.  
  
 *HRESULT*  
 Um valor que indica êxito ou um código de erro.  
  
## <a name="return-values"></a>Valores de retorno  
  
## <a name="remarks"></a>Comentários  
 Os métodos expostos pelos objetos de gerenciamento de WMI são chamados pela função InvokeMethod. Para obter mais informações, consulte "Executando Métodos em Objetos de Gerenciamento" na documentação da WMI do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
