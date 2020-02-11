---
title: Foram detectados itens de relatório personalizados no servidor de relatório (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- custom report items, upgrading
ms.assetid: aee32006-65b2-4dfe-9570-d85a249d17b2
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 5788b94356ec887b8c83850a4cb2c47d34b7388f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952279"
---
# <a name="custom-report-items-were-detected-on-the-report-server-upgrade-advisor"></a>Itens de relatório personalizado detectados no servidor de relatório (Supervisor de Atualização)
  Os itens de relatório personalizados que foram criados para versões [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anteriores do não são [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]compatíveis com o. A atualização pode continuar, mas os relatórios que usam o item de relatório personalizado não serão executados como esperado. O Supervisor de Atualização detectou itens de relatório personalizados. A atualização pode prosseguir, mas você deverá mover os arquivos de item de relatório personalizado manualmente para a nova pasta de instalação ao final da atualização.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>DESCRIÇÃO  
 O Supervisor de Atualização detectou configurações de extensão personalizadas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em arquivos de configuração, indicando que sua instalação inclui um ou mais assemblies personalizados para relatórios.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Concluída a atualização, mova os arquivos de item de relatório personalizado manualmente para a nova pasta de instalação.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Reporting Services &#40;o supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
