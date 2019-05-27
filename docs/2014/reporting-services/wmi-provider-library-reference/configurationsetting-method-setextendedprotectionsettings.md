---
title: Método SetExtendedProtectionSettings (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2d8e7232-42f4-41b6-98eb-c856f6c85d8c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0583632b9c9b8548e16b7a74718b48cad8066ced
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098037"
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
  
 `"Off | Allow | Require"`  
  
 *ExtendedProtectionScenario*  
 Define o RSWindowsExtendedProtectionScenario no arquivo RSReportserver.config. O valor obrigatório não diferencia maiúsculas de minúsculas.  
  
 A lista a seguir mostra os valores válidos:  
  
 `"Any" | "Proxy" | "Direct"`  
  
## <a name="remarks"></a>Comentários  
 As propriedades RSWindowsExtendedProtectionLevel e RSWindowsExtendedProtectionScenario aplicam-se quando AuthenticationTypes no arquivo RSReportServer.config inclui RSWindowNTLM, RSWindowsNegotiate ou RSWindowsKerberos. Definir essas propriedades afeta a maneira como os usuários e o software cliente se autenticam com um servidor de relatórios. É recomendável ler a documentação da proteção estendida antes de definir ExtendedProtectionLevel como `Allow` ou `Require`.  
  
 Para definir o ExtendedProtectionLevel, o usuário deve ser membro do grupo BUILTIN\Administradores no servidor de relatório.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade RSWindowsExtendedProtectionScenario &#40;WMI MSReportServer_ConfigurationSetting&#41;](rswindowsextendedprotectionscenario-property.md)   
 [Propriedade RSWindowsExtendedProtectionLevel &#40;WMI MSReportServer_ConfigurationSetting&#41;](rswindowsextendedprotectionlevel-property.md)   
 [Proteção Estendida para Autenticação com o Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [Arquivo de configuração RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
  
  
