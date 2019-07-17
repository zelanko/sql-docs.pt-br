---
title: Criar consultas de detalhamento usando DMX | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6616f90f475da91f3f5c38c0f5922d16d72a5408
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210148"
---
# <a name="create-drillthrough-queries-using-dmx"></a>Criar consultas de detalhamento usando DMX
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
  
