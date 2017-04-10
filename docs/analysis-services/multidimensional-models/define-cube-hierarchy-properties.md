---
title: "Definir propriedades de hierarquia de cubo | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
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
  - "hierarquias [Analysis Services], multinível"
  - "hierarquias [Analysis Services], cubos"
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 18
---
# Definir propriedades de hierarquia de cubo
  As propriedades de hierarquia de cubo permitem a especificação de configurações exclusivas para hierarquias definidas pelo usuário em dimensões de cubo com base na mesma dimensão do banco de dados. A tabela a seguir descreve as propriedades de uma hierarquia de cubo.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**Ativado**|Determina se a hierarquia está habilitada para a dimensão de cubo.|  
|**HierarchyID**|Contém o identificador exclusivo (ID) da hierarquia.|  
|**OptimizedState**|Determina o nível de otimização aplicado à hierarquia. Essa propriedade pode ter os seguintes valores:<br /><br /> **FullyOptimized**:<br />                    A instância cria índices para a hierarquia a fim de melhorar o desempenho das consultas. Este é o valor padrão.<br /><br /> **NotOptimized**:<br />                    A instância não cria índices adicionais.|  
|**Visível**|Determina a visibilidade da hierarquia de cubo. O valor padrão é **True**.|  
  
## Consulte também  
 [Hierarquias do usuário](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  