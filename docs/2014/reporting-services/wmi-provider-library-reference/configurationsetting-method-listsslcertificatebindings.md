---
title: Método ListSSLCertificateBindings (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListSSLCertificateBindings method
ms.assetid: d12d280c-9b6f-47a8-bcd9-34cde31c8886
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0a2a33d7aa992fd434b29fd519c805f57b2b46fc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098356"
---
# <a name="listsslcertificatebindings-method-wmi-msreportserverconfigurationsetting"></a>Método ListSSLCertificateBindings (WMI MSReportServer_ConfigurationSetting)
  Retorna uma lista de certificados SSL instalados no computador.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub ListSSLCertificateBindings(ByVal LCID As Int32, ByRef Application() As String, _  
    ByRef CertificateHash() As String, ByRef IPAddresses() As String, ByRef Port() As Int32, _  
    ByRef Errors() As String, ByRef Length As Int32, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListSSLCertificateBindings(Int32 Lcid, out string[] Application,   
    out string[] CertificateHash,out string[] IPAddress,   
    out Int32[] Port, out string Errors,   
    out Int32 length, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *LCID*  
 A localidade a ser usada para as mensagens de erro retornadas.  
  
 *Application[]*  
 [fora] Os aplicativos que têm associações de certificado.  
  
 *CertificateHash[]*  
 [fora] Os hashes dos certificados.  
  
 *IPAddress[]*  
 [fora] O endereço IP dos aplicativos.  
  
 *Port[]*  
 [fora] O número de porta armazenado na associação em rsreportserver.config.  
  
 *Errors[]*  
 [fora] As descrições dos erros ocorridos.  
  
 *Comprimento*  
 [fora] O tamanho da matriz retornada pelo método.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
