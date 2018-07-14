---
title: Biblioteca de extensões do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- namespaces [Reporting Services]
- Reporting Services, extending
- extensions [Reporting Services], library
- library [Reporting Services]
ms.assetid: e8eff470-64d6-41c3-b98b-5ec916c121c3
caps.latest.revision: 33
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ea7edf14017fc8f382705397ce5bd5763b7c02bf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246416"
---
# <a name="reporting-services-extension-library"></a>Biblioteca de extensões do Reporting Services
  A biblioteca de extensões do Reporting Services é um conjunto de classes, interfaces e tipos de valores que são incluídos no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Essa biblioteca fornece acesso à funcionalidade do sistema e foi projetada para ser a base na qual os aplicativos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] podem ser usados para estender os componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="namespaces"></a>Namespaces  
 A biblioteca de extensão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece os namespaces a seguir.  
  
 <xref:Microsoft.ReportingServices.DataProcessing>  
 Contém classes e interfaces que permitem a criação de componentes que estendem a capacidade do processamento de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 <xref:Microsoft.ReportingServices.Interfaces>  
 Contém classes e interfaces que permitem a criação e o envio de notificações personalizadas para usuários por meio de suas próprias extensões de entrega e a criação de extensões de segurança personalizadas para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 `Microsoft.ReportingServices.ReportRendering`  
 Contém classes e interfaces que permitem a extensão dos recursos de renderização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Usando os membros desse namespace junto com os membros do namespace <xref:Microsoft.ReportingServices.Interfaces>, você pode criar suas próprias extensões de renderização personalizadas para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](reporting-services-extensions.md)  
  
  
