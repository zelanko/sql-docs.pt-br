---
title: "Propriedade IsSharePointIntegrated (WMI MSReportServer_Instance) | Microsoft Docs"
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
  - "Propriedade IsSharePointIntegrated"
ms.assetid: e21d00ad-5d9a-4290-8d74-7eeeda39e1ed
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Propriedade IsSharePointIntegrated (WMI MSReportServer_Instance)
  Especifica se o servidor de relatório está no modo integrado do SharePoint. A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], essa propriedade sempre retorna **Falso** porque, no modo do SharePoint, as instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são serviços compartilhados do SharePoint e não são controladas por provedores WMI.  
  
## Sintaxe  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## Valores da propriedade  
 Um objeto **Boolean** que indica se o servidor de relatório está no modo integrado do SharePoint.  
  
## Requisitos  
 **Namespace: ** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## Consulte também  
 [Membros MSReportServer_Instance](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-members.md)   
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  