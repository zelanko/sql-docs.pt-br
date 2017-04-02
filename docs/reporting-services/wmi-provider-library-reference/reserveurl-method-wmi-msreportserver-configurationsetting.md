---
title: "M&#233;todo ReserveURL (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "Método ReservedURL"
ms.assetid: b9008a62-3edd-4f8a-99f2-7598c2133899
caps.latest.revision: 14
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo ReserveURL (WMI MSReportServer_ConfigurationSetting)
  Adiciona uma reserva de URL para um determinado aplicativo.  
  
## Sintaxe  
  
```vb  
Public Sub ReserveURL(Application as String, _  
    UrlString as String, Lcid as Int32, _   
    ByRef [Error] as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ReserveURL(string Application, string UrlString, int Lcid,   
    out string error, out int HRESULT);  
```  
  
## Parâmetros  
 *Aplicativo*  
 O nome do aplicativo para o qual reservar a URL.  
  
 *URLString*  
 A URL para a reserva.  
  
 *lcid*  
 A localidade a ser usada para as mensagens de erro retornadas.  
  
 *Erro*  
 [fora] A descrição do erro ocorrido.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método foi bem-sucedida; um código de erro indica que a chamada não foi bem-sucedida.  
  
## Comentários  
 *UrlString* não inclui o nome do diretório virtual. O método [SetVirtualDirectory](../../reporting-services/wmi-provider-library-reference/setvirtualdirectory-method-wmi-msreportserver-configurationsetting.md) é disponibilizado para essa finalidade.  
  
 As reservas de URL são criadas para a conta atual de serviço do Windows. Para alterar a conta de serviço do Windows, é necessário atualizar todas as reservas de URL manualmente.  
  
 Este método faz com que todos os domínios de aplicativo façam uma reciclagem agressiva. Os domínios de aplicativo são reiniciados após o término desta operação.  
  
## Requisitos  
 **Namespace: ** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  