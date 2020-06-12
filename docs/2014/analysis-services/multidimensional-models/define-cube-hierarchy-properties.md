---
title: Definir propriedades de hierarquia de cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8903a49754357aad9cf24ee63fffa45fbf120e4d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546988"
---
# <a name="define-cube-hierarchy-properties"></a>Definir propriedades de hierarquia de cubo
  As propriedades de hierarquia de cubo permitem a especificação de configurações exclusivas para hierarquias definidas pelo usuário em dimensões de cubo com base na mesma dimensão do banco de dados. A tabela a seguir descreve as propriedades de uma hierarquia de cubo.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`Enabled`|Determina se a hierarquia está habilitada para a dimensão de cubo.|  
|`HierarchyID`|Contém o identificador exclusivo (ID) da hierarquia.|  
|`OptimizedState`|Determina o nível de otimização aplicado à hierarquia. Essa propriedade pode ter os seguintes valores:<br /><br /> `FullyOptimized`: a instância cria índices para a hierarquia a fim de melhorar o desempenho das consultas. Esse é o valor padrão.<br /><br /> `NotOptimized`: a instância não compila índices adicionais.|  
|`Visible`|Determina a visibilidade da hierarquia de cubo. O valor padrão é `True`.|  
  
## <a name="see-also"></a>Consulte Também  
 [Hierarquias do usuário](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
