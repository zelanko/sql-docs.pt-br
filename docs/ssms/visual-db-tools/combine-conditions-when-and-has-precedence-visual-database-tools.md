---
description: Combinar condições quando AND tem precedência (Visual Database Tools)
title: Combinar condições quando AND tiver precedência
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- AND, Criteria pane
ms.assetid: 450eb2eb-6ea3-405b-8dd2-1ff926c016e7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 6ad323d3efdbb760b315c16d94752d8c658fdab5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468472"
---
# <a name="combine-conditions-when-and-has-precedence-visual-database-tools"></a>Combinar condições quando AND tem precedência (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Para combinar condições com AND, você adiciona a coluna duas vezes à consulta – uma vez para cada condição. Para combinar condições com OR, você coloca a primeira na coluna Filtro e as condições adicionais em uma coluna **Ou...** .  
  
Por exemplo, imagine que você deseja localizar funcionários que estão na empresa por mais de cinco anos em trabalhos de nível inferior ou funcionários com trabalhos de nível médio, independentemente da data de contratação. Essa consulta exige três condições, duas delas vinculadas a AND:  
  
-   Os funcionários com data de contratação anterior há cinco anos AND com um nível de trabalho de 100.  
  
    - ou -  
  
-   Funcionários com um nível de trabalho de 200.  
  
## <a name="to-combine-conditions-when-and-has-precedence"></a>Para combinar condições quando AND tem precedência  
  
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
  
## <a name="see-also"></a>Consulte Também

[Combinar condições quando OR tem precedência](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
[Convenções para combinar condições de pesquisa no painel Critérios](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[Regras para inserir valores de pesquisa](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Especificar critérios de pesquisa](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)
