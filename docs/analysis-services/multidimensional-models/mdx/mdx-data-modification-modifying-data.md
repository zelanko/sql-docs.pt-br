---
title: Modificando dados (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
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
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4c490f3998b148691f35328fe5543874be92f997
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-data-modification---modifying-data"></a>Modificação de dados MDX - modificando dados
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Além de usar MDX (Multidimensional Expressions) para recuperar e manipular dados de cubos e dimensões, você pode usar MDX para atualizar ou *write-back* dados de cubo e dimensão. Essas atualizações podem ser temporárias, como na análise teórica (ou"what if"), ou permanentes, como quando alterações devem ser feitas com base na análise dos dados.  
  
 As atualizações de dados podem ocorrer no nível de dimensão ou de cubo:  
  
 **Write-backs de dimensão**  
 Use a [Instrução ALTER CUBE (MDX)](../../../mdx/mdx-data-definition-alter-cube.md) para alterar os dados de uma dimensão habilitada para gravação e a [Instrução REFRESH CUBE (MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) para refletir a exclusão, criação e atualização de valores de atributo. Você também pode usar a instrução ALTER CUBE para executar operações complexas, como excluir uma subárvore inteira de uma hierarquia e promover os filhos de um membro excluído.  
  
 **Write-backs de cubo**  
 Use a instrução [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) para fazer atualizações em um cubo habilitado para gravação. A instrução UPDATE CUBE permite atualizar uma tupla com um valor específico. Use a [Instrução REFRESH CUBE (MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) para atualizar dados de uma sessão de cliente com dados atualizados do servidor.  
  
 Para obter mais informações, consulte [Usando write-backs de cubo &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-using-cube-writebacks.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
