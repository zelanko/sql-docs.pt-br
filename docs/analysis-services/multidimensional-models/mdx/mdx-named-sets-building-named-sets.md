---
title: Criando conjuntos nomeados em MDX (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 526d1cc2ec6ecc7e4e2e74793960137b8dfb3647
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-named-sets---building-named-sets"></a>MDX denominado conjuntos - criando conjuntos nomeados
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Uma expressão de conjunto pode ser uma declaração longa e complexa e, portanto, difícil de seguir ou entender. Ou ainda, a expressão de conjunto pode ser usada com tanta frequência que sua definição repetidamente passa a ser penosa. Para ajudar a facilitar o trabalho com expressões longas, complexas e geralmente usadas, as expressões MDX permitem que você trabalhe nelas como um *conjunto nomeado*.  
  
 Basicamente, um conjunto nomeado é uma expressão de conjunto para a qual um alias foi atribuído. Um conjunto nomeado pode incorporar todos os membros ou funções que normalmente podem ser incorporados a um conjunto. Como a linguagem MDX trata o conjunto nomeado como uma expressão de conjunto, é possível usar esse alias em qualquer lugar que aceite uma expressão de conjunto.  
  
 Você pode definir um conjunto nomeado para ter um destes contextos:  
  
-   **No escopo da consulta** Para criar um conjunto nomeado que seja definido como parte de uma consulta MDX e, portanto, cujo escopo esteja limitado à consulta, use a palavra-chave WITH. Em seguida, você pode usar o conjunto nomeado em uma instrução MDX SELECT. Usando essa abordagem, o conjunto nomeado criado pelo uso da palavra-chave pode ser alterado sem afetar a instrução SELECT.  
  
     Para obter mais informações sobre como usar a palavra-chave WITH para criar conjuntos nomeados, consulte [Criando conjuntos nomeados no escopo da consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md).  
  
-   **No escopo da sessão** Para criar um conjunto nomeado cujo escopo seja mais amplo que o contexto da consulta, ou seja, cujo escopo seja o tempo de vida da sessão de MDX, use a instrução CREATE SET. Um conjunto nomeado definido pela instrução CREATE SET estará disponível para todas as consultas MDX dessa sessão. A instrução CREATE SET faz sentido, por exemplo, em um aplicativo cliente que reutiliza consistentemente um conjunto em diversas consultas.  
  
     Para obter mais informações sobre como usar a instrução CREATE SET para criar conjuntos nomeados em uma sessão, consulte [Criando conjuntos nomeados no escopo da sessão &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-session-scoped-named-sets.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instrução SELECT & #40; MDX & #41;](../../../mdx/mdx-data-manipulation-select.md)   
 [CRIAR a instrução SET & #40; MDX & #41;](../../../mdx/mdx-data-definition-create-set.md)   
 [Conceitos básicos de consulta MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
