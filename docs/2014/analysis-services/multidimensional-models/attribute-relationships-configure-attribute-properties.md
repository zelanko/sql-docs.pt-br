---
title: Configurar propriedades de relação de atributo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- flexible relationships (Analysis Services)
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
- properties [Analysis Services], attribute relationships
- rigid relationships (Analysis Services)
ms.assetid: fce511af-66d7-42fc-bb3a-6c516f16b10e
author: minewiskan
ms.author: owend
ms.openlocfilehash: 241fa2af16377fd2cacf657ec6f99c5ca4bd0c53
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544698"
---
# <a name="configure-attribute-relationship-properties"></a>Configurar propriedades de relação de atributo
  A tabela a seguir lista e descreve as propriedades de uma relação de atributo.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|Atributo|Contém o nome do atributo.|  
|Cardinalidade|Indica a cardinalidade da relação. Os valores são Many, para uma relação muitos para um, ou One, para uma relação um para um. O valor padrão é Many. No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , a propriedade cardinalidade não tem nenhum efeito – seu uso é reservado para uma implementação futura.|  
|Name|Contém o nome amigável do atributo.|  
|RelationshipType|Indica se relações de membro alteram com o passar do tempo. Os valores são Rigid, o que significa que as relações entre membros não muda com o passar do tempo, ou Flexible, o que significa que as relações entre os membros mudam. O padrão é Flexible. Se você definir uma relação como flexível, as agregações serão descartadas e recomputadas como parte de uma atualização incremental (elas não serão descartadas se apenas novos membros forem adicionados). Se você definir uma relação como rígida, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] manterá as agregações quando a dimensão for atualizada incrementalmente. Se uma relação que é definida como rígida mudar, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gerará um erro durante o processamento incremental. Ao especificar as relações apropriadas e as propriedades da relação, são produzidos aumento de consulta e desempenho de processamento.|  
|Visible|Determina a visibilidade da relação do atributo. Os valores são True ou False. O padrão é True.|  
  
  
