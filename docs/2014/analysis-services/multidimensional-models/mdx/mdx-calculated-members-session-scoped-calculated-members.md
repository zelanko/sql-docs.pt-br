---
title: No escopo da sessão de criação de membros (MDX) calculados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- CREATE MEMBER statement
- session-scoped calculated members [MDX]
ms.assetid: 2875ed89-2c26-4645-8ed9-8848479d110f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 53d6cc069e316bc399235aafbf59c7586bbdc6c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136496"
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
 [Criando no escopo da consulta de membros calculados &#40;MDX&#41;](mdx-calculated-members-query-scoped-calculated-members.md)  
  
  
