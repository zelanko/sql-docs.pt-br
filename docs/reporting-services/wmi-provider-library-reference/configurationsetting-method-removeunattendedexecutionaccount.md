---
title: "Método de ConfigurationSetting – RemoveUnattendedExecutionAccount | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
apiname: RemoveUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting Class)
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: RemoveUnattendedExecutionAccount method
ms.assetid: 77e371c1-7c26-44f9-9119-7c8dc838db32
caps.latest.revision: "18"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 78c4d4b74e3090da3fd4397dc99148c2230fe795
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---removeunattendedexecutionaccount"></a>Método de ConfigurationSetting – RemoveUnattendedExecutionAccount
  Exclui a entrada de conta de execução autônoma do arquivo de configuração do servidor de relatório.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub RemoveUnattendedExecutionAccount(ByRef HRESULT as Int32)  
```  
  
```csharp  
public void RemoveUnattendedExecutionAccount (out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
