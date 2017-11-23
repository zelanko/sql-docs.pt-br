---
title: "Criando no escopo da sessão calculados membros (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE MEMBER statement
- session-scoped calculated members [MDX]
ms.assetid: 2875ed89-2c26-4645-8ed9-8848479d110f
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7c8eadd09ca4946db6618f30e48907d97147b80d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-calculated-members---session-scoped-calculated-members"></a>MDX calculadas membros - membros calculados no escopo da sessão
  Para criar um membro calculado disponível por meio de uma sessão de expressões MDX, use a instrução [CREATE MEMBER](../../../mdx/mdx-data-definition-create-member.md) . Um membro calculado criado com a instrução CREATE MEMBER não será removido até que a sessão MDX seja encerrada.  
  
 Como discutido neste tópico, a sintaxe da instrução CREATE MEMBER é direta e fácil usar.  
  
> [!NOTE]  
>  Para obter mais informações sobre membros calculados, consulte [Criando membros calculados no MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md).  
  
## <a name="create-member-syntax"></a>Sintaxe de CREATE MEMBER  
 Use a sintaxe a seguir para adicionar a instrução CREATE MEMBER à instrução MDX:  
  
```  
CREATE [SESSION] MEMBER [<cube-name>.]<fully-qualified-member-name> AS <expression> [,<property-definition-list>]  
<cube name> ::= CURRENTCUBE | <Cube Name>  
<property-definition-list> ::= <property-definition>  
  | <property-definition>, <property-definition-list>  
<property-definition> ::= <property-identifier> = <property-value>  
<property-identifier> ::= VISIBLE | SOLVEORDER | SOLVE_ORDER | FORMAT_STRING | NON_EMPTY_BEHAVIOR <ole db member properties>  
```  
  
 Na sintaxe da instrução CREATE MEMBER, o valor `fully-qualified-member-name` é o nome totalmente qualificado do membro calculado. O nome totalmente qualificado inclui a dimensão ou o nível a que o membro calculado está associado. O valor `expression` retorna o valor do membro calculado depois que o valor de expressão foi avaliado.  
  
## <a name="create-member-example"></a>Exemplo de CREATE MEMBER  
 O exemplo a seguir usa a instrução CREATE MEMBER para criar o membro calculado `LastFourStores` . Esse membro calculado retorna a soma de unidades vendidas nas últimas quatro lojas e estará disponível durante toda a sessão do cubo.  
  
```  
Create Session Member [Store].[Measures].LastFourStores as   
sum(([Stores].[ByLocation].Lag(3) :  
[Stores].[ByLocation].NextMember), [Measures].[Units Sold])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criando membros calculados no escopo da consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md)  
  
  
