---
title: Configurar propriedades de relação de atributo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9a7270dd698dfb8d3d3002c302186e97b912044f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="attribute-relationships---configure-attribute-properties"></a>Relações de atributo - configurar as propriedades de atributo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  A tabela a seguir lista e descreve as propriedades de uma relação de atributo.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|Atributo|Contém o nome do atributo.|  
|Cardinalidade|Indica a cardinalidade da relação. Os valores são Many, para uma relação muitos para um, ou One, para uma relação um para um. O valor padrão é Many. No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a propriedade cardinality não tem nenhum efeito – seu uso é reservado para uma implementação futura.|  
|Nome|Contém o nome amigável do atributo.|  
|RelationshipType|Indica se relações de membro alteram com o passar do tempo. Os valores são Rigid, o que significa que as relações entre membros não muda com o passar do tempo, ou Flexible, o que significa que as relações entre os membros mudam. O padrão é Flexible. Se você definir uma relação como flexível, as agregações serão descartadas e recomputadas como parte de uma atualização incremental (elas não serão descartadas se apenas novos membros forem adicionados). Se você definir uma relação como rígida, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] manterá as agregações quando a dimensão for atualizada incrementalmente. Se uma relação que é definida como rígida mudar, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gerará um erro durante o processamento incremental. Ao especificar as relações apropriadas e as propriedades da relação, são produzidos aumento de consulta e desempenho de processamento.|  
|Visível|Determina a visibilidade da relação do atributo. Os valores são True ou False. O padrão é True.|  
  
  
