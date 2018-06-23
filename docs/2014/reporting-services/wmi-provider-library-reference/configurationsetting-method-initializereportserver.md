---
title: Método InitializeReportServer (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- InitializeReportServer (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- InitializeReportServer method
ms.assetid: 0304acc2-1fd7-437b-94d9-1c1073dd3ca4
caps.latest.revision: 20
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: e5c3ace1e9e4cb25fde4d836bc15ad9f30eee3e2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020192"
---
# <a name="initializereportserver-method-wmi-msreportserverconfigurationsetting"></a>Método InitializeReportServer (WMI MSReportServer_ConfigurationSetting)
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
  
 Se o servidor de relatório [IsInitialized](configurationsetting-property-isinitialized.md) está definida como `true` quando o método InitializeReportServer é chamado, o método terá êxito sem tentar criptografar a chave de criptografia.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  