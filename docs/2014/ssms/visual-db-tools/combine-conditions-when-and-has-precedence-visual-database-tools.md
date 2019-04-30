---
title: Combinar condições quando AND tem precedência (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- AND, Criteria pane
ms.assetid: 450eb2eb-6ea3-405b-8dd2-1ff926c016e7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4d0a0bcb7115255c3c6b3750cd930e7d06b9e2df
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225808"
---
# <a name="combine-conditions-when-and-has-precedence-visual-database-tools"></a>Combinar condições quando AND tem precedência (Visual Database Tools)
  Para combinar condições com AND, você adiciona a coluna duas vezes à consulta – uma vez para cada condição. Para combinar condições com OR, você coloca a primeira na coluna Filtro e as condições adicionais em uma coluna **Ou...** .  
  
 Por exemplo, imagine que você deseja localizar funcionários que estão na empresa por mais de cinco anos em trabalhos de nível inferior ou funcionários com trabalhos de nível médio, independentemente da data de contratação. Essa consulta exige três condições, duas delas vinculadas a AND:  
  
-   Os funcionários com data de contratação anterior há cinco anos AND com um nível de trabalho de 100.  
  
     -ou-  
  
-   Funcionários com um nível de trabalho de 200.  
  
### <a name="to-combine-conditions-when-and-has-precedence"></a>Para combinar condições quando AND tem precedência  
  
1.  No [Painel Critérios](visual-database-tools.md), adicione as colunas de dados a serem pesquisadas. Para pesquisar a mesma coluna usando duas ou mais condições vinculadas com AND, é preciso adicionar o nome da coluna de dados à grade uma vez para cada valor a ser pesquisado.  
  
2.  Na coluna **Filtro** , digite todas as condições que deseja vincular a AND. Por exemplo, para vincular condições a AND que pesquisam as colunas `hire_date` e `job_lvl` , digite os valores `< '1/1/91'` e `= 100`, respectivamente, na coluna Filtro.  
  
     Essas entradas de grade produzem a seguinte cláusula WHERE na instrução no [Painel SQL](sql-pane-visual-database-tools.md):  
  
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
 [Combinar condições quando OR tem precedência &#40;Visual Database Tools&#41;](combine-conditions-when-or-has-precedence-visual-database-tools.md)   
 [Convenções para combinar critérios de pesquisa no painel critérios &#40;Visual Database Tools&#41;](conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)   
 [Regras para inserção de valores de pesquisa &#40;Visual Database Tools&#41;](rules-for-entering-search-values-visual-database-tools.md)   
 [Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)  
  
  
