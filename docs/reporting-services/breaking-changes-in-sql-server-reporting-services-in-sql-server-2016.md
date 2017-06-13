---
title: "Alterações recentes no SQL Server Reporting Services no SQL Server 2016 | Microsoft Docs"
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
caps.latest.revision: 121
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 36ec7d7f1aa78e08f7fa4b63e8ca6525afe1c215
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2016"></a>Alterações recentes do SQL Server Reporting Services no SQL Server 2016
  Este tópico descreve as alterações recentes no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Você pode encontrar esses problemas durante a atualização ou em scripts ou relatórios personalizados.  
  
  ## <a name="security-extensions"></a>Extensões de Segurança
  
  As extensões de segurança personalizadas precisam de algumas modificações para funcionar com o novo [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. As extensões de segurança precisam usar a interface IAuthenticationExtension2.
  
  ## <a name="wmi-provider"></a>Provedor WMI
  
  O nome do aplicativo [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] foi alterado de “ReportManager” para “ReportServerWebApp”.
  
## <a name="see-also"></a>Consulte também 

[Alterações de comportamento no SQL Server Reporting Services no SQL Server 2016](../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)

[Novidades no Reporting Services (SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)
 
[Recursos preteridos do SQL Server Reporting Services no SQL Server 2016](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)
  
[Funcionalidade descontinuada do SQL Server Reporting Services no SQL Server 2016](../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)



