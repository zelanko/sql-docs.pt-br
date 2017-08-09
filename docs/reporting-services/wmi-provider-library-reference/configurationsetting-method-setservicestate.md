---
title: "Método SetServiceState (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8964b2b0886ffd0483e48c8e9baf91ab9b2dae3d
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-method---setservicestate"></a>Método ConfigurationSetting - SetServiceState
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
 > Essa configuração foi substituída a partir do SQL Server 2016 Reporting Services atualização cumulativa 2. O portal da web sempre será habilitado. O valor será ignorado.
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

