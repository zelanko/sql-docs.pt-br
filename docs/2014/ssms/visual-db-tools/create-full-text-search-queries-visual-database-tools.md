---
title: Criar consultas de pesquisa de texto completo (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- CONTAINS predicate (Transact-SQL)
- queries [full-text search], creating
- full-text queries [SQL Server], creating
ms.assetid: 537fa556-390e-4c88-9b8e-679848d94abc
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3963876ce326529fd2538adc2d303d218406a924
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013489"
---
# <a name="create-full-text-search-queries-visual-database-tools"></a>Criar consultas de pesquisa de texto completo (Visual Database Tools)
  Pesquisas de texto completo usam o predicado CONTAINS para localizar linhas que especificaram texto em uma determinada coluna. Pesquisas de texto completo somente são possíveis em colunas que têm índices de texto completo ativos. Se você tentar usar a cláusula CONTAINS em uma coluna que não tem um índice de texto completo ativo atualmente, receberá um erro. Para obter mais informações sobre índices de texto completo e a cláusula CONTAINS, consulte [Full-Text Search](../../relational-databases/search/full-text-search.md) e [contém &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql).  
  
### <a name="to-create-a-full-text-search-query"></a>Para criar uma consulta de pesquisa de texto completo  
  
1.  Abra uma consulta no Gerenciador de Soluções ou crie uma consulta nova.  
  
2.  Na cláusula WHERE da consulta, use a função CONTAINS para pesquisar uma coluna de texto completo.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte para tipos de consulta &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Tópicos de instruções de consultas e modos de exibição de design &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Executar operações básicas com consultas &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
