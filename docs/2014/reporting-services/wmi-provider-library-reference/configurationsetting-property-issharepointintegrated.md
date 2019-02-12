---
title: Propriedade de IsSharePointIntegrated (WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: c548fed8-5e04-4faf-8b10-b37c86178056
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 96c8db6fa6d21c0354047061d708250861f0b0c4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56016677"
---
# <a name="issharepointintegrated-property-wmi"></a>Propriedade IsSharePointIntegrated (WMI)
  Especifica se o servidor de relatório está no modo integrado do SharePoint. A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], essa propriedade sempre retorna `False` porque, em modo do SharePoint, as instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são serviços compartilhados do SharePoint e não são controladas por provedores WMI.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>Valores da propriedade  
 Um objeto `Boolean` que indica se o servidor de relatório está no modo integrado do SharePoint.  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
