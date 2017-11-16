---
title: Recolher grupos de linhas (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- group collapsing [SQL Server]
- collapsing rows
- row collapsing [SQL Server]
ms.assetid: 7338dad0-965d-44ba-8c1a-b993acb7156d
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 11ab34e9c5651be1dc771d71a738f49bb230262a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="collapse-groups-of-rows-visual-database-tools"></a>Recolher grupos de linhas (Visual Database Tools)
Você pode criar um resultado de consulta no qual cada linha de resultado corresponda a um grupo inteiro de linhas dos dados originais. Existem várias coisas a serem levadas em consideração ao recolher linhas:  
  
-   **Você pode eliminar linhas duplicadas** Algumas consultas podem criar conjuntos de resultados nos quais são exibidas várias linhas idênticas. Por exemplo, você pode criar um conjunto de resultados no qual cada linha contém o nome da cidade e do estado de uma cidade que contém um autor – mas se uma cidade contiver vários autores, haverá várias linhas idênticas. O SQL resultante pode ter esta aparência:  
  
    ```  
    SELECT city, state  
    FROM authors  
    ```  
  
    O conjunto de resultados gerado pela consulta anterior não é muito útil. Se uma cidade contiver quatro autores, o conjunto de resultados incluirá quatro linhas idênticas. Considerando que o conjunto de resultados não inclui nenhuma coluna além de cidade e estado, não há meios de distinguir as linhas idênticas umas das outras. Um modo para evitar tais linhas duplicadas é incluir colunas adicionais que podem diferenciar as linhas. Por exemplo, se você incluir o nome de autor, cada linha será diferente (contanto que nenhum autor com o mesmo nome viva na mesma cidade). O SQL resultante pode ter esta aparência:  
  
    ```  
    SELECT city, state, fname, minit, lname  
    FROM authors  
    ```  
  
    Claro, a consulta anterior elimina o sintoma, mas não resolve realmente o problema. Ou seja, o conjunto de resultados não tem linhas duplicadas, mas não é mais um conjunto de resultados sobre cidades. Para eliminar linhas duplicadas no conjunto de resultados original e cada linha ainda descrever uma cidade, você pode criar uma consulta que só retorne linhas distintas. O SQL resultante pode ter esta aparência:  
  
    ```  
    SELECT DISTINCT city, state  
    FROM authors  
    ```  
  
    Para obter detalhes sobre a eliminação de duplicatas, consulte [Excluir linhas duplicadas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/exclude-duplicate-rows-visual-database-tools.md).  
  
-   **Você pode calcular em grupos de linhas** Ou seja, você pode resumir as informações em grupos de linhas. Por exemplo, você pode criar um conjunto de resultados no qual cada linha contém o nome da cidade e do estado de uma cidade que contém um autor, mais uma contagem do número de autores que moram nessa cidade. O SQL resultante pode ter esta aparência:  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ```  
  
    Para obter detalhes sobre como calcular em grupos de linhas, consulte [Resumir resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md) e [Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md).  
  
-   **Você pode utilizar critérios de seleção para incluir grupos de linhas** Por exemplo, você pode criar um conjunto de resultados no qual cada linha contém o nome da cidade e do estado que contém vários autores, mais uma contagem do número de autores contidos naquela cidade. O SQL resultante pode ter esta aparência:  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    HAVING COUNT(*) > 1  
    ```  
  
    Para obter detalhes sobre como aplicar critérios de seleção em grupos de linhas, consulte [Especificar condições para grupos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-conditions-for-groups-visual-database-tools.md) e [Usar as cláusulas HAVING e WHERE na mesma consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/use-having-and-where-clauses-in-the-same-query-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte também  
[Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
