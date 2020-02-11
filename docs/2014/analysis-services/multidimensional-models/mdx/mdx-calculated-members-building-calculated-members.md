---
title: Criando membros calculados em MDX (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MDX [Analysis Services], calculated members
- calculated members [MDX]
- Multidimensional Expressions [Analysis Services], calculated members
- queries [MDX], calculated members
ms.assetid: 9322e8b8-43e1-4e02-a7d1-e41a586a5bb8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0275a071c5548de7086844e48cec7eff3bb72d31
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074537"
---
# <a name="building-calculated-members-in-mdx-mdx"></a>Criando membros calculados em MDX (MDX)
  Na linguagem MDX, um membro calculado é aquele resolvido pelo cálculo de uma expressão MDX para retornar um valor. Essa simples definição abrange uma quantidade enorme implicações. A capacidade de construir e usar membros calculados em uma consulta MDX proporciona uma grande capacidade de manipulação de dados multidimensionais.  
  
 Você pode criar membros calculados em qualquer ponto de uma hierarquia. Pode também criar membros calculados que dependem não só dos membros existentes em um cubo, mas também de outros membros calculados definidos na mesma expressão MDX.  
  
 É possível definir um membro calculado para ter um destes contextos:  
  
-   **Com escopo de consulta** Para criar um membro calculado que é definido como parte de uma consulta MDX e, portanto, cujo escopo é limitado à consulta, você usa a palavra-chave WITH. Você pode usar o membro calculado em uma instrução MDX SELECT. Usando essa abordagem, o membro calculado criado pelo uso da palavra-chave pode ser alterado sem afetar a instrução SELECT.  
  
     Para obter mais informações sobre como usar a palavra-chave WITH para criar membros calculados, consulte [Criando membros calculados no escopo da consulta &#40;MDX&#41;](mdx-calculated-members-query-scoped-calculated-members.md).  
  
-   **Escopo da sessão** Para criar um membro calculado cujo escopo seja mais largo do que o contexto da consulta, ou seja, cujo escopo é o tempo de vida da sessão MDX, use a instrução CREATE MEMBER. Um membro calculado definido usando-se a instrução CREATE MEMBER fica disponível para todas as consultas MDX dessa sessão. A instrução CREATE MEMBER faz sentido, por exemplo, em um aplicativo cliente que reutiliza consistentemente o mesmo conjunto em diversas consultas.  
  
     Para obter mais informações sobre como usar a instrução CREATE MEMBER para criar membros calculados em uma sessão, consulte [Criando membros calculados no escopo da sessão &#40;MDX&#41;](mdx-calculated-members-session-scoped-calculated-members.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instrução CREATE MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)   
 [Referência de função MDX &#40;&#41;MDX](/sql/mdx/mdx-function-reference-mdx)   
 [Instrução SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)  
  
  
