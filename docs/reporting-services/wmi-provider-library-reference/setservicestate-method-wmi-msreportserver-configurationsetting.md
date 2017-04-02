---
title: "M&#233;todo SetServiceState (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "SetServiceState (WMI MSReportServer_ConfigurationSetting Class)"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "Método SetServiceState"
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
caps.latest.revision: 20
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo SetServiceState (WMI MSReportServer_ConfigurationSetting)
  Ativa e desativa o Servidor de Relatório do Windows e os serviços Web.  
  
## Sintaxe  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## Parâmetros  
 *EnableWindowsService*  
 Um valor **Boolean** que indica o estado do serviço Windows. Um valor **true** inicia o serviço Servidor de Relatório do Windows; um valor **false** interrompe o serviço do Windows.  
  
 *EnableWebService*  
 Um valor **Boolean** que indica o estado do serviço Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Um valor **true** inicia o serviço Web Servidor de Relatórios; um valor **false** interrompe o serviço Web.  
  
 *EnableReportManager*  
 Um valor **Boolean** que indica o estado desejado do Gerenciador de Relatórios.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## Comentários  
  
## Requisitos  
 **Namespace: ** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  