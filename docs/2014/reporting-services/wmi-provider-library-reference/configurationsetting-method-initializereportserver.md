---
title: Método InitializeReportServer (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- InitializeReportServer (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- InitializeReportServer method
ms.assetid: 0304acc2-1fd7-437b-94d9-1c1073dd3ca4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f5ea9e6e4e36e62828f3036c3765ba42c202448c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098352"
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
  
## <a name="remarks"></a>Comentários  
 Quando este método é chamado, a chave de criptografia que acessa as informações seguras do banco de dados do servidor de relatório é criptografada usando-se a chave pública do servidor de relatório identificada por *InstallationID*.  
  
 A chave pública do servidor de relatório especificada deve ter sido gravada previamente no banco de dados do servidor de relatório.  
  
 O método *InitializeReportServer* deve ser chamado em um servidor de relatório que já tenha acesso às informações seguras para que possa descriptografar a chave de criptografia. Em seguida, a chave de criptografia criptografada resultante é armazenada no banco de dados do servidor de relatório.  
  
 Se o servidor de relatório [IsInitialized](configurationsetting-property-isinitialized.md) estiver definida como `true` quando o método InitializeReportServer for chamado, o método retornará êxito sem tentar criptografar a chave de criptografia.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
