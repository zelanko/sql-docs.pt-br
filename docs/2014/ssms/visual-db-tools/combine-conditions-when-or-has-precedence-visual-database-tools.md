---
title: Combinar condições quando OR tem precedência (Ferramentas de Banco de Dados Visual) | Microsoft Docs
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
- OR operator
ms.assetid: b30f5ac9-25e7-4163-80ed-44e4bccb455d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 28203de42b3cdb4a033ce222c747df3e80da96f9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63224500"
---
# <a name="combine-conditions-when-or-has-precedence-visual-database-tools"></a>Combinar condições quando OR tem precedência (Visual Database Tools)
  Para vincular condições com OR e dar-lhes precedência sobre condições vinculadas com AND, é preciso repetir a condição AND em todas as condições OR.  
  
 Por exemplo, suponhamos que você pretenda localizar os funcionários que estão na empresa há mais de cinco anos, que ocupem cargos de nível mais baixo ou que estejam aposentados. Essa consulta requer três condições, uma condição única vinculada a duas condições adicionais com AND:  
  
-   Funcionários com data de contratação anterior a cinco anos e  
  
-   Funcionários com um nível de cargo 100 ou cujo status é "R" (aposentado).  
  
 O procedimento a seguir explica como criar esse tipo de consulta no Painel de Critérios.  
  
### <a name="to-combine-conditions-when-or-has-precedence"></a>Para combinar condições quando OR  tem precedência  
  
1.  No [Painel Critérios](visual-database-tools.md), adicione as colunas de dados a serem pesquisadas. Para pesquisar a mesma coluna usando duas ou mais condições vinculadas com AND, é preciso adicionar o nome da coluna de dados à grade uma vez para cada valor a ser pesquisado.  
  
2.  Crie as condições a serem vinculadas com OR digitando a primeira na coluna de grade **Filtro** e a segunda (e seguintes) em colunas **Ou...** separadas. Por exemplo, para vincular condições com OR que pesquisem as colunas `job_lvl` e `status` , digite `= 100` na coluna **Filtro** para `job_lvl` e `= 'R'` na coluna **Ou...** para `status`.  
  
     Digitar esses valores na grade produz a cláusula WHERE seguinte na instrução do Painel SQL:  
  
    ```  
    WHERE (job_lvl = 100) OR (status = 'R')  
    ```  
  
3.  Crie a condição AND inserindo-a uma vez para cada uma das condições OR. Coloque cada entrada na mesma coluna de grade como sendo a condição OR à qual ela corresponde. Por exemplo, para adicionar uma condição AND que pesquise a coluna `hire_date` e que se aplique a ambas as condições OR, digite `< '1/1/91'` na coluna Critérios e na coluna **Ou...** .  
  
     Digitar esses valores na grade produz a cláusula WHERE seguinte na instrução do Painel SQL:  
  
    ```  
    WHERE (job_lvl = 100) AND   
      (hire_date < '01/01/91' ) OR  
      (status = 'R') AND   
      (hire_date < '01/01/91' )  
    ```  
  
    > [!TIP]  
    >  Repita uma condição AND adicionando-a uma vez e usando os comandos **Recortar** e **Colar** do menu **Editar** para repeti-la em outras condições OR.  
  
 A cláusula WHERE, criada pelo Designer de Consulta e Exibição, equivale à seguinte cláusula WHERE, que usa parênteses para especificar a precedência de OR sobre AND:  
  
```  
WHERE (job_lvl = 100 OR status = 'R') AND  
   (hire_date < '01/01/91')  
```  
  
> [!NOTE]  
>  Se você digitar os critérios de pesquisa no formato mostrado anteriormente no [Painel SQL](sql-pane-visual-database-tools.md), mas depois fizer uma alteração na consulta no Painel Diagrama ou Critérios, o Designer de Consulta e Exibição recriará a instrução SQL para que corresponda ao formato em que a condição AND é explicitamente distribuída em ambas as condições OR.  
  
## <a name="see-also"></a>Consulte Também  
 [Convenções para combinar critérios de pesquisa no painel critérios &#40;Visual Database Tools&#41;](conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)   
 [Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)  
  
  
