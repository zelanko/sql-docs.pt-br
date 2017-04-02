---
title: "M&#233;todo RemoveUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
apiname: 
  - "RemoveUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting Class)"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "Método RemoveUnattendedExecutionAccount"
ms.assetid: 77e371c1-7c26-44f9-9119-7c8dc838db32
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo RemoveUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting)
  Exclui a entrada de conta de execução autônoma do arquivo de configuração do servidor de relatório.  
  
## Sintaxe  
  
```vb  
Public Sub RemoveUnattendedExecutionAccount(ByRef HRESULT as Int32)  
```  
  
```csharp  
public void RemoveUnattendedExecutionAccount (out Int32 HRESULT);  
```  
  
## Parâmetros  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## Requisitos  
 **Namespace: ** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  