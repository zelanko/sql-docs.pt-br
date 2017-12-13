---
title: "Criando cálculos de célula no escopo da consulta (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
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
- WITH keyword
- query-scoped cell calculations [MDX]
ms.assetid: 45987daa-4400-41e9-add7-2428fd75709b
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6348f5728c937b5f41531566de6df853cfbb210f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-cell-calculations---query-scoped-cell-calculations"></a>Cálculos de célula MDX - cálculos de célula no escopo da consulta
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Você usa o **WITH** palavra-chave em expressões multidimensionais (MDX) para descrever células calculadas no contexto de uma consulta. A sintaxe da palavra-chave **WITH** é:  
  
```  
WITH CELL CALCULATION Cube_Name.CellCalc_Identifier  String_Expression  
```  
  
 O valor `CellCalc_Identifier` é o nome das células calculadas. O valor `String_Expression` contém uma lista de expressões de conjunto MDX ortogonais e unidimensionais. Cada uma delas deve resolver uma das categorias listadas na tabela a seguir.  
  
|Categoria|Description|  
|--------------|-----------------|  
|Conjunto vazio|Uma expressão de conjunto MDX resolvida em um conjunto vazio. Nesse caso, o escopo da célula calculada é o cubo inteiro.|  
|Conjunto de membro único|Uma expressão de conjunto MDX resolvida em um único membro.|  
|Conjunto de membros do nível|Uma expressão de conjunto MDX resolvida nos membros de um mesmo nível. Um exemplo de uma expressão de conjunto desse tipo é a função MDX *Level_Expression*.**Members** . Para incluir membros calculados, use a função MDX *Level_Expression*.**AllMembers**. Para obter mais informações, consulte [AllMembers &#40;MDX&#41;](../../../mdx/allmembers-mdx.md).|  
|Conjunto de descendentes|Uma expressão de conjunto MDX resolvida nos descendentes de um membro especificado. Um exemplo de uma expressão de conjunto desse tipo é a função MDX **Descendants**(*Member_Expression*, *Level_Expresion*, *Desc_Flag*). Para obter mais informações, consulte [Descendants &#40;MDX&#41;](../../../mdx/descendants-mdx.md).|  
  
 Se o argumento `String_Expression` não descrever uma dimensão, a linguagem MDX assumirá que todos os membros foram incluídos para a construção do subcubo de cálculo. Portanto, se o argumento `String_Expression` for NULL, a definição de células calculada será válida para o cubo inteiro.  
  
 O argumento `MDX_Expression` contém uma expressão MDX que avalia o valor de célula de todas as células definidas no argumento `String_Expression` .  
  
## <a name="additional-considerations"></a>Considerações adicionais  
 A linguagem MDX processa a condição de cálculo, especificada pela propriedade **CONDITION** , somente uma vez. Esse único processamento proporciona melhor desempenho para a avaliação de várias definições de células calculadas, especialmente com a sobreposição de células calculadas nas passagens do cubo.  
  
 Quando esse único processamento ocorre depende do escopo de criação da definição de células calculadas:  
  
-   Se criada em um escopo global, como parte de um cubo, a linguagem MDX processará a condição de cálculo quando o cubo for processado. Se, de alguma forma, as células forem modificadas no cubo e estiverem incluídas no subcubo de cálculo de uma definição de células calculadas, a condição de cálculo pode não ser precisa até que o cubo seja reprocessado. A modificação da célula pode ser causada, por exemplo, por write-backs. A condição de cálculo será novamente processada quando o cubo for reprocessado.  
  
-   Se criada no escopo de sessão, a linguagem MDX processará a condição de cálculo quando a instrução for emitida durante a sessão. Como no caso de definições de células calculadas criadas globalmente, se as células forem modificadas, a condição de cálculo pode não ser precisa até que o cubo seja reprocessado.  
  
-   Se criada no escopo de consulta, a linguagem MDX processará a condição de cálculo quando a consulta for executada. A questão da modificação da célula também ocorre aqui, embora os problemas de latência de dados sejam mínimos dado o pouco tempo de processamento da execução de consultas MDX.  
  
 Por outro lado, a linguagem MDX processará a fórmula do cálculo sempre que uma consulta MDX for emitida para um cubo que contém células incluídas na definição de células calculadas. Esse processamento ocorre independentemente do escopo de criação.  
  
## <a name="see-also"></a>Consulte também  
 [Instrução CREATE CELL CALCULATION &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-cell-calculation.md)  
  
  
