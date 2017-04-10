---
title: "Propriedade DatabaseLogonType (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
apiname: 
  - "DatabaseLogonType"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "Propriedade DatabaseLogonType"
ms.assetid: 6b592582-4c35-4029-ab86-982fff47d8d6
caps.latest.revision: 24
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Propriedade DatabaseLogonType (WMI MSReportServer_ConfigurationSetting)
  Especifica se o servidor de relatório usa uma conta de serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, uma conta do usuário do Windows ou um logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para acessar o banco de dados do servidor de relatório. Somente leitura.  
  
## Sintaxe  
  
```vb  
Public Dim DatabaseLogonType As Integer  
```  
  
```csharp  
public int DatabaseLogonType;  
```  
  
## Valores da propriedade  
 Um objeto **integer** que representa o tipo de logon.  
  
## Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## Comentários  
 Os valores são:  
  
-   0 para logon do Windows  
  
-   1 para logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 para fazer logon como um serviço  
  
 Se você especificar 0 (Windows), deverá definir o valor na propriedade [DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/databaselogonaccount-property-wmi-msreportserver-configurationsetting.md) com uma conta de usuário válida e correspondente do Windows.  
  
 Se especificar 1 (SQL Server), certifique-se de que o valor de [DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/databaselogonaccount-property-wmi-msreportserver-configurationsetting.md) corresponda a um logon válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se você especificar 2 (serviço Windows), o servidor de relatório usará uma conta [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] e a conta de serviço do Windows para acessar o banco de dados do servidor de relatório. A propriedade DatabaseLogonAccount é ignorada.  
  
## Requisitos  
 **Namespace: ** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  