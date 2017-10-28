---
title: Propriedade SecureConnectionLevel (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SecureConnectionLevel
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
caps.latest.revision: 19
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 926be7ba1e11f82f6306b8828b84823a91b3d515
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-property---secureconnectionlevel"></a>Propriedade ConfigurationSetting - SecureConnectionLevel
  Retorna o nível de conexão segura especificado no arquivo RSReportServer.config. Somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>Valores da propriedade  
 Um valor **inteiro** que representa o nível de conexão segura. Os valores de retorno indicam se o SSL está configurado ou não. Um valor maior ou igual a 1 indica que o SSL está ativado. Um valor de 0 indica que o SSL está desativado.  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

