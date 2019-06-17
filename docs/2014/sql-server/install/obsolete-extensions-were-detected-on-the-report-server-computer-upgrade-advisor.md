---
title: Extensões obsoletas detectadas no computador do servidor de relatório (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 40d245a2-0631-470e-81b3-1feb47e028cb
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 93a971b82fa4bafd1d8fb51a148b7e488c7d6d20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093812"
---
# <a name="obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor"></a>Extensões obsoletas detectadas no computador do servidor de relatório (Supervisor de Atualização)
  O Supervisor de Atualização detectou uma ou mais extensões de renderização que não estão mais disponíveis na versão atual.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 O servidor de relatório está configurado para usar uma ou mais extensões que foram descontinuadas nesta versão. As extensões descontinuadas incluem:  
  
-   Extensão de renderização HTML OWC  
  
-   Extensão de renderização 3,2 HTML  
  
 A atualização pode continuar, mas a funcionalidade sem suporte não estará mais disponível no servidor de relatório atualizado.  
  
 Se você precisar dessas extensões, não faça a atualização antes de encontrar uma outra solução para esses requisitos. Talvez seja necessário obter ou criar uma extensão de renderização personalizada que forneça funcionalidade igual ou similar.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Avalie o conjunto atual de recursos incluídos no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para determinar se a funcionalidade suportada satisfaz suas necessidades.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
