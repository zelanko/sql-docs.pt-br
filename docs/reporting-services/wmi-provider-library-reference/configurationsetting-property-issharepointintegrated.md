---
title: Propriedade de IsSharePointIntegrated (WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: c548fed8-5e04-4faf-8b10-b37c86178056
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0bac72cf23cfebf48f58b24bea0b50aa9033bf5d
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65573737"
---
# <a name="configurationsetting-property---issharepointintegrated"></a>Propriedade de ConfigurationSetting – IsSharePointIntegrated
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
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
