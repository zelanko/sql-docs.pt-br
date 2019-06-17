---
title: Especificar condições para grupos (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- HAVING clause, query groups
- group query conditions [SQL Server]
ms.assetid: 269ad9c5-3261-4526-badf-7be3c869f229
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc0f9319e4d598548111b44b1a10542773a7daa4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049124"
---
# <a name="specify-conditions-for-groups-visual-database-tools"></a>Especificar condições para grupos (Visual Database Tools)
  Você pode limitar os grupos exibidos em uma consulta especificando uma condição aplicável aos grupos como um todo, ou seja, uma cláusula HAVING. Depois que os dados são agrupados e agregados, as condições na cláusula HAVING são aplicadas. Somente os grupos que atendem as condições são exibidos na consulta.  
  
 Por exemplo, você pode desejar ver o preço médio de todos os livros de cada editor em uma tabela `titles` , mas somente se o preço médio exceder R$ 10,00. Nesse caso, você pode especificar uma cláusula HAVING com uma condição, como `AVG(price) > 10`.  
  
> [!NOTE]  
>  Em algumas instâncias, você pode desejar excluir linhas individuais de grupos antes de aplicar uma condição a grupos como um todo. Para obter detalhes, veja [Usar cláusulas HAVING e WHERE na mesma consulta &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
 Você pode criar condições complexas para uma cláusula HAVING usando AND e OR para vincular condições. Para obter detalhes sobre como usar AND e OR em critérios de pesquisa, consulte [Especificar vários critérios de pesquisa para uma coluna &#40;Visual Database Tools&#41;](specify-multiple-search-conditions-for-one-column-visual-database-tools.md).  
  
### <a name="to-specify-a-condition-for-a-group"></a>Para especificar uma condição para um grupo  
  
1.  Especifique os grupos para a sua consulta. Para obter detalhes, veja [Agrupar linhas em resultados da consulta &#40;Visual Database Tools&#41;](group-rows-in-query-results-visual-database-tools.md).  
  
2.  Se ainda não estiver no [Painel Critérios](criteria-pane-visual-database-tools.md), adicione a coluna em que você deseja basear a condição. (Na maioria das vezes, a condição envolve uma coluna que já é um grupo ou uma coluna de resumo.) Você não pode usar uma coluna que não faça parte de uma função de agregação ou da cláusula GROUP BY.  
  
3.  Na coluna **Filtro**, especifique a condição que será aplicada ao grupo.  
  
     O [Designer de Consulta e Exibição](query-and-view-designer-tools-visual-database-tools.md) cria automaticamente uma cláusula HAVING na instrução no [Painel SQL](sql-pane-visual-database-tools.md), como no seguinte exemplo:  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
  
    ```  
  
4.  Repita as etapas 2 e 3 para cada condição adicional que você deseja especificar.  
  
## <a name="see-also"></a>Consulte também  
 [Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)  
  
  
