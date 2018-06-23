---
title: Definir propriedades de hierarquia de cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 199e00331e26cea5c84242582f9c6382215ad411
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006740"
---
# <a name="define-cube-hierarchy-properties"></a>Definir propriedades de hierarquia de cubo
  As propriedades de hierarquia de cubo permitem a especificação de configurações exclusivas para hierarquias definidas pelo usuário em dimensões de cubo com base na mesma dimensão do banco de dados. A tabela a seguir descreve as propriedades de uma hierarquia de cubo.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|`Enabled`|Determina se a hierarquia está habilitada para a dimensão de cubo.|  
|`HierarchyID`|Contém o identificador exclusivo (ID) da hierarquia.|  
|`OptimizedState`|Determina o nível de otimização aplicado à hierarquia. Essa propriedade pode ter os seguintes valores:<br /><br /> `FullyOptimized`: A instância cria índices para a hierarquia melhorar o desempenho da consulta. Este é o valor padrão.<br /><br /> `NotOptimized`: A instância não cria índices adicionais.|  
|`Visible`|Determina a visibilidade da hierarquia de cubo. O valor padrão é `True`.|  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquias de usuário](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  