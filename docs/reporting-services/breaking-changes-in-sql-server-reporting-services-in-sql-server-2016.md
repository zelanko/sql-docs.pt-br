---
title: "Alterações recentes no SQL Server Reporting Services no SQL Server 2016 | Microsoft Docs"
ms.date: 07/02/2017
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
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 6348d05b8dbe6c8ab1a682388b4e69ce438e6a12
ms.contentlocale: pt-br
ms.lasthandoff: 07/03/2017

---

# Alterações recentes do SQL Server Reporting Services no SQL Server 2016
<a id="breaking-changes-in-sql-server-reporting-services-in-sql-server-2016" class="xliff"></a>

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

Este tópico descreve as alterações recentes no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Você pode encontrar esses problemas durante a atualização ou em scripts ou relatórios personalizados.

## Extensões de Segurança
<a id="security-extensions" class="xliff"></a>

As extensões de segurança personalizadas precisam de algumas modificações para funcionar com o novo [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. As extensões de segurança precisam usar a interface IAuthenticationExtension2.

## Provedor WMI
<a id="wmi-provider" class="xliff"></a>

O nome do aplicativo [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] foi alterado de “ReportManager” para “ReportServerWebApp”.

## Próximas etapas
<a id="next-steps" class="xliff"></a>

[Alterações de comportamento no SQL Server Reporting Services no SQL Server 2016](../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)  
[Novidades no Reporting Services (SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)   
[Recursos preteridos no SQL Server Reporting Services no SQL Server 2016](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)    
[Funcionalidade descontinuada do SQL Server Reporting Services no SQL Server 2016](../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
