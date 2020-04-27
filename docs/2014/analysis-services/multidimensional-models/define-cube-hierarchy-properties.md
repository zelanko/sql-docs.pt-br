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
manager: craigg
ms.openlocfilehash: 0ace708cc4ee09295380b814bbf21f5a1c350974
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66075712"
---
# <a name="define-cube-hierarchy-properties"></a>Definir propriedades de hierarquia de cubo
  As propriedades de hierarquia de cubo permitem a especificação de configurações exclusivas para hierarquias definidas pelo usuário em dimensões de cubo com base na mesma dimensão do banco de dados. A tabela a seguir descreve as propriedades de uma hierarquia de cubo.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`Enabled`|Determina se a hierarquia está habilitada para a dimensão de cubo.|  
|`HierarchyID`|Contém o identificador exclusivo (ID) da hierarquia.|  
|`OptimizedState`|Determina o nível de otimização aplicado à hierarquia. Essa propriedade pode ter os seguintes valores:<br /><br /> `FullyOptimized`: a instância cria índices para a hierarquia a fim de melhorar o desempenho das consultas. Este é o valor padrão.<br /><br /> `NotOptimized`: a instância não compila índices adicionais.|  
|`Visible`|Determina a visibilidade da hierarquia de cubo. O valor padrão é `True`.|  
  
## <a name="see-also"></a>Consulte Também  
 [Hierarquias do usuário](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
