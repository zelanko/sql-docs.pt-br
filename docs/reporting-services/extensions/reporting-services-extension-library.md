---
title: "Biblioteca do Reporting Services extensão | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- namespaces [Reporting Services]
- Reporting Services, extending
- extensions [Reporting Services], library
- library [Reporting Services]
ms.assetid: e8eff470-64d6-41c3-b98b-5ec916c121c3
caps.latest.revision: 33
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b9a1ce1e388575d6d5b9b46a00dbc85ae8cde84b
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="reporting-services-extension-library"></a>Biblioteca de extensões do Reporting Services
  A biblioteca de extensões do Reporting Services é um conjunto de classes, interfaces e tipos de valores que são incluídos no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esta biblioteca fornece acesso à funcionalidade do sistema e é projetada para ser a base de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] aplicativos podem ser usados para estender [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] componentes.  
  
## <a name="namespaces"></a>Namespaces  
 A biblioteca de extensão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece os namespaces a seguir.  
  
 <xref:Microsoft.ReportingServices.DataProcessing>  
 Contém classes e interfaces que permitem a criação de componentes que estendem a capacidade do processamento de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 <xref:Microsoft.ReportingServices.Interfaces>  
 Contém classes e interfaces que permitem a criação e o envio de notificações personalizadas para usuários por meio de suas próprias extensões de entrega e a criação de extensões de segurança personalizadas para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 **Microsoft.ReportingServices.ReportRendering**  
 Contém classes e interfaces que permitem a extensão dos recursos de renderização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Usando os membros desse namespace junto com os membros do namespace <xref:Microsoft.ReportingServices.Interfaces>, você pode criar suas próprias extensões de renderização personalizadas para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../reporting-services/extensions/reporting-services-extensions.md)  
  
  
