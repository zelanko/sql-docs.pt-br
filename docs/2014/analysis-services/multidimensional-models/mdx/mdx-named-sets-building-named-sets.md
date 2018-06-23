---
title: Criando conjuntos nomeados em MDX (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], named sets
- named sets [MDX]
- sets [MDX]
- MDX [Analysis Services], named sets
- queries [MDX], named sets
- set expressions [MDX]
ms.assetid: 213b0035-e96d-4ba0-83f2-ded206905603
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9a05b343150cf72a760ba5eb9de24651f0f5db9f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008500"
---
# <a name="building-named-sets-in-mdx-mdx"></a>Criando conjuntos nomeados em MDX (MDX)
  Uma expressão de conjunto pode ser uma declaração longa e complexa e, portanto, difícil de seguir ou entender. Ou ainda, a expressão de conjunto pode ser usada com tanta frequência que sua definição repetidamente passa a ser penosa. Para ajudar a facilitar o trabalho com expressões longas, complexas e geralmente usadas, as expressões MDX permitem que você trabalhe nelas como um *conjunto nomeado*.  
  
 Basicamente, um conjunto nomeado é uma expressão de conjunto para a qual um alias foi atribuído. Um conjunto nomeado pode incorporar todos os membros ou funções que normalmente podem ser incorporados a um conjunto. Como a linguagem MDX trata o conjunto nomeado como uma expressão de conjunto, é possível usar esse alias em qualquer lugar que aceite uma expressão de conjunto.  
  
 Você pode definir um conjunto nomeado para ter um destes contextos:  
  
-   **No escopo da consulta** Para criar um conjunto nomeado que seja definido como parte de uma consulta MDX e, portanto, cujo escopo esteja limitado à consulta, use a palavra-chave WITH. Em seguida, você pode usar o conjunto nomeado em uma instrução MDX SELECT. Usando essa abordagem, o conjunto nomeado criado pelo uso da palavra-chave pode ser alterado sem afetar a instrução SELECT.  
  
     Para obter mais informações sobre como usar a palavra-chave WITH para criar conjuntos nomeados, consulte [Criando conjuntos nomeados no escopo da consulta &#40;MDX&#41;](mdx-named-sets-creating-query-scoped-named-sets.md).  
  
-   **No escopo da sessão** Para criar um conjunto nomeado cujo escopo seja mais amplo que o contexto da consulta, ou seja, cujo escopo seja o tempo de vida da sessão de MDX, use a instrução CREATE SET. Um conjunto nomeado definido pela instrução CREATE SET estará disponível para todas as consultas MDX dessa sessão. A instrução CREATE SET faz sentido, por exemplo, em um aplicativo cliente que reutiliza consistentemente um conjunto em diversas consultas.  
  
     Para obter mais informações sobre como usar a instrução CREATE SET para criar conjuntos nomeados em uma sessão, consulte [Criando conjuntos nomeados no escopo da sessão &#40;MDX&#41;](mdx-named-sets-creating-session-scoped-named-sets.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instrução SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [Instrução CREATE SET &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-set)   
 [Conceitos básicos de consulta MDX &#40;do Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
