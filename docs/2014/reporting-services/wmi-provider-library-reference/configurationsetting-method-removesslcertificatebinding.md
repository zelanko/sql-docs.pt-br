---
title: Método RemoveSSLCertificateBindings (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- RemoveSSLCertificateBindings method
ms.assetid: b8b484c9-04c4-4ae9-980e-67bbe5aa8481
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e479580d9d5b7720fe4fb7b641236ec12e4537c9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024238"
---
# <a name="removesslcertificatebindings-method-wmi-msreportserverconfigurationsetting"></a>Método RemoveSSLCertificateBindings (WMI MSReportServer_ConfigurationSetting)
  Remove uma associação de Certificado SSL.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub RemoveSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal Lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void RemoveSSLCertificateBindings(string Application,  
    string CertificateHash, string IPAddress, Int32 Port, Int32 Lcid,  
    out string Error, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *Aplicativo*  
 O nome do aplicativo para o qual a associação de certificado deve ser removida.  
  
 *CertificateHash*  
 O hash para o certificado.  
  
 *EndereçoIP*  
 O endereço IP para o aplicativo.  
  
 *Porta*  
 A porta SSL relacionada à associação.  
  
 *lcid*  
 A localidade a ser usada para as mensagens de erro retornadas.  
  
 *Erro*  
 [fora] A descrição do erro ocorrido.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método foi bem-sucedida; um código de erro indica que a chamada não foi bem-sucedida.  
  
## <a name="remarks"></a>Comentários  
 Este método remove a associação específica do arquivo rsreportserver.config e, opcionalmente, de HTTP.SYS.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
