---
title: "Criando no escopo da sessão conjuntos nomeados (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE SET statement
- session-scoped named sets [MDX]
ms.assetid: b751e1e4-6d4c-4d36-a28d-ffdaaee0f1c7
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 372990a1016616c72768cd51cb8c6eedb2008a58
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="mdx-named-sets---creating-session-scoped-named-sets"></a>Conjuntos nomeados de MDX denominado conjuntos - criando no escopo da sessão
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
Para criar um conjunto nomeado que esteja disponível por meio de uma sessão da linguagem MDX, use a instrução [CREATE SET](../../../mdx/mdx-data-definition-create-set.md). Um conjunto nomeado criado com a instrução CREATE SET não será removido até que a sessão MDX seja encerrada.  
  
 Como discutido neste tópico, a sintaxe da palavra-chave WITH é direta e fácil usar.  
  
> [!NOTE]  
>  Para obter mais informações sobre conjuntos nomeados, consulte [Criando conjuntos nomeados em MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md).  
  
## <a name="create-set-syntax"></a>Sintaxe de CREATE SET  
 Use a sintaxe a seguir para uma instrução CREATE SET:  
  
```  
CREATE SESSION SET [CURRENTCUBE. | <cube name>.]<Set Identifier> AS <Set Expression>  
```  
  
 Na sintaxe de CREATE SET, o parâmetro `cube name` contém o nome do cubo que contém os membros do conjunto nomeado. Se o parâmetro `cube name` não for especificado, o cubo atual será usado como o cubo que contém o membro do conjunto nomeado. Além disso, o parâmetro `Set_Identifier` contém o alias do conjunto nomeado, e o parâmetro `Set_Expression` contém a expressão de conjunto à qual o alias do conjunto nomeado fará referência.  
  
## <a name="create-set-example"></a>Exemplo de CREATE SET  
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
  
## <a name="see-also"></a>Consulte também  
 [Criar no escopo da consulta nomeada conjuntos &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md)  
  
  
