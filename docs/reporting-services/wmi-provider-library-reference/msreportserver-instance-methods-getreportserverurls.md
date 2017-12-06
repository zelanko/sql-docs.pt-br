---
title: "Método GetReportServerUrls (WMI MSReportServer_Instance) | Microsoft Docs"
ms.custom: 
ms.date: 06/09/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
caps.latest.revision: "12"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1d1042cfa240c6c115a8461fcd3eb1387fe66639
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
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
  
## <a name="remarks"></a>Comentários  
 Os métodos expostos pelos objetos de gerenciamento de WMI são chamados pela função InvokeMethod. Para obter mais informações, consulte "Executando Métodos em Objetos de Gerenciamento" na documentação da WMI do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
