---
title: Método CreateSSLCertificateBinding (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- CreateSSLCertificateBinding
ms.assetid: 407d50e4-0a55-43cb-8ddf-2d82714071b1
caps.latest.revision: 14
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: ac698f790d9e47410901fddc9dc974d6fa8cf7ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010138"
---
# <a name="createsslcertificatebinding-method-wmi-msreportserverconfigurationsetting"></a>Método CreateSSLCertificateBinding (WMI MSReportServer_ConfigurationSetting)
  Cria uma associação de Certificado SSL.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub CreateSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void CreateSSLCertificateBinding(string application,   
    string certificateHash, string IPAddress, int Port,   
    int lcid, out string error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *Aplicativo*  
 O nome do aplicativo para o qual a associação de certificado deve ser criada.  
  
 *CertificateHash*  
 O hash para o certificado.  
  
 *EndereçoIP*  
 O endereço IP para o aplicativo.  
  
 *Porta*  
 A porta SSL relacionada à associação.  
  
 *Lcid*  
 A localidade a ser usada para as mensagens de erro retornadas.  
  
 *Erro*  
 [fora] A descrição dos erros ocorridos.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método foi bem-sucedida; um código de erro indica que a chamada não foi bem-sucedida.  
  
## <a name="remarks"></a>Remarks  
 Este método adiciona uma associação a rsreportserver.config para o aplicativo. Caso ainda não exista uma associação em HTTP.SYS, ela será criada ali.  
  
 Antes de criar a associação, a chamada do método examina as Reservas de Url referentes ao aplicativo especificado a fim de determinar se a Associação de Certificado SSL é válida.  
  
 As seguintes condições são validadas e podem resultar em erros:  
  
1.  O certificado não existe.  
  
2.  O valor IPAddress especificado não corresponde a um IPAddress deste computador.  
  
3.  O IPAddress especificado é um IPAddress DHCP (muda periodicamente) – no lugar dele, use o endereço IP Curinga (0.0.0.0).  
  
4.  O IPAddress especificado não corresponde ao endereço IP de uma reserva de URL, tampouco existe uma reserva de URL com nome de host ou curinga.  
  
5.  Uma reserva de URL que especifica que existe um nome de host, mas o nome de host não corresponde ao nome de host do certificado.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  