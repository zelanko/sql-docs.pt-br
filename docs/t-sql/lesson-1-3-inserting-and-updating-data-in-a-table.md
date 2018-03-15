---
title: Inserindo e atualizando dados em uma tabela (tutorial) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- inserting and updating data
ms.assetid: 514dc87a-b829-43b5-8fc8-1a400a260284
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: c64d3f2835e7c63b8c8e86946545641015188e29
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="lesson-1-3---inserting-and-updating-data-in-a-table"></a>Lição 1-3: Inserindo e atualizando dados em uma tabela (tutorial)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]Agora que você criou a tabela **Products**, está pronto para inserir dados na tabela usando a instrução INSERT. Depois que os dados forem inseridos, você alterará o conteúdo de uma linha usando uma instrução UPDATE. Você usará a cláusula WHERE da instrução UPDATE para restringir a atualização a uma única linha. As quatro instruções inserem os dados a seguir.  
  
|ProductID|ProductName|Price|ProductDescription|  
|-------------|---------------|---------|----------------------|  
|1|Clamp|12.48|Workbench clamp|  
|50|Screwdriver|3.17|Flat head|  
|75|Tire Bar||Tool for changing tires.|  
|3000|3mm Bracket|.52||  
  
A sintaxe básica é: INSERT, nome da tabela, lista de colunas, VALUES e uma lista de valores a serem inseridos. Os dois hifens antes de uma linha indicam que a linha é um comentário e o texto será ignorado pelo compilador. Neste caso, o comentário descreve uma variação admissível da sintaxe.  
  
### <a name="to-insert-data-into-a-table"></a>Para inserir dados em uma tabela  
  
1.  Execute a instrução a seguir para inserir uma linha na tabela `Products` que foi criada na tarefa anterior. Esta é a sintaxe básica.  
  
    ```  
    -- Standard syntax  
    INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
        VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
    GO  
  
    ```  
  
2.  A instrução a seguir mostra como você pode alterar a ordem na qual os parâmetros são fornecidos alternando o posicionamento de `ProductID` e `ProductName` na lista de campos (entre parênteses) e na lista de valores.  
  
    ```  
    -- Changing the order of the columns  
    INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
        VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
    GO  
  
    ```  
  
3.  A instrução a seguir demonstra que os nomes das colunas são opcionais, desde que os valores estejam listados na ordem correta. Esta sintaxe é comum, mas não é recomendada, pois possivelmente outras usuários terão dificuldade para compreender o código. `NULL` é especificado para a coluna `Price` porque o preço desse produto ainda não é conhecido.  
  
    ```  
    -- Skipping the column list, but keeping the values in order  
    INSERT dbo.Products  
        VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
    GO  
  
    ```  
  
4.  O nome de esquema é opcional, desde que você esteja acessando e alterando uma tabela em seu esquema padrão. Como a coluna `ProductDescription` permite valores nulos e nenhum valor está sendo fornecido, o nome de coluna `ProductDescription` e o valor podem ser descartados completamente da instrução.  
  
    ```  
    -- Dropping the optional dbo and dropping the ProductDescription column  
    INSERT Products (ProductID, ProductName, Price)  
        VALUES (3000, '3mm Bracket', .52)  
    GO  
    ```  
  
### <a name="to-update-the-products-table"></a>Para atualizar a tabela de produtos  
  
1.  Digite e execute a instrução `UPDATE` a seguir para alterar o `ProductName` do segundo produto de `Screwdriver`para `Flat Head Screwdriver`.  
  
    ```  
    UPDATE dbo.Products  
        SET ProductName = 'Flat Head Screwdriver'  
        WHERE ProductID = 50  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Lendo os dados em uma tabela &#40;Tutorial&#41;](../t-sql/lesson-1-4-reading-the-data-in-a-table.md)  
  
## <a name="see-also"></a>Consulte Também  
[INSERT &#40;Transact-SQL&#41;](../t-sql/statements/insert-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](../t-sql/queries/update-transact-sql.md)  
  
  
  
