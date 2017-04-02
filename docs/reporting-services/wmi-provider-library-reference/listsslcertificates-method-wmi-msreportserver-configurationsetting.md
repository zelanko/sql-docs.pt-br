---
title: "M&#233;todo ListSSLCertificates (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Método ListSSLCertificates"
ms.assetid: 88cd0936-b202-4ab8-90f2-d9c3f66d37f4
caps.latest.revision: 12
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo ListSSLCertificates (WMI MSReportServer_ConfigurationSetting)
  Retorna uma lista de certificados no computador do servidor de relatório.  
  
## Sintaxe  
  
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
  
## Parâmetros  
 *CertificateHash[]*  
 [fora] O certificado efetua hash.  
  
 *CertName[]*  
 [fora] Nomes do certificado.  
  
 *HostName[]*  
 [fora] Nomes de host dos certificados.  
  
 *Comprimento*  
 [out] Representa o comprimento das matrizes *CertificateHash*, *CertName* e *HostName*.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método foi bem-sucedida; um código de erro indica que a chamada não foi bem-sucedida.  
  
## Comentários  
  
## Requisitos  
 **Namespace: ** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  