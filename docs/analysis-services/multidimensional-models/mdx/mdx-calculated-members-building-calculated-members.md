---
title: Criando membros calculados em MDX (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- MDX [Analysis Services], calculated members
- calculated members [MDX]
- Multidimensional Expressions [Analysis Services], calculated members
- queries [MDX], calculated members
ms.assetid: 9322e8b8-43e1-4e02-a7d1-e41a586a5bb8
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: cbfe97ab13483ccaf31134bfa45ab5b583f797d7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-calculated-members---building-calculated-members"></a>MDX calculadas membros - Criando membros calculados
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Em expressões multidimensionais (MDX), um membro calculado é um membro que é resolvido pelo cálculo de uma expressão MDX para retornar um valor. Essa simples definição abrange uma quantidade enorme implicações. A capacidade de construir e usar membros calculados em uma consulta MDX proporciona uma grande capacidade de manipulação de dados multidimensionais.  
  
 Você pode criar membros calculados em qualquer ponto de uma hierarquia. Pode também criar membros calculados que dependem não só dos membros existentes em um cubo, mas também de outros membros calculados definidos na mesma expressão MDX.  
  
 É possível definir um membro calculado para ter um destes contextos:  
  
-   **Com escopo da consulta** Para criar um membro calculado que seja definido como parte de uma consulta MDX e, portanto, cujo escopo esteja limitado à consulta, use a palavra-chave WITH. Você pode usar o membro calculado em uma instrução MDX SELECT. Usando essa abordagem, o membro calculado criado pelo uso da palavra-chave pode ser alterado sem afetar a instrução SELECT.  
  
     Para obter mais informações sobre como usar a palavra-chave WITH para criar membros calculados, consulte [Criando membros calculados no escopo da consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
-   **Com escopo da sessão** Para criar um membro calculado cujo escopo seja mais amplo que o contexto da consulta, ou seja, cujo escopo seja o tempo de vida da sessão MDX, use a instrução CREATE MEMBER. Um membro calculado definido usando-se a instrução CREATE MEMBER fica disponível para todas as consultas MDX dessa sessão. A instrução CREATE MEMBER faz sentido, por exemplo, em um aplicativo cliente que reutiliza consistentemente o mesmo conjunto em diversas consultas.  
  
     Para obter mais informações sobre como usar a instrução CREATE MEMBER para criar membros calculados em uma sessão, consulte [Criando membros calculados no escopo da sessão &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instrução CREATE MEMBER &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)   
 [Referência da Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)   
 [Instrução SELECT &#40; MDX &#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
