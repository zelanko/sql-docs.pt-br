---
title: "Criando conjuntos nomeados no escopo da sess&#227;o (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
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
  - "Instrução CREATE SET"
  - "conjuntos nomeados no escopo da sessão [MDX]"
ms.assetid: b751e1e4-6d4c-4d36-a28d-ffdaaee0f1c7
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Criando conjuntos nomeados no escopo da sess&#227;o (MDX)
  Para criar um conjunto nomeado que esteja disponível por meio de uma sessão da linguagem MDX, use a instrução [CREATE SET](../Topic/CREATE%20SET%20Statement%20\(MDX\).md). Um conjunto nomeado criado com a instrução CREATE SET não será removido até que a sessão MDX seja encerrada.  
  
 Como discutido neste tópico, a sintaxe da palavra-chave WITH é direta e fácil usar.  
  
> [!NOTE]  
>  Para obter mais informações sobre conjuntos nomeados, consulte [Criando conjuntos nomeados em MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-named-sets-in-mdx-mdx.md).  
  
## Sintaxe de CREATE SET  
 Use a sintaxe a seguir para uma instrução CREATE SET:  
  
```  
CREATE SESSION SET [CURRENTCUBE. | <cube name>.]<Set Identifier> AS <Set Expression>  
```  
  
 Na sintaxe de CREATE SET, o parâmetro `cube name` contém o nome do cubo que contém os membros do conjunto nomeado. Se o parâmetro `cube name` não for especificado, o cubo atual será usado como o cubo que contém o membro do conjunto nomeado. Além disso, o parâmetro `Set_Identifier` contém o alias do conjunto nomeado, e o parâmetro `Set_Expression` contém a expressão de conjunto à qual o alias do conjunto nomeado fará referência.  
  
## Exemplo de CREATE SET  
 O exemplo a seguir usa a instrução CREATE SET para criar o conjunto nomeado `SetCities_2_3` com base no cubo Loja. Os membros do conjunto nomeado `SetCities_2_3` são as lojas localizadas em Cidade 2 e Cidade 3.  
  
```  
create Session set [Store].[SetCities_2_3] as  
{[Data Stores].[ByLocation].[State].&[CA].&[City 02],  
[Data Stores].[ByLocation].[State].&[NH].&[City 03]}  
```  
  
 Ao usar a instrução CREATE SET para definir o conjunto nomeado `SetCities_2_3` , esse conjunto nomeado continuará disponível durante a sessão MDX atual. O exemplo a seguir é uma consulta válida que retornaria os membros de Cidade 2 e Cidade 3 e que poderia ser executada a qualquer momento após a criação do conjunto nomeado `SetCities_2_3` e antes do fim da sessão.  
  
```  
select SetCities_2_3 on 0 from [Store]  
```  
  
## Consulte também  
 [Criando conjuntos nomeados no escopo da consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/creating-query-scoped-named-sets-mdx.md)  
  
  