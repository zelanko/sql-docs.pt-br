---
title: Modificando dados (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying data [MDX]
- Multidimensional Expressions [Analysis Services], data modifications
- MDX [Analysis Services], data modifications
- data modifications [MDX]
ms.assetid: 363b662c-b839-4971-bbd7-1842f73ce141
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2f703f4f86c7c16118026ff2209bf0a1e35c8d3a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-data-modification---modifying-data"></a>Modificação de dados MDX - modificando dados
  Além de usar a linguagem MDX para recuperar e manipular dados de dimensões e cubos, você pode usá-la para atualizar ou executar *write-back* de dados de dimensão e de cubo. Essas atualizações podem ser temporárias, como na análise teórica (ou"what if"), ou permanentes, como quando alterações devem ser feitas com base na análise dos dados.  
  
 As atualizações de dados podem ocorrer no nível de dimensão ou de cubo:  
  
 **Write-backs de dimensão**  
 Use a [Instrução ALTER CUBE (MDX)](../../../mdx/mdx-data-definition-alter-cube.md) para alterar os dados de uma dimensão habilitada para gravação e a [Instrução REFRESH CUBE (MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) para refletir a exclusão, criação e atualização de valores de atributo. Você também pode usar a instrução ALTER CUBE para executar operações complexas, como excluir uma subárvore inteira de uma hierarquia e promover os filhos de um membro excluído.  
  
 **Write-backs de cubo**  
 Use a instrução [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) para fazer atualizações em um cubo habilitado para gravação. A instrução UPDATE CUBE permite atualizar uma tupla com um valor específico. Use a [Instrução REFRESH CUBE (MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) para atualizar dados de uma sessão de cliente com dados atualizados do servidor.  
  
 Para obter mais informações, consulte [Usando write-backs de cubo &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-using-cube-writebacks.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  

