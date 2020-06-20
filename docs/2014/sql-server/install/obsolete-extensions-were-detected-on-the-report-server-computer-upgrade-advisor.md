---
title: Extensões obsoletas foram detectadas no computador do servidor de relatório (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 40d245a2-0631-470e-81b3-1feb47e028cb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5fa59ce825a8731997cc905db636f40dcd7964e8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012152"
---
# <a name="obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor"></a>Extensões obsoletas detectadas no computador do servidor de relatório (Supervisor de Atualização)
  O Supervisor de Atualização detectou uma ou mais extensões de renderização que não estão mais disponíveis na versão atual.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 O servidor de relatório está configurado para usar uma ou mais extensões que foram descontinuadas nesta versão. As extensões descontinuadas incluem:  
  
-   Extensão de renderização do OWC HTML  
  
-   Extensão de renderização HTML 3,2  
  
 A atualização pode continuar, mas a funcionalidade sem suporte não estará mais disponível no servidor de relatório atualizado.  
  
 Se você precisar dessas extensões, não faça a atualização antes de encontrar uma outra solução para esses requisitos. Talvez seja necessário obter ou criar uma extensão de renderização personalizada que forneça funcionalidade igual ou similar.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Avalie o conjunto atual de recursos incluídos no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para determinar se a funcionalidade suportada satisfaz suas necessidades.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Reporting Services &#40;o supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
