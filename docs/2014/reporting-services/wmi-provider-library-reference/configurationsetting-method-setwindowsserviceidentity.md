---
title: Método SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d2cee56a3aa15e00e2de72761eb872f6e297b680
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48067306"
---
# <a name="setwindowsserviceidentity-method-wmi-msreportserverconfigurationsetting"></a>Método SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting)
  Faz com que o serviço do Windows do servidor de relatório seja executado como um usuário do Windows especificado e concede a esta conta permissões de sistema de arquivos suficientes para permitir que o servidor de relatório opere.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub SetWindowsServiceIdentity(UseBuiltInAccount as Boolean, _  
    Account as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetWindowsServiceIdentity(boolean UseBuiltInAccount,   
    string Account, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *UseBuiltInAccount*  
 Indica se a conta especificada é uma conta interna do Windows.  
  
 *Conta*  
 A conta do Windows a ser utilizada para executar o serviço de Windows, no formato "DOMAIN\alias".  
  
 *Senha*  
 A senha para a conta.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
 Quando o *UseBuiltInAccount* parâmetro for definido como `true` e o servidor de relatório está em execução no Microsoft [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)] ou o Windows XP, o valor da *nome*, *domínio*, e *senha* parâmetros serão ignorados e a conta Sistema Local é usada.  
  
 Quando o *UseBuiltInAccount* parâmetro for definido como `true` e o servidor de relatório está em execução no Windows Server 2003, o *domínio* e *senha* propriedades são ignorado, e o campo de nome deve conter "Builtin\NetworkService" ou "Builtin\System" ou "Builtin\LocalService".  
  
 O método SetWindowsServiceIdentity define as permissões de arquivo nos arquivos e nas pastas do diretório de instalação do servidor de relatório.  
  
 A conta especificada na *conta* parâmetro requer `LogonAsService` direitos no Windows. O método concede esse direito à conta especificada.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
