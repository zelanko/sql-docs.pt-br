---
title: Especificar vários critérios de pesquisa para várias colunas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], multiple conditions
- multiple search conditions
- search conditions [SQL Server], multiple
- OR operator
- AND, Criteria pane
ms.assetid: 06617729-0d0b-4da2-9890-b7e2f5cdbc7b
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d916035a3ef7fc84103f2e2a94738effcc6cc6eb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37234356"
---
# <a name="specify-multiple-search-conditions-for-multiple-columns-visual-database-tools"></a>Especificar várias condições de pesquisa para diversas colunas (Visual Database Tools)
  Você pode expandir ou estreitar o escopo de sua consulta incluindo várias colunas de dados como parte de seu critério de pesquisa. Por exemplo, você pode querer:  
  
-   Pesquisar funcionários que já trabalham há mais de cinco anos na empresa ou que possuam determinados cargos.  
  
-   Pesquisar um livro publicado por um editor específico e que pertence ao setor de culinária.  
  
 Para criar uma consulta que pesquisa valores em duas (ou mais) colunas, você especifica uma condição OR. Para criar uma consulta que atenda todas as condições em duas (ou mais) colunas, você especifica uma condição AND.  
  
## <a name="specifying-an-or-condition"></a>Especificando um critério OR  
 Para criar várias condições vinculadas a OR, você coloca cada condição separada em uma coluna diferente do painel Critérios.  
  
#### <a name="to-specify-an-or-condition-for-two-different-columns"></a>Para especificar uma condição OR para duas colunas diferentes  
  
1.  No [Painel Critérios](visual-database-tools.md), adicione as colunas a serem pesquisadas.  
  
2.  Na coluna **Filtro** da primeira coluna a ser pesquisada, especifique a primeira condição.  
  
3.  Na coluna **Ou...** da segunda coluna de dados a ser pesquisada, especifique a segunda condição, deixando a coluna **Filtro** em branco.  
  
     O Designer de Consulta e Exibição cria uma cláusula WHERE que contém um critério OR, como o seguinte:  
  
    ```  
    SELECT job_lvl, hire_date  
    FROM employee  
    WHERE (job_lvl >= 200) OR   
      (hire_date < '01/01/1998')  
    ```  
  
4.  Repita as etapas 2 e 3 para cada condição adicional que você deseja adicionar. Utilize uma coluna **Ou...** diferente para cada condição nova.  
  
## <a name="specifying-an-and-condition"></a>Especificando um critério AND  
 Para pesquisar várias colunas de dados usando condições vinculadas a AND, coloque todas as condições na coluna **Filtro** da grade.  
  
#### <a name="to-specify-an-and-condition-for-two-different-columns"></a>Para especificar uma condição AND para duas colunas diferentes  
  
1.  No [Painel Critérios](visual-database-tools.md), adicione as colunas a serem pesquisadas.  
  
2.  Na coluna **Filtro** da primeira coluna de dados a ser pesquisada, especifique a primeira condição.  
  
3.  Na coluna **Filtro** da segunda coluna de dados, especifique a segunda condição.  
  
     O Designer de Consulta e Exibição cria uma cláusula WHERE que contém uma condição AND, igual a:  
  
    ```  
    SELECT pub_id, title  
    FROM titles  
    WHERE (pub_id = '0877') AND (title LIKE '%Cook%')  
    ```  
  
4.  Repita as etapas 2 e 3 para cada condição adicional que você deseja adicionar.  
  
## <a name="see-also"></a>Consulte também  
 [Combinar condições quando AND tem precedência &#40;Visual Database Tools&#41;](combine-conditions-when-and-has-precedence-visual-database-tools.md)   
 [Combinar condições quando OR tem precedência &#40;Visual Database Tools&#41;](combine-conditions-when-or-has-precedence-visual-database-tools.md)   
 [Convenções para combinar critérios de pesquisa no painel critérios &#40;Visual Database Tools&#41;](conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)   
 [Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)  
  
  
