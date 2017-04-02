---
title: "Criar consultas de detalhamento usando DMX | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 42c896ee-e5ee-4017-b66e-31d1fe66d369
caps.latest.revision: 5
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 5
---
# Criar consultas de detalhamento usando DMX
  Em todos os modelos com suporte ao detalhamento, você pode recuperar dados de caso e dados de estrutura criando uma consulta DMX no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou qualquer outro cliente que ofereça suporte a DMX.  
  
> [!WARNING]  
>  Para exibir os dados, o detalhamento precisa estar habilitado e você precisa ter as permissões necessárias.  
  
## Especificando opções de detalhamento  
 A sintaxe geral é para recuperar casos de modelo e de estrutura como se segue:  
  
```  
SELECT <model column list>, StructureColumn('<structure column name') FROM <modelname>.CASES  
```  
  
 Para obter mais informações sobre como usar consultas DMX para retornar dados de caso, consulte [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](../Topic/SELECT%20FROM%20%3Cmodel%3E.CASES%20\(DMX\).md) e [SELECT FROM &#60;structure&#62;.CASES](../Topic/SELECT%20FROM%20%3Cstructure%3E.CASES.md).  
  
## Exemplos  
 A consulta DMX a seguir retorna os dados de caso para uma série de produtos específica, de um modelo de série temporal. A consulta também retorna a coluna **Amount**, que não foi usada no modelo, mas está disponível na estrutura de mineração.  
  
```  
SELECT [DateSeries], [Model Region], Quantity, StructureColumn('Amount') AS [M200 Pacific Amount]  
FROM Forecasting.CASES  
WHERE [Model Region] = 'M200 Pacific'  
```  
  
 Note que, neste exemplo, um alias foi usado para renomear a coluna de estrutura. Se você não atribuir um alias à coluna de estrutura, a coluna será retornada com o nome 'Expression'. Este é o comportamento padrão para todas as colunas sem nome.  
  
## Consulte também  
 [Consultas de detalhamento &#40;Mineração de dados&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [Detalhamento em estruturas de mineração](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  