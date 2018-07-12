---
title: Método SetExtendedProtectionSettings (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2d8e7232-42f4-41b6-98eb-c856f6c85d8c
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fbc49b6978c9d60344795b3c05729e14e9fa3838
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37181473"
---
# <a name="setextendedprotectionsettings-method-wmi-msreportserverconfigurationsetting"></a>Método SetExtendedProtectionSettings (WMI MSReportServer_ConfigurationSetting)
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
 As propriedades RSWindowsExtendedProtectionLevel e RSWindowsExtendedProtectionScenario aplicam-se quando AuthenticationTypes no arquivo RSReportServer.config inclui RSWindowNTLM, RSWindowsNegotiate ou RSWindowsKerberos. Definir essas propriedades afeta a maneira como os usuários e o software cliente se autenticam com um servidor de relatórios. É recomendável que você leia a documentação para proteção estendida antes de definir ExtendedProtectionLevel como `Allow` ou `Require`.  
  
 Para definir o ExtendedProtectionLevel, o usuário deve ser membro do grupo BUILTIN\Administradores no servidor de relatório.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade RSWindowsExtendedProtectionScenario &#40;Msreportserver_configurationsetting&#41&#41;](rswindowsextendedprotectionscenario-property.md)   
 [Propriedade RSWindowsExtendedProtectionLevel &#40;Msreportserver_configurationsetting&#41&#41;](rswindowsextendedprotectionlevel-property.md)   
 [Proteção Estendida para Autenticação com o Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [Arquivo de configuração RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
  
  
