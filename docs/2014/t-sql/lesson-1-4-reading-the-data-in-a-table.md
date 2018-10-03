---
title: Lendo os dados em uma tabela (tutorial) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- reading data in a table
ms.assetid: 532232c9-3d41-45cd-9150-de67a1cbfcf5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 0649e167ebaa90267422594ccd193ba468838e6f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48182006"
---
# <a name="reading-the-data-in-a-table-tutorial"></a>Lendo os dados em uma tabela (tutorial)
  Use a instrução SELECT para ler os dados em uma tabela. A instrução SELECT é um das instruções [!INCLUDE[tsql](../includes/tsql-md.md)] mais importantes e há muitas variações na sintaxe. Para este tutorial, você trabalhará com cinco versões simples.  
  
### <a name="to-read-the-data-in-a-table"></a>Ler os dados em uma tabela  
  
1.  Digite e execute as instruções seguintes para ler os dados na tabela `Products` .  
  
    ```  
    -- The basic syntax for reading data from a single table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
    GO  
  
    ```  
  
2.  Você pode usar um asterisco para selecionar todas as colunas na tabela. Isso é frequentemente usado em consultas ad hoc. Você deve fornecer a lista de colunas em seu código permanente para que a instrução retorne as colunas previstas, mesmo se uma coluna nova for adicionada posteriormente à tabela.  
  
    ```  
    -- Returns all columns in the table  
    -- Does not use the optional schema, dbo  
    SELECT * FROM Products  
    GO  
  
    ```  
  
3.  Você pode omitir colunas que não deseja retornar. As colunas serão retornadas na ordem em que são listadas.  
  
    ```  
    -- Returns only two of the columns from the table  
    SELECT ProductName, Price  
        FROM dbo.Products  
    GO  
  
    ```  
  
4.  Use uma cláusula `WHERE` para limitar as linhas que serão retornadas ao usuário.  
  
    ```  
    -- Returns only two of the records in the table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
        WHERE ProductID < 60  
    GO  
  
    ```  
  
5.  Você pode trabalhar com os valores nas colunas à medida que elas forem retornadas. O exemplo seguinte executa uma operação matemática na coluna `Price` . Colunas que foram alteradas dessa maneira não terão um nome, a menos que você forneça um, usando a palavra-chave `AS` .  
  
    ```  
    -- Returns ProductName and the Price including a 7% tax  
    -- Provides the name CustomerPays for the calculated column  
    SELECT ProductName, Price * 1.07 AS CustomerPays  
        FROM dbo.Products  
    GO  
    ```  
  
## <a name="functions-that-are-useful-in-a-select-statement"></a>Funções úteis em uma instrução SELECT  
 Para obter informações sobre algumas funções que você pode usar para trabalhar com instruções SELECT, consulte os seguintes tópicos:  
  
|||  
|-|-|  
|[Funções de cadeia de caracteres &#40;Transact-SQL&#41;](/sql/t-sql/functions/string-functions-transact-sql)|[Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)|  
|[Funções matemáticas &#40;Transact-SQL&#41;](/sql/t-sql/functions/mathematical-functions-transact-sql)|[Funções de texto e imagem &#40;Transact-SQL&#41;](/sql/t-sql/functions/text-and-image-functions-textptr-transact-sql)|  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Resumo: Criando objetos de banco de dados](lesson-1-5-summary-creating-database-objects.md)  
  
## <a name="see-also"></a>Consulte também  
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)  
  
  
