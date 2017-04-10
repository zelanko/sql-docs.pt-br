---
title: "Configurar propriedades de rela&#231;&#227;o de atributo | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "relações flexíveis (Analysis Services)"
  - "atributos [Analysis Services], relações"
  - "relações [Analysis Services], atributos"
  - "propriedades [Analysis Services], relações de atributos"
  - "relações rígidas (Analysis Services)"
ms.assetid: fce511af-66d7-42fc-bb3a-6c516f16b10e
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Configurar propriedades de rela&#231;&#227;o de atributo
  A tabela a seguir lista e descreve as propriedades de uma relação de atributo.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|Atributo|Contém o nome do atributo.|  
|Cardinalidade|Indica a cardinalidade da relação. Os valores são Many, para uma relação muitos para um, ou One, para uma relação um para um. O valor padrão é Many. No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a propriedade cardinality não tem nenhum efeito – seu uso é reservado para uma implementação futura.|  
|Nome|Contém o nome amigável do atributo.|  
|RelationshipType|Indica se relações de membro alteram com o passar do tempo. Os valores são Rigid, o que significa que as relações entre membros não muda com o passar do tempo, ou Flexible, o que significa que as relações entre os membros mudam. O padrão é Flexible. Se você definir uma relação como flexível, as agregações serão descartadas e recomputadas como parte de uma atualização incremental (elas não serão descartadas se apenas novos membros forem adicionados). Se você definir uma relação como rígida, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] manterá as agregações quando a dimensão for atualizada incrementalmente. Se uma relação que é definida como rígida mudar, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gerará um erro durante o processamento incremental. Ao especificar as relações apropriadas e as propriedades da relação, são produzidos aumento de consulta e desempenho de processamento.|  
|Visível|Determina a visibilidade da relação do atributo. Os valores são True ou False. O padrão é True.|  
  
  