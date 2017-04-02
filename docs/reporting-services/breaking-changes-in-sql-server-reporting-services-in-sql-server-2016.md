---
title: "Altera&#231;&#245;es recentes do SQL Server Reporting Services no SQL Server 2016 | Microsoft Docs"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Me.Value references"
  - "Reporting Services, backward compatibility"
  - "alterações recentes [Reporting Services]"
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
caps.latest.revision: 121
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 116
---
# Altera&#231;&#245;es recentes do SQL Server Reporting Services no SQL Server 2016
  Este tópico descreve as alterações recentes no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Você pode encontrar esses problemas durante a atualização ou em scripts ou relatórios personalizados.  
  
  ## Extensões de Segurança
  
  As extensões de segurança personalizadas precisam de algumas modificações para funcionar com o novo [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. As extensões de segurança precisam usar a interface IAuthenticationExtension2.
  
  ## Provedor WMI
  
  O nome do aplicativo [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] foi alterado de “ReportManager” para “ReportServerWebApp”.
  
## Consulte também  
 [Alterações de comportamento do SQL Server Reporting Services no SQL Server 2016](http://msdn.microsoft.com/pt-br/2a767f0f-84f2-4099-8784-1e37790f858e)   
 [Novidades no Reporting Services &#40;SSRS&#41;](../Topic/What's%20New%20in%20Reporting%20Services%20\(SSRS\).md)   
 [Recursos preteridos do SQL Server Reporting Services no SQL Server 2016](http://msdn.microsoft.com/pt-br/3876c01e-f81d-4cce-9104-5106a8c369e6)   
 [Funcionalidade descontinuada do SQL Server Reporting Services no SQL Server 2016](http://msdn.microsoft.com/pt-br/d529cc96-3483-480b-9bfc-bd28b1d0ef52)  
  
  