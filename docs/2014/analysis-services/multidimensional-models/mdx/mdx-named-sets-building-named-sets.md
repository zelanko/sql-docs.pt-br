---
title: Criando conjuntos nomeados em MDX (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], named sets
- named sets [MDX]
- sets [MDX]
- MDX [Analysis Services], named sets
- queries [MDX], named sets
- set expressions [MDX]
ms.assetid: 213b0035-e96d-4ba0-83f2-ded206905603
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 98d363ab09e75905b13503687fe425a981c790e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074153"
---
# <a name="building-named-sets-in-mdx-mdx"></a>Criando conjuntos nomeados em MDX (MDX)
  Uma expressão de conjunto pode ser uma declaração longa e complexa e, portanto, difícil de seguir ou entender. Ou ainda, a expressão de conjunto pode ser usada com tanta frequência que sua definição repetidamente passa a ser penosa. Para ajudar a facilitar o trabalho com expressões longas, complexas e geralmente usadas, as expressões MDX permitem que você trabalhe nelas como um *conjunto nomeado*.  
  
 Basicamente, um conjunto nomeado é uma expressão de conjunto para a qual um alias foi atribuído. Um conjunto nomeado pode incorporar todos os membros ou funções que normalmente podem ser incorporados a um conjunto. Como a linguagem MDX trata o conjunto nomeado como uma expressão de conjunto, é possível usar esse alias em qualquer lugar que aceite uma expressão de conjunto.  
  
 Você pode definir um conjunto nomeado para ter um destes contextos:  
  
-   **Com escopo de consulta** Para criar um conjunto nomeado que é definido como parte de uma consulta MDX e, portanto, cujo escopo é limitado à consulta, você usa a palavra-chave WITH. Em seguida, você pode usar o conjunto nomeado em uma instrução MDX SELECT. Usando essa abordagem, o conjunto nomeado criado pelo uso da palavra-chave pode ser alterado sem afetar a instrução SELECT.  
  
     Para obter mais informações sobre como usar a palavra-chave WITH para criar conjuntos nomeados, consulte [Criando conjuntos nomeados no escopo da consulta &#40;MDX&#41;](mdx-named-sets-creating-query-scoped-named-sets.md).  
  
-   **Escopo da sessão** Para criar um conjunto nomeado cujo escopo é mais largo do que o contexto da consulta, ou seja, cujo escopo é o tempo de vida da sessão MDX, use a instrução CREATE SET. Um conjunto nomeado definido pela instrução CREATE SET estará disponível para todas as consultas MDX dessa sessão. A instrução CREATE SET faz sentido, por exemplo, em um aplicativo cliente que reutiliza consistentemente um conjunto em diversas consultas.  
  
     Para obter mais informações sobre como usar a instrução CREATE SET para criar conjuntos nomeados em uma sessão, consulte [Criando conjuntos nomeados no escopo da sessão &#40;MDX&#41;](mdx-named-sets-creating-session-scoped-named-sets.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instrução SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [Instrução CREATE SET &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-set)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
