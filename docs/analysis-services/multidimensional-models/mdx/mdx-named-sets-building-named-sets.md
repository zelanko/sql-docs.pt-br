---
title: Criando conjuntos nomeados em MDX (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], named sets
- named sets [MDX]
- sets [MDX]
- MDX [Analysis Services], named sets
- queries [MDX], named sets
- set expressions [MDX]
ms.assetid: 213b0035-e96d-4ba0-83f2-ded206905603
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9239f7ee621cec3032c42d10b70c75702b58db6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-named-sets---building-named-sets"></a>MDX denominado conjuntos - criando conjuntos nomeados
  Uma expressão de conjunto pode ser uma declaração longa e complexa e, portanto, difícil de seguir ou entender. Ou ainda, a expressão de conjunto pode ser usada com tanta frequência que sua definição repetidamente passa a ser penosa. Para ajudar a facilitar o trabalho com expressões longas, complexas e geralmente usadas, as expressões MDX permitem que você trabalhe nelas como um *conjunto nomeado*.  
  
 Basicamente, um conjunto nomeado é uma expressão de conjunto para a qual um alias foi atribuído. Um conjunto nomeado pode incorporar todos os membros ou funções que normalmente podem ser incorporados a um conjunto. Como a linguagem MDX trata o conjunto nomeado como uma expressão de conjunto, é possível usar esse alias em qualquer lugar que aceite uma expressão de conjunto.  
  
 Você pode definir um conjunto nomeado para ter um destes contextos:  
  
-   **No escopo da consulta** Para criar um conjunto nomeado que seja definido como parte de uma consulta MDX e, portanto, cujo escopo esteja limitado à consulta, use a palavra-chave WITH. Em seguida, você pode usar o conjunto nomeado em uma instrução MDX SELECT. Usando essa abordagem, o conjunto nomeado criado pelo uso da palavra-chave pode ser alterado sem afetar a instrução SELECT.  
  
     Para obter mais informações sobre como usar a palavra-chave WITH para criar conjuntos nomeados, consulte [Criando conjuntos nomeados no escopo da consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md).  
  
-   **No escopo da sessão** Para criar um conjunto nomeado cujo escopo seja mais amplo que o contexto da consulta, ou seja, cujo escopo seja o tempo de vida da sessão de MDX, use a instrução CREATE SET. Um conjunto nomeado definido pela instrução CREATE SET estará disponível para todas as consultas MDX dessa sessão. A instrução CREATE SET faz sentido, por exemplo, em um aplicativo cliente que reutiliza consistentemente um conjunto em diversas consultas.  
  
     Para obter mais informações sobre como usar a instrução CREATE SET para criar conjuntos nomeados em uma sessão, consulte [Criando conjuntos nomeados no escopo da sessão &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-session-scoped-named-sets.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instrução SELECT &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)   
 [CRIAR a instrução SET &#40; MDX &#41;](../../../mdx/mdx-data-definition-create-set.md)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  

