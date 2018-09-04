---
title: Método InitializeReportServer (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
apiname:
- InitializeReportServer (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- InitializeReportServer method
ms.assetid: 0304acc2-1fd7-437b-94d9-1c1073dd3ca4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e0cc3282b495267c0023925888ad639a22348b21
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43268518"
---
# <a name="configurationsetting-method---initializereportserver"></a>Método de ConfigurationSetting – InitializeReportServer
  Inicializa a instância do serviço de relatório especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub InitializeReportServer(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void InitializeReportServer(string InstallationID,   
    out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *InstallationID*  
 Uma cadeia de caracteres usada para criptografar a chave de criptografia antes de ela ser retornada.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
 *ExtendedErrors[]*  
 [fora] Uma matriz de cadeia de caracteres que contém erros adicionais retornados pela chamada.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Remarks  
 Quando este método é chamado, a chave de criptografia que acessa as informações seguras do banco de dados do servidor de relatório é criptografada usando-se a chave pública do servidor de relatório identificada por *InstallationID*.  
  
 A chave pública do servidor de relatório especificada deve ter sido gravada previamente no banco de dados do servidor de relatório.  
  
 O método *InitializeReportServer* deve ser chamado em um servidor de relatório que já tenha acesso às informações seguras para que possa descriptografar a chave de criptografia. Em seguida, a chave de criptografia criptografada resultante é armazenada no banco de dados do servidor de relatório.  
  
 Se a propriedade [IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md) do servidor de relatório for definida como **true** quando o método InitializeReportServer for chamado, o método terá êxito sem tentar criptografar a chave de criptografia.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
