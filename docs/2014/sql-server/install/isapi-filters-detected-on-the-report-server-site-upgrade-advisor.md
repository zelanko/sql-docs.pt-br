---
title: Filtros ISAPI detectados no site do servidor de relatório (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ISAPI filters
- report servers [Reporting Services], upgrade issues
ms.assetid: dd30560d-9e16-47c7-ba68-a9743a657e4e
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 18a9aab0737cb6d5127bbb3357d307c9c8f03aef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117075"
---
# <a name="isapi-filters-detected-on-the-report-server-site-upgrade-advisor"></a>Filtros ISAPI detectados no site do servidor de relatório (Supervisor de Atualização)
  O Supervisor de Atualização detectou um ou mais filtros ISAPI no site que hospeda o servidor de relatório e os diretórios virtuais do Gerenciador de Relatórios. Não há suporte para filtros ISAPI no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Nativo.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 Antes da atualização, verifique se os filtros ISAPI do site são usados por aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se você não precisar do filtro ISAPI, poderá atualizar o servidor de relatório. A Instalação criará URLs padrão sem suporte para o filtro ISAPI executado no IIS. Se precisar do filtro ISAPI, não faça a atualização até encontrar uma maneira alternativa de hospedar o filtro ISAPI (por exemplo, usando o ISA Server ou continuando a hospedar o filtro ISAPI no IIS). O servidor de relatório suporta o ASP.NET HTTPModules como substituto dos filtros ISAPI em certos cenários. Para obter mais informações, consulte a documentação do ASP.NET sobre MSDN.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Avalie e use uma solução separada para hospedar filtros ISAPI necessários para sua implantação.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  