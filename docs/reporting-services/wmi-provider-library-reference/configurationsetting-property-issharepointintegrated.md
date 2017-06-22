---
title: Propriedade IsSharePointIntegrated (WMI) | Microsoft Docs
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
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: c548fed8-5e04-4faf-8b10-b37c86178056
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 60a335947abf0fc19297ec16737071a708732a33
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="configurationsetting-property---issharepointintegrated"></a>Propriedade ConfigurationSetting - IsSharePointIntegrated
  Especifica se o servidor de relatório está no modo integrado do SharePoint. A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], essa propriedade sempre retorna **Falso** porque, no modo do SharePoint, as instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são serviços compartilhados do SharePoint e não são controladas por provedores WMI.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>Valores da propriedade  
 Um objeto **Boolean** que indica se o servidor de relatório está no modo integrado do SharePoint.  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
