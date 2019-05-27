---
title: No escopo da sessão de criação de membros (MDX) calculados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- CREATE MEMBER statement
- session-scoped calculated members [MDX]
ms.assetid: 2875ed89-2c26-4645-8ed9-8848479d110f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 701d7a49f7ddda60983a03723506442eac17866b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074546"
---
# <a name="creating-session-scoped-calculated-members-mdx"></a>Criando membros calculados no escopo da sessão (MDX)
  Para criar um membro calculado disponível por meio de uma sessão de expressões MDX, use a instrução [CREATE MEMBER](/sql/mdx/mdx-data-definition-create-member). Um membro calculado criado com a instrução CREATE MEMBER não será removido até que a sessão MDX seja encerrada.  
  
 Como discutido neste tópico, a sintaxe da instrução CREATE MEMBER é direta e fácil usar.  
  
> [!NOTE]  
>  Para obter mais informações sobre membros calculados, consulte [Criando membros calculados no MDX &#40;MDX&#41;](mdx-calculated-members-building-calculated-members.md).  
  
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
 [Criando membros calculados no escopo da consulta &#40;MDX&#41;](mdx-calculated-members-query-scoped-calculated-members.md)  
  
  
