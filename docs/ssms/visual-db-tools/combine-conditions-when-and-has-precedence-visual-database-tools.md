---
title: "Combinar condições quando AND tem precedência (Ferramentas de Banco de Dados Visual) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- AND, Criteria pane
ms.assetid: 450eb2eb-6ea3-405b-8dd2-1ff926c016e7
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a84b1997c18d5e23554dbb9f85e2c6baad4e9b58
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="combine-conditions-when-and-has-precedence-visual-database-tools"></a>Combinar condições quando AND tem precedência (Visual Database Tools)
Para combinar condições com AND, você adiciona a coluna duas vezes à consulta – uma vez para cada condição. Para combinar condições com OR, você coloca a primeira na coluna Filtro e as condições adicionais em uma coluna **Ou...** .  
  
Por exemplo, imagine que você deseja localizar funcionários que estão na empresa por mais de cinco anos em trabalhos de nível inferior ou funcionários com trabalhos de nível médio, independentemente da data de contratação. Essa consulta exige três condições, duas delas vinculadas a AND:  
  
-   Os funcionários com data de contratação anterior há cinco anos AND com um nível de trabalho de 100.  
  
    -ou-  
  
-   Funcionários com um nível de trabalho de 200.  
  
### <a name="to-combine-conditions-when-and-has-precedence"></a>Para combinar condições quando AND tem precedência  
  
1.  No [Painel Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), adicione as colunas de dados a serem pesquisadas. Para pesquisar a mesma coluna usando duas ou mais condições vinculadas com AND, é preciso adicionar o nome da coluna de dados à grade uma vez para cada valor a ser pesquisado.  
  
2.  Na coluna **Filtro** , digite todas as condições que deseja vincular a AND. Por exemplo, para vincular condições a AND que pesquisam as colunas `hire_date` e `job_lvl` , digite os valores `< '1/1/91'` e `= 100`, respectivamente, na coluna Filtro.  
  
    Essas entradas de grade produzem a seguinte cláusula WHERE na instrução no [Painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md):  
  
    ```  
    WHERE (hire_date < '01/01/91') AND  
      (job_lvl = 100)  
    ```  
  
3.  Na coluna de grade **Ou...** , digite as condições que você deseja vincular a OR. Por exemplo, para adicionar uma condição que pesquisa outro valor na coluna `job_lvl` , digite um valor adicional na coluna **Ou...** , como `= 200`.  
  
    A adição de um valor na coluna **Ou...** adiciona outra condição à cláusula WHERE na instrução no painel SQL:  
  
    ```  
    WHERE (hire_date < '01/01/91' ) AND  
      (job_lvl = 100) OR   
      (job_lvl = 200)  
    ```  
  
## <a name="see-also"></a>Consulte também  
[Combinar condições quando OR tem precedência (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
[Convenções para combinar critérios de pesquisa no painel de Critérios (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[Regras para inserção de valores de pesquisa (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Especificar critérios de pesquisa (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
