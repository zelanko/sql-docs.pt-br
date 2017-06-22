---
title: "Especificar condições para grupos (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- HAVING clause, query groups
- group query conditions [SQL Server]
ms.assetid: 269ad9c5-3261-4526-badf-7be3c869f229
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 017e0e7937cd076da1cd700da7db298a1f289035
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="specify-conditions-for-groups-visual-database-tools"></a>Especificar condições para grupos (Visual Database Tools)
Você pode limitar os grupos exibidos em uma consulta especificando uma condição aplicável aos grupos como um todo – uma cláusula HAVING. Depois que os dados são agrupados e agregados, as condições na cláusula HAVING são aplicadas. Somente os grupos que atendem as condições são exibidos na consulta.  
  
Por exemplo, você pode desejar ver o preço médio de todos os livros de cada editor em uma tabela `titles` , mas somente se o preço médio exceder R$ 10,00. Nesse caso, você pode especificar uma cláusula HAVING com uma condição, como `AVG(price) > 10`.  
  
> [!NOTE]  
> Em algumas instâncias, você pode desejar excluir linhas individuais de grupos antes de aplicar uma condição a grupos como um todo. Para obter detalhes, veja [Usar cláusulas HAVING e WHERE na mesma consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/use-having-and-where-clauses-in-the-same-query-visual-database-tools.md).  
  
Você pode criar condições complexas para uma cláusula HAVING usando AND e OR para vincular condições. Para obter detalhes sobre como usar AND e OR em critérios de pesquisa, consulte [Especificar vários critérios de pesquisa para uma coluna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-one-column-visual-database-tools.md).  
  
### <a name="to-specify-a-condition-for-a-group"></a>Para especificar uma condição para um grupo  
  
1.  Especifique os grupos para a sua consulta. Para obter detalhes, veja [Agrupar linhas em resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md).  
  
2.  Se ainda não estiver no [Painel Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), adicione a coluna em que você deseja basear a condição. (Na maioria das vezes, a condição envolve uma coluna que já é um grupo ou uma coluna de resumo.) Você não pode usar uma coluna que não faça parte de uma função de agregação ou da cláusula GROUP BY.  
  
3.  Na coluna **Filtro**, especifique a condição que será aplicada ao grupo.  
  
    O [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) cria automaticamente uma cláusula HAVING na instrução no [Painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md), como no seguinte exemplo:  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
4.  Repita as etapas 2 e 3 para cada condição adicional que você deseja especificar.  
  
## <a name="see-also"></a>Consulte também  
[Classificar e agrupar resultados da consulta &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  

