---
title: Lendo os dados em uma tabela (Tutorial) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- reading data in a table
ms.assetid: 532232c9-3d41-45cd-9150-de67a1cbfcf5
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b4f808355e765cb54fa973fce76af98ae56dbdc5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-1-4---reading-the-data-in-a-table"></a>Lição 1-4-lendo os dados em uma tabela
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
|[Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md)|[Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)|  
|[Funções matemáticas &#40;Transact-SQL&#41;](../t-sql/functions/mathematical-functions-transact-sql.md)|[Funções de texto e imagem &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Resumo: Criando objetos de banco de dados](../t-sql/lesson-1-5-summary-creating-database-objects.md)  
  
## <a name="see-also"></a>Consulte também  
[SELECT &#40;Transact-SQL&#41;](../t-sql/queries/select-transact-sql.md)  
  
  
  

