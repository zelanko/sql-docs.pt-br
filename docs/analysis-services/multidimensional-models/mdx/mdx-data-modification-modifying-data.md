---
title: Modificação de dados (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f4fdaf60309d09a706fea552722017756b7945d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208759"
---
# <a name="mdx-data-modification---modifying-data"></a>Modificação de dados MDX – modificando dados
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Além de usar a linguagem MDX para recuperar e manipular dados de dimensões e cubos, você pode usá-la para atualizar ou executar *write-back* de dados de dimensão e de cubo. Essas atualizações podem ser temporárias, como na análise teórica (ou"what if"), ou permanentes, como quando alterações devem ser feitas com base na análise dos dados.  
  
 As atualizações de dados podem ocorrer no nível de dimensão ou de cubo:  
  
 **Write-backs de dimensão**  
 Use a [Instrução ALTER CUBE (MDX)](../../../mdx/mdx-data-definition-alter-cube.md) para alterar os dados de uma dimensão habilitada para gravação e a [Instrução REFRESH CUBE (MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) para refletir a exclusão, criação e atualização de valores de atributo. Você também pode usar a instrução ALTER CUBE para executar operações complexas, como excluir uma subárvore inteira de uma hierarquia e promover os filhos de um membro excluído.  
  
 **Write-backs de cubo**  
 Use a instrução [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) para fazer atualizações em um cubo habilitado para gravação. A instrução UPDATE CUBE permite atualizar uma tupla com um valor específico. Use a [Instrução REFRESH CUBE (MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) para atualizar dados de uma sessão de cliente com dados atualizados do servidor.  
  
 Para obter mais informações, consulte [Usando write-backs de cubo &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-using-cube-writebacks.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
