---
title: Criando membros calculados em MDX (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MDX [Analysis Services], calculated members
- calculated members [MDX]
- Multidimensional Expressions [Analysis Services], calculated members
- queries [MDX], calculated members
ms.assetid: 9322e8b8-43e1-4e02-a7d1-e41a586a5bb8
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5f01746c6bb0c73705451db8f236c75c1b8935bf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312646"
---
# <a name="building-calculated-members-in-mdx-mdx"></a>Criando membros calculados em MDX (MDX)
  Na linguagem MDX, um membro calculado é aquele resolvido pelo cálculo de uma expressão MDX para retornar um valor. Essa simples definição abrange uma quantidade enorme implicações. A capacidade de construir e usar membros calculados em uma consulta MDX proporciona uma grande capacidade de manipulação de dados multidimensionais.  
  
 Você pode criar membros calculados em qualquer ponto de uma hierarquia. Pode também criar membros calculados que dependem não só dos membros existentes em um cubo, mas também de outros membros calculados definidos na mesma expressão MDX.  
  
 É possível definir um membro calculado para ter um destes contextos:  
  
-   **Com escopo da consulta** Para criar um membro calculado que seja definido como parte de uma consulta MDX e, portanto, cujo escopo esteja limitado à consulta, use a palavra-chave WITH. Você pode usar o membro calculado em uma instrução MDX SELECT. Usando essa abordagem, o membro calculado criado pelo uso da palavra-chave pode ser alterado sem afetar a instrução SELECT.  
  
     Para obter mais informações sobre como usar a palavra-chave WITH para criar membros calculados, consulte [Criando membros calculados no escopo da consulta &#40;MDX&#41;](mdx-calculated-members-query-scoped-calculated-members.md).  
  
-   **Com escopo da sessão** Para criar um membro calculado cujo escopo seja mais amplo que o contexto da consulta, ou seja, cujo escopo seja o tempo de vida da sessão MDX, use a instrução CREATE MEMBER. Um membro calculado definido usando-se a instrução CREATE MEMBER fica disponível para todas as consultas MDX dessa sessão. A instrução CREATE MEMBER faz sentido, por exemplo, em um aplicativo cliente que reutiliza consistentemente o mesmo conjunto em diversas consultas.  
  
     Para obter mais informações sobre como usar a instrução CREATE MEMBER para criar membros calculados em uma sessão, consulte [Criando membros calculados no escopo da sessão &#40;MDX&#41;](mdx-calculated-members-session-scoped-calculated-members.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instrução CREATE MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)   
 [Referência da função MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)   
 [Instrução SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)  
  
  
