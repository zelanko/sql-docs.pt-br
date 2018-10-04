---
title: Definir propriedades de hierarquia de cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b064db7ff0e496ea7a46085825afc202fced605
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087316"
---
# <a name="define-cube-hierarchy-properties"></a>Definir propriedades de hierarquia de cubo
  As propriedades de hierarquia de cubo permitem a especificação de configurações exclusivas para hierarquias definidas pelo usuário em dimensões de cubo com base na mesma dimensão do banco de dados. A tabela a seguir descreve as propriedades de uma hierarquia de cubo.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|`Enabled`|Determina se a hierarquia está habilitada para a dimensão de cubo.|  
|`HierarchyID`|Contém o identificador exclusivo (ID) da hierarquia.|  
|`OptimizedState`|Determina o nível de otimização aplicado à hierarquia. Essa propriedade pode ter os seguintes valores:<br /><br /> `FullyOptimized`: A instância cria índices para a hierarquia melhorar o desempenho da consulta. Este é o valor padrão.<br /><br /> `NotOptimized`: A instância não compila índices adicionais.|  
|`Visible`|Determina a visibilidade da hierarquia de cubo. O valor padrão é `True`.|  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquias de usuário](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
