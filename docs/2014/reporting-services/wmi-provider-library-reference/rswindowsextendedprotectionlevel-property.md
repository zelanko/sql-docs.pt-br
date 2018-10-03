---
title: Propriedade RSWindowsExtendedProtectionLevel (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 095d09011199aae209f4e659fdd1f9719a5a5ba8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172096"
---
# <a name="rswindowsextendedprotectionlevel-property-wmi-msreportserverconfigurationsetting"></a>Propriedade RSWindowsExtendedProtectionLevel (WMI MSReportServer_ConfigurationSetting)
  Retorna um valor de cadeia de caracteres que indica o nível de proteção para o qual o servidor de relatório está configurado para oferecer suporte. Esta propriedade é somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim RSWindowsExtendedProtectionLevel As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionLevel;  
```  
  
## <a name="remarks"></a>Comentários  
 Retorna um valor de cadeia de caracteres que indica o nível de proteção para o qual o servidor de relatório está configurado para oferecer suporte. Se o servidor de relatório ao qual o provedor WMI está conectado não oferecer suporte à proteção estendida, “” (cadeia de caracteres vazia) será retornado. A lista a seguir mostra os valores válidos:  
  
 `“Off” | “Allow” | “Require”`  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade RSWindowsExtendedProtectionScenario &#40;Msreportserver_configurationsetting&#41&#41;](rswindowsextendedprotectionscenario-property.md)   
 [Método SetExtendedProtectionSettings &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setextendedprotectionsettings.md)   
 [Proteção Estendida para Autenticação com o Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [Arquivo de configuração RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
  
  
