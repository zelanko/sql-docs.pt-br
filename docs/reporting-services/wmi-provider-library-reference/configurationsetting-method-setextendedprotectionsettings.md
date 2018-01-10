---
title: "Método SetExtendedProtectionSettings (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2d8e7232-42f4-41b6-98eb-c856f6c85d8c
caps.latest.revision: "7"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f2c5e606cc11ad8e7026dd0d7bebe1d9395d6d2f
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---setextendedprotectionsettings"></a>Método de ConfigurationSetting – SetExtendedProtectionSettings
  O método SetExtendedProtectionSettings é usado para definir as propriedades RSWindowsExtendedProtectionLevel e RSWindowsExtendedProtectionScenario no arquivo de configuração RSReportServer.config do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub SetExtendedProtectionSettings( _  
        ByVal ExtendedProtectionLevel As String, _  
        ByVal ExtendedProtectionScenario As String, _  
        ByRef Warnings() As String, _  
        ByRef Length As Int32, _  
        ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetExtendedProtectionSettings(  
            string ExtendedProtectionLevel,  
            string ExtendedProtectionScenario,  
            out string[] Warnings,  
            out Int32 Length,  
            out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *ExtendedProtectionLevel*  
 Define o RSWindowsExtendedProtectionLevel no arquivo RSRreportserver.config. O valor obrigatório não diferencia maiúsculas de minúsculas.  
  
 A lista a seguir mostra os valores válidos:  
  
 `”Off | Allow | Require”`  
  
 *ExtendedProtectionScenario*  
 Define o RSWindowsExtendedProtectionScenario no arquivo RSReportserver.config. O valor obrigatório não diferencia maiúsculas de minúsculas.  
  
 A lista a seguir mostra os valores válidos:  
  
 `”Any” | “Proxy” | “Direct”`  
  
## <a name="remarks"></a>Remarks  
 As propriedades RSWindowsExtendedProtectionLevel e RSWindowsExtendedProtectionScenario aplicam-se quando AuthenticationTypes no arquivo RSReportServer.config inclui RSWindowNTLM, RSWindowsNegotiate ou RSWindowsKerberos. Definir essas propriedades afeta a maneira como os usuários e o software cliente se autenticam com um servidor de relatórios. É recomendável ler a documentação da proteção estendida antes de definir ExtendedProtectionLevel como **Allow** ou **Require**.  
  
 Para definir o ExtendedProtectionLevel, o usuário deve ser membro do grupo BUILTIN\Administradores no servidor de relatório.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade RSWindowsExtendedProtectionScenario &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario-property.md)   
 [Propriedade RSWindowsExtendedProtectionLevel &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionlevel-property.md)   
 [Proteção Estendida para Autenticação com o Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
