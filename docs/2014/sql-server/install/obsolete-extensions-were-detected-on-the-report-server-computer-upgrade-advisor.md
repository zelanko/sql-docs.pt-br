---
title: Extensões obsoletas detectadas no computador do servidor de relatório (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 40d245a2-0631-470e-81b3-1feb47e028cb
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c29365b40d59d76ab65d8f9f40a3bec86a0b486f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37328977"
---
# <a name="obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor"></a>Extensões obsoletas detectadas no computador do servidor de relatório (Supervisor de Atualização)
  O Supervisor de Atualização detectou uma ou mais extensões de renderização que não estão mais disponíveis na versão atual.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 O servidor de relatório está configurado para usar uma ou mais extensões que foram descontinuadas nesta versão. As extensões descontinuadas incluem:  
  
-   Extensão de renderização HTML OWC  
  
-   Extensão de renderização 3,2 HTML  
  
 A atualização pode continuar, mas a funcionalidade sem suporte não estará mais disponível no servidor de relatório atualizado.  
  
 Se você precisar dessas extensões, não faça a atualização antes de encontrar uma outra solução para esses requisitos. Talvez seja necessário obter ou criar uma extensão de renderização personalizada que forneça funcionalidade igual ou similar.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Avalie o conjunto atual de recursos incluídos no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para determinar se a funcionalidade suportada satisfaz suas necessidades.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
