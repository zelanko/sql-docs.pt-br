---
title: Criar consultas de pesquisa de texto completo (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CONTAINS predicate (Transact-SQL)
- queries [full-text search], creating
- full-text queries [SQL Server], creating
ms.assetid: 537fa556-390e-4c88-9b8e-679848d94abc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1f3ab74c6dd095fd92e0f9d20ba622be70a37ef9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63184348"
---
# <a name="create-full-text-search-queries-visual-database-tools"></a>Criar consultas de pesquisa de texto completo (Visual Database Tools)
  Pesquisas de texto completo usam o predicado CONTAINS para localizar linhas que especificaram texto em uma determinada coluna. Pesquisas de texto completo somente são possíveis em colunas que têm índices de texto completo ativos. Se você tentar usar a cláusula CONTAINS em uma coluna que não tem um índice de texto completo ativo atualmente, receberá um erro. Para obter mais informações sobre índices de texto completo e a cláusula CONTAINS, consulte [pesquisa de texto completo](../../relational-databases/search/full-text-search.md) e [contém &#40;&#41;Transact-SQL ](/sql/t-sql/queries/contains-transact-sql).  
  
### <a name="to-create-a-full-text-search-query"></a>Para criar uma consulta de pesquisa de texto completo  
  
1.  Abra uma consulta no Gerenciador de Soluções ou crie uma consulta nova.  
  
2.  Na cláusula WHERE da consulta, use a função CONTAINS para pesquisar uma coluna de texto completo.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de consulta com suporte &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Tópicos de instruções sobre como criar consultas e exibições &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Executar operações básicas com consultas &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
