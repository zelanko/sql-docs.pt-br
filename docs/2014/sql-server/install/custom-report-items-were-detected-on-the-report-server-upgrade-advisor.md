---
title: Itens de relatório personalizado detectados no servidor de relatório (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- custom report items, upgrading
ms.assetid: aee32006-65b2-4dfe-9570-d85a249d17b2
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c971c8e19c6881cdc172a4e5c29952a1f829912a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48170756"
---
# <a name="custom-report-items-were-detected-on-the-report-server-upgrade-advisor"></a>Itens de relatório personalizado detectados no servidor de relatório (Supervisor de Atualização)
  Itens de relatório personalizados que foram criados para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não são compatíveis com [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. A atualização pode continuar, mas os relatórios que usam o item de relatório personalizado não serão executados como esperado. O Supervisor de Atualização detectou itens de relatório personalizados. A atualização pode prosseguir, mas você deverá mover os arquivos de item de relatório personalizado manualmente para a nova pasta de instalação ao final da atualização.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 O Supervisor de Atualização detectou configurações de extensão personalizadas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em arquivos de configuração, indicando que sua instalação inclui um ou mais assemblies personalizados para relatórios.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Concluída a atualização, mova os arquivos de item de relatório personalizado manualmente para a nova pasta de instalação.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
