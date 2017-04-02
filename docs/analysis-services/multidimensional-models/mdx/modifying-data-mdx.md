---
title: "Modificando dados (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modificando dados [MDX]"
  - "Expressões MDX [Analysis Services], modificações de dados"
  - "MDX [Analysis Services], modificações de dados"
  - "modificações de dados [MDX]"
ms.assetid: 363b662c-b839-4971-bbd7-1842f73ce141
caps.latest.revision: 30
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Modificando dados (MDX)
  Além de usar a linguagem MDX para recuperar e manipular dados de dimensões e cubos, você pode usá-la para atualizar ou executar *write-back* de dados de dimensão e de cubo. Essas atualizações podem ser temporárias, como na análise teórica (ou"what if"), ou permanentes, como quando alterações devem ser feitas com base na análise dos dados.  
  
 As atualizações de dados podem ocorrer no nível de dimensão ou de cubo:  
  
 **Write-backs de dimensão**  
 Use a [Instrução ALTER CUBE (MDX)](../Topic/ALTER%20CUBE%20Statement%20\(MDX\).md) para alterar os dados de uma dimensão habilitada para gravação e a [Instrução REFRESH CUBE (MDX)](../Topic/REFRESH%20CUBE%20Statement%20\(MDX\).md) para refletir a exclusão, criação e atualização de valores de atributo. Você também pode usar a instrução ALTER CUBE para executar operações complexas, como excluir uma subárvore inteira de uma hierarquia e promover os filhos de um membro excluído.  
  
 **Write-backs de cubo**  
 Use a instrução [UPDATE CUBE](../Topic/UPDATE%20CUBE%20Statement%20\(MDX\).md) para fazer atualizações em um cubo habilitado para gravação. A instrução UPDATE CUBE permite atualizar uma tupla com um valor específico. Use a [Instrução REFRESH CUBE (MDX)](../Topic/REFRESH%20CUBE%20Statement%20\(MDX\).md) para atualizar dados de uma sessão de cliente com dados atualizados do servidor.  
  
 Para obter mais informações, consulte [Usando write-backs de cubo &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-cube-writebacks-mdx.md).  
  
## Consulte também  
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  