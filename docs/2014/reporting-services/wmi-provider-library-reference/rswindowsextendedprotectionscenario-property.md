---
title: Propriedade RSWindowsExtendedProtectionScenario (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5ac7ab80-9adf-4f65-abfa-fedf53b082b5
caps.latest.revision: 5
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3eca2ad0b54e6efad5e197528b7aa0c48ecb3489
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37309077"
---
# <a name="rswindowsextendedprotectionscenario-property-wmi-msreportserverconfigurationsetting"></a>Propriedade RSWindowsExtendedProtectionScenario (WMI MSReportServer_ConfigurationSetting)
  Retorna um valor de cadeia de caracteres que indica o cenário de proteção estendida que o servidor de relatório está configurado para permitir.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim RSWindowsExtendedProtectionScenario As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionScenario;  
```  
  
## <a name="remarks"></a>Remarks  
 Retorna um valor de cadeia de caracteres que indica o cenário de proteção estendida que o servidor de relatório está configurado para permitir. Se o servidor de relatório ao qual o provedor WMI está conectado não oferecer suporte à proteção estendida, “” (cadeia de caracteres vazia) será retornado.  
  
 A lista a seguir mostra os valores válidos:  
  
 `”Any | Proxy | Direct”`  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade RSWindowsExtendedProtectionLevel &#40;Msreportserver_configurationsetting&#41&#41;](rswindowsextendedprotectionlevel-property.md)   
 [Método SetExtendedProtectionSettings &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setextendedprotectionsettings.md)   
 [Proteção Estendida para Autenticação com o Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [Arquivo de configuração RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
  
  
