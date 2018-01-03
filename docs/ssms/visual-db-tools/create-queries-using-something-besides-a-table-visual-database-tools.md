---
title: "Criar consultas usando algo além de uma tabela | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user-defined functions [SQL Server], queries
- queries [SQL Server], creating
ms.assetid: 8e4a1f0a-8a42-4733-be8d-e21d6dbddb33
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc1923dcca1052c3c0bcdc2d1ba9abfb7935803a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="create-queries-using-something-besides-a-table-visual-database-tools"></a>Criar consultas usando algo além de uma tabela (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Sempre que você escreve uma consulta de recuperação, você articula as colunas e as linhas desejadas e nas quais o processador de consulta deve procurar os dados originais. Tipicamente, esses dados originais consistem em uma tabela ou várias tabelas unidas. Mas os dados originais podem vir de fontes diferentes de tabelas. Na realidade, podem vir de exibições, consultas, sinônimos ou funções definidas pelo usuário que retornam uma tabela.  
  
## <a name="using-a-view-in-place-of-a-table"></a>Usando uma exibição no lugar de uma tabela  
Você pode selecionar linhas de uma exibição. Por exemplo, suponha que o banco de dados inclui uma exibição chamada "ExpensiveBooks" na qual cada linha descreve um título cujo preço excede 19,99. A definição da exibição pode ter esta aparência:  
  
```  
SELECT *  
FROM titles  
WHERE price > 19.99  
```  
  
Você pode selecionar os livros caros de psicologia selecionando apenas os livros de psicologia da exibição ExpensiveBooks. O SQL resultante pode ter esta aparência:  
  
```  
SELECT *  
FROM ExpensiveBooks  
WHERE type = 'psychology'  
```  
  
Semelhantemente, uma exibição pode participar de uma operação JOIN. Por exemplo, você pode achar as vendas de livros caros unindo somente a tabela de vendas à exibição ExpensiveBooks. O SQL resultante pode ter esta aparência:  
  
```  
SELECT *  
FROM sales   
         INNER JOIN   
         ExpensiveBooks   
         ON sales.title_id   
         =  ExpensiveBooks.title_id  
```  
  
Para obter mais informações sobre como adicionar um modo de exibição a uma consulta, veja [Adicionar tabelas a consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md).  
  
## <a name="using-a-query-in-place-of-a-table"></a>Usando uma consulta no lugar de uma tabela  
Você pode selecionar linhas de uma consulta. Por exemplo, suponha você já escreveu uma consulta que recupera títulos e identificadores dos livros com coautoria – os livros com mais de um autor. O SQL pode ter esta aparência:  
  
```  
SELECT   
     titles.title_id, title, type  
FROM   
     titleauthor   
         INNER JOIN  
         titles   
         ON titleauthor.title_id   
         =  titles.title_id   
GROUP BY   
     titles.title_id, title, type  
HAVING COUNT(*) > 1  
```  
  
Depois, você pode escrever outra consulta compilada nesse resultado. Por exemplo, é possível escrever uma consulta que recupera os livros de psicologia com coautoria. Para escrever essa consulta nova, você pode usar a consulta existente como fonte de dados da nova consulta. O SQL resultante pode ter esta aparência:  
  
```  
SELECT   
    title  
FROM   
    (  
    SELECT   
        titles.title_id,   
        title,   
        type  
    FROM   
        titleauthor   
            INNER JOIN  
            titles   
            ON titleauthor.title_id   
            =  titles.title_id   
    GROUP BY   
        titles.title_id,   
        title,   
        type  
    HAVING COUNT(*) > 1  
    )   
    co_authored_books  
WHERE     type = 'psychology'  
```  
  
O texto enfatizado mostra a consulta existente usada como fonte de dados da nova consulta. Note que a nova consulta usa um alias ("co_authored_books") para a consulta existente. Para obter mais informações sobre aliases, consulte [Criar aliases de tabela &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md) e [Criar aliases de coluna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
Da mesma forma, uma consulta pode participar de uma operação JOIN. Por exemplo, você pode encontrar as vendas de livros caros com coautoria unindo somente a exibição ExpensiveBooks à consulta para recuperar a consulta de livros com coautoria. O SQL resultante pode ter esta aparência:  
  
```  
SELECT   
    ExpensiveBooks.title  
FROM   
    ExpensiveBooks   
        INNER JOIN  
        (  
        SELECT   
            titles.title_id,   
            title,   
            type  
        FROM   
            titleauthor   
                INNER JOIN  
                titles   
                ON titleauthor.title_id   
                =  titles.title_id   
        GROUP BY   
            titles.title_id,   
            title,   
            type  
        HAVING COUNT(*) > 1  
        )  
```  
  
Para obter mais informações sobre como adicionar uma consulta a uma consulta, veja [Adicionar tabelas a consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md).  
  
## <a name="using-a-user-defined-function-in-place-of-a-table"></a>Usando uma função definida pelo usuário no lugar de uma tabela  
No SQL Server 2000 ou superior, você pode criar uma função definida pelo usuário que retorna uma tabela. Tais funções são úteis para executar lógica complexa ou de procedimento.  
  
Por exemplo, suponha que a tabela de funcionários contenha uma coluna adicional, employee.manager_emp_id, e que exista uma chave estrangeira de manager_emp_id a employee.emp_id. Dentro de cada linha da tabela de funcionários, a coluna manager_emp_id indica o chefe do funcionário. Mais precisamente, indica a emp_id do chefe do funcionário. Você pode criar uma função definida pelo usuário que retorna a tabela contendo uma linha para cada funcionário que trabalha em uma determinada hierarquia organizacional de gerenciamento de alto nível. Você poderia chamar a função fn_GetWholeTeam e projetar isto para aceitar uma variável de entrada – a emp_id do administrador cuja equipe você quer recuperar.  
  
Você pode escrever uma consulta que use a função fn_GetWholeTeam como uma fonte de dados. O SQL resultante pode ter esta aparência:  
  
```  
SELECT *   
FROM   
     fn_GetWholeTeam ('VPA30890F')  
```  
  
"VPA30890F" é a emp_id do gerente cuja organização você quer recuperar. Para obter mais informações sobre como adicionar uma função definida pelo usuário a uma consulta, veja [Adicionar tabelas a consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md). Para uma descrição completa de funções definidas pelo usuário, consulte [Funções definidas pelo usuário](http://msdn.microsoft.com/en-us/d7ddafab-f5a6-44b0-81d5-ba96425aada4).  
  
