---
title: Criando no escopo da sessão calculados membros (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 476c62ef2aa4f0aad3d65cd2b78f27fc9ae6fd7c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-calculated-members---session-scoped-calculated-members"></a>MDX calculadas membros - membros calculados no escopo da sessão
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Para criar um membro calculado disponível por meio de uma sessão de expressões MDX, use a instrução [CREATE MEMBER](../../../mdx/mdx-data-definition-create-member.md). Um membro calculado criado com a instrução CREATE MEMBER não será removido até que a sessão MDX seja encerrada.  
  
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
 [Criando no escopo da consulta calculados membros & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md)  
  
  
