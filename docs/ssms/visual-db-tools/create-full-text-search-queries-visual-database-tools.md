---
description: Criar consultas de pesquisa de texto completo (Visual Database Tools)
title: Criar consultas de pesquisa de texto completo
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CONTAINS predicate (Transact-SQL)
- queries [full-text search], creating
- full-text queries [SQL Server], creating
ms.assetid: 537fa556-390e-4c88-9b8e-679848d94abc
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: b861cf926bdbc43fda8986be44dacb5652196b7a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88369892"
---
# <a name="create-full-text-search-queries-visual-database-tools"></a>Criar consultas de pesquisa de texto completo (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Pesquisas de texto completo usam o predicado CONTAINS para localizar linhas que especificaram texto em uma determinada coluna. Pesquisas de texto completo somente são possíveis em colunas que têm índices de texto completo ativos. Se você tentar usar a cláusula CONTAINS em uma coluna que não tem um índice de texto completo ativo atualmente, receberá um erro. Para obter mais informações sobre índices de texto completo e a cláusula CONTAINS, consulte [Pesquisa de texto completo (SQL Server)](../../relational-databases/search/full-text-search.md) e [CONTAINS (Transact-SQL)](https://msdn.microsoft.com/996c72fc-b1ab-4c96-bd12-946be9c18f84).  
  
### <a name="to-create-a-full-text-search-query"></a>Para criar uma consulta de pesquisa de texto completo  
  
1.  Abra uma consulta no Gerenciador de Soluções ou crie uma consulta nova.  
  
2.  Na cláusula WHERE da consulta, use a função CONTAINS para pesquisar uma coluna de texto completo.  
  
## <a name="see-also"></a>Consulte Também  
[Tipos de consulta com suporte &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Executar operações básicas com consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
