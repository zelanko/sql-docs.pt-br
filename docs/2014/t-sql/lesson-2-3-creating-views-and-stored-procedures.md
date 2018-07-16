---
title: Criando exibições e procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- creating views and stored procedures
ms.assetid: 53a0426d-07d8-4b7c-aa21-22632753bad8
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: f4ff7d53cc51d8995cdf348742299daedf574d26
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37301286"
---
# <a name="creating-views-and-stored-procedures"></a>criando exibições e procedimentos armazenados
  Agora que a Mary pode acessar o banco de dados **TestData** , talvez convenha criar alguns objetos de banco de dados, como uma exibição e um procedimento armazenado, e conceder a Mary acesso a eles. Uma exibição é uma instrução SELECT armazenada e um procedimento armazenado é uma ou mais instruções [!INCLUDE[tsql](../includes/tsql-md.md)] executadas como um lote.  
  
 Exibições são tabelas do tipo para consultas e não aceitam parâmetros. Procedimentos armazenados são mais complexos que exibições. Procedimentos armazenados podem ter parâmetros de entrada e saída e conter instruções para controlar o fluxo do código, como instruções IF e WHILE. É uma boa prática de programação usar procedimentos armazenados para todas as ações repetitivas no banco de dados.  
  
 Neste exemplo, você usará CREATE VIEW para criar uma exibição que seleciona apenas duas das colunas na tabela **Products** . Em seguida, você usará CREATE PROCEDURE para criar um procedimento armazenado que aceita um parâmetro de preço e retorna apenas produtos que custam menos do que o valor do parâmetro especificado.  
  
### <a name="to-create-a-view"></a>Para criar uma exibição  
  
1.  Execute a instrução a seguir para criar uma exibição muito simples que executa uma instrução SELECT e retorna os nomes e preços de nossos produtos para o usuário.  
  
    ```  
    CREATE VIEW vw_Names  
       AS  
       SELECT ProductName, Price FROM Products;  
    GO  
  
    ```  
  
### <a name="test-the-view"></a>Teste a exibição  
  
1.  Exibições são tratadas como tabelas. Use uma instrução `SELECT` para acessar uma exibição.  
  
    ```  
    SELECT * FROM vw_Names;  
    GO  
  
    ```  
  
### <a name="to-create-a-stored-procedure"></a>Para criar um procedimento armazenado  
  
1.  A instrução a seguir cria um `pr_Names`de nome de procedimento armazenado, aceita um parâmetro de entrada denominado `@VarPrice` do tipo de dados `money`. O procedimento armazenado imprime a instrução `Products less than` concatenada com o parâmetro de entrada que é alterado do tipo de dados `money` para o tipo de dados de caractere `varchar(10)` . Depois, o procedimento executa uma instrução `SELECT` na exibição, passando o parâmetro de entrada como parte da cláusula `WHERE` . Isso retorna todos os produtos que custam menos do que o valor do parâmetro de entrada.  
  
    ```  
    CREATE PROCEDURE pr_Names @VarPrice money  
       AS  
       BEGIN  
          -- The print statement returns text to the user  
          PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
          -- A second statement starts here  
          SELECT ProductName, Price FROM vw_Names  
                WHERE Price < @varPrice;  
       END  
    GO  
  
    ```  
  
### <a name="test-the-stored-procedure"></a>Testar o procedimento armazenado  
  
1.  Para testar o procedimento armazenado, digite e execute a instrução a seguir. O procedimento deve retornar os nomes dos dois produtos inseridos na tabela `Products` , na Lição 1, com um preço menor que `10.00`.  
  
    ```  
    EXECUTE pr_Names 10.00;  
    GO  
  
    ```  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Conceder acesso a um objeto de banco de dados](lesson-2-4-granting-access-to-a-database-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
