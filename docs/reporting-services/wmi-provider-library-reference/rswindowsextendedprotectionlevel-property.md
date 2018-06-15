---
title: Propriedade RSWindowsExtendedProtectionLevel | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c46372fb98ede794afa6cbf1d2621d64cb0200f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33032303"
---
# <a name="rswindowsextendedprotectionlevel-property"></a>Propriedade RSWindowsExtendedProtectionLevel
  Retorna um valor de cadeia de caracteres que indica o nível de proteção para o qual o servidor de relatório está configurado para oferecer suporte. Esta propriedade é somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim RSWindowsExtendedProtectionLevel As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionLevel;  
```  
  
## <a name="remarks"></a>Remarks  
 Retorna um valor de cadeia de caracteres que indica o nível de proteção para o qual o servidor de relatório está configurado para oferecer suporte. Se o servidor de relatório ao qual o provedor WMI está conectado não oferecer suporte à proteção estendida, “” (cadeia de caracteres vazia) será retornado. A lista a seguir mostra os valores válidos:  
  
 `“Off” | “Allow” | “Require”`  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade RSWindowsExtendedProtectionScenario &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario-property.md)   
 [Método SetExtendedProtectionSettings &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)   
 [Proteção Estendida para Autenticação com o Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
