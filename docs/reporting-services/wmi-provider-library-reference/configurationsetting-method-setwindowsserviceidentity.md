---
title: Método SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
caps.latest.revision: 19
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 45ceacca295b5ba6df2cb45f0386ed5bf50da70c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="configurationsetting-method---setwindowsserviceidentity"></a>Método de ConfigurationSetting – SetWindowsServiceIdentity
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
  
## <a name="remarks"></a>Remarks  
 Quando o parâmetro *UseBuiltInAccount* estiver definido como **true** e o servidor de relatório estiver em execução no Microsoft [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)] ou no Windows XP, os valores dos parâmetros *Name*, *Domain*e *Password* serão ignorados e a conta sistema Local será usada.  
  
 Quando o parâmetro *UseBuiltInAccount* estiver definido como **true** e o servidor de relatório estiver em execução no Windows Server 2003, as propriedades *Domain* e *Password* serão ignoradas e o campo de nome deverá conter “Builtin\NetworkService”, “Builtin\System” ou “Builtin\LocalService”.  
  
 O método SetWindowsServiceIdentity define as permissões de arquivo nos arquivos e nas pastas do diretório de instalação do servidor de relatório.  
  
 A conta especificada no parâmetro *Account* requer direitos de **LogonAsService** no Windows. O método concede esse direito à conta especificada.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
