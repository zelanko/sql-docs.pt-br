---
title: Método ListSSLCertificates (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
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
- ListSSLCertificates method
ms.assetid: 88cd0936-b202-4ab8-90f2-d9c3f66d37f4
caps.latest.revision: 12
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 7f187fa6f3f99d476faada44639caa7e89b33750
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115636"
---
# <a name="listsslcertificates-method-wmi-msreportserverconfigurationsetting"></a>Método ListSSLCertificates (WMI MSReportServer_ConfigurationSetting)
  Retorna uma lista de certificados no computador do servidor de relatório.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub CreateSSLCertificateBinding (ByRef CertificateHash() as String, _  
    ByRef CertName() as String, ByRef HostName() as String, ByRef Length as Int32, _   
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListSSLCertificates(out string[] CertificateHash,   
    out string[] CertName, out string[] Hostname, out Int32 length,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *CertificateHash[]*  
 [fora] O certificado efetua hash.  
  
 *CertName[]*  
 [fora] Nomes do certificado.  
  
 *HostName[]*  
 [fora] Nomes de host dos certificados.  
  
 *Comprimento*  
 [out] Representa o comprimento das matrizes *CertificateHash*, *CertName* e *HostName* .  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método foi bem-sucedida; um código de erro indica que a chamada não foi bem-sucedida.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  