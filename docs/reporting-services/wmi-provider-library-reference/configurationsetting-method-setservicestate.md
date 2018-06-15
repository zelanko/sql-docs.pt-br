---
title: Método SetServiceState (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
caps.latest.revision: 20
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7e17d962dce18a3d5f384ba07ff37a1d1f67b7f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33031573"
---
# <a name="configurationsetting-method---setservicestate"></a>Método de ConfigurationSetting – SetServiceState
  Ativa e desativa o Servidor de Relatório do Windows e os serviços Web.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetServiceState(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *EnableWindowsService*  
 Um valor **Boolean** que indica o estado do serviço Windows. Um valor **true** inicia o serviço Servidor de Relatório do Windows; um valor **false** interrompe o serviço do Windows.  
  
 *EnableWebService*  
 Um valor **Boolean** que indica o estado do serviço Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Um valor **true** inicia o serviço Web Servidor de Relatórios; um valor **false** interrompe o serviço Web.  
  
 *EnableReportManager*  
 Um valor **Boolean** que indica o estado desejado do Gerenciador de Relatórios.
 
 > [!NOTE] 
 > Essa configuração foi preterida a partir do SQL Server 2016 Reporting Services Atualização Cumulativa 2. O portal da Web sempre será habilitado. O valor será ignorado.
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
