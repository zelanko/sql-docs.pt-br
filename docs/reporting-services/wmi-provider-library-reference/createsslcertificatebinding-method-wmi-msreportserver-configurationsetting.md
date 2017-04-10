---
title: "M&#233;todo CreateSSLCertificateBinding (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "CreateSSLCertificateBinding"
ms.assetid: 407d50e4-0a55-43cb-8ddf-2d82714071b1
caps.latest.revision: 14
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo CreateSSLCertificateBinding (WMI MSReportServer_ConfigurationSetting)
  Cria uma associação de Certificado SSL.  
  
## Sintaxe  
  
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
  
## Parâmetros  
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
  
## Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método foi bem-sucedida; um código de erro indica que a chamada não foi bem-sucedida.  
  
## Comentários  
 Este método adiciona uma associação a rsreportserver.config para o aplicativo. Caso ainda não exista uma associação em HTTP.SYS, ela será criada ali.  
  
 Antes de criar a associação, a chamada do método examina as Reservas de Url referentes ao aplicativo especificado a fim de determinar se a Associação de Certificado SSL é válida.  
  
 As seguintes condições são validadas e podem resultar em erros:  
  
1.  O certificado não existe.  
  
2.  O valor IPAddress especificado não corresponde a um IPAddress deste computador.  
  
3.  O IPAddress especificado é um IPAddress DHCP (muda periodicamente) – no lugar dele, use o endereço IP Curinga (0.0.0.0).  
  
4.  O IPAddress especificado não corresponde ao endereço IP de uma reserva de URL, tampouco existe uma reserva de URL com nome de host ou curinga.  
  
5.  Uma reserva de URL que especifica que existe um nome de host, mas o nome de host não corresponde ao nome de host do certificado.  
  
## Requisitos  
 **Namespace: ** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  