---
title: Criar consultas de detalhamento usando DMX | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 42c896ee-e5ee-4017-b66e-31d1fe66d369
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9d211455f1b7ee27071f166485b41764253734cb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="create-drillthrough-queries-using-dmx"></a>Criar consultas de detalhamento usando DMX
  Em todos os modelos com suporte ao detalhamento, você pode recuperar dados de caso e dados de estrutura criando uma consulta DMX no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou qualquer outro cliente que ofereça suporte a DMX.  
  
> [!WARNING]  
>  Para exibir os dados, o detalhamento precisa estar habilitado e você precisa ter as permissões necessárias.  
  
## <a name="specifying-drillthrough-options"></a>Especificando opções de detalhamento  
 A sintaxe geral é para recuperar casos de modelo e de estrutura como se segue:  
  
```  
SELECT <model column list>, StructureColumn('<structure column name') FROM <modelname>.CASES  
```  
  
 Para obter mais informações sobre como usar consultas DMX para retornar dados de caso, consulte [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](../../dmx/select-from-model-cases-dmx.md) e [SELECT FROM &#60;structure&#62;.CASES](../../dmx/select-from-structure-cases.md).  
  
## <a name="examples"></a>Exemplos  
 A consulta DMX a seguir retorna os dados de caso para uma série de produtos específica, de um modelo de série temporal. A consulta também retorna a coluna **Amount**, que não foi usada no modelo, mas está disponível na estrutura de mineração.  
  
```  
SELECT [DateSeries], [Model Region], Quantity, StructureColumn('Amount') AS [M200 Pacific Amount]  
FROM Forecasting.CASES  
WHERE [Model Region] = 'M200 Pacific'  
```  
  
 Note que, neste exemplo, um alias foi usado para renomear a coluna de estrutura. Se você não atribuir um alias à coluna de estrutura, a coluna será retornada com o nome 'Expression'. Este é o comportamento padrão para todas as colunas sem nome.  
  
## <a name="see-also"></a>Consulte também  
 [Consultas de detalhamento &#40;Mineração de dados&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [Detalhamento em estruturas de mineração](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  
