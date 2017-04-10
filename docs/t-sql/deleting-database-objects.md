---
title: "Excluindo objetos de bancos de dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "excluindo objetos de bancos de dados"
ms.assetid: dbb94fdf-c85b-477b-8e84-f830d259bade
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Excluindo objetos de bancos de dados
Para remover todos os rastreamentos deste tutorial, você pode simplesmente excluir o banco de dados. No entanto, neste tópico, você passará pelas etapas para reverter todas as ações feitas durante o tutorial.  
  
### Removendo permissões e objetos  
  
1.  Antes de excluir objetos, tenha certeza de selecionar o banco de dados correto:  
  
    ```  
    USE TestData;  
    GO  
    ```  
  
2.  Use a instrução `REVOKE` para remover a permissão de execução para `Mary` no procedimento armazenado:  
  
    ```  
    REVOKE EXECUTE ON pr_Names FROM Mary;  
    GO  
  
    ```  
  
3.  Use a instrução `DROP` para remover a permissão de `Mary` para acessar o banco de dados `TestData` :  
  
    ```  
    DROP USER Mary;  
    GO  
  
    ```  
  
4.  Use a instrução `DROP` para remover a permissão de `Mary` para acessar esta instância do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]:  
  
    ```  
    DROP LOGIN [<computer_name>\Mary];  
    GO  
  
    ```  
  
5.  Use a instrução `DROP` para remover ao procedimento armazenado `pr_Names`:  
  
    ```  
    DROP PROC pr_Names;  
    GO  
  
    ```  
  
6.  Use a instrução `DROP` para remover a exibição `vw_Names`:  
  
    ```  
    DROP View vw_Names;  
    GO  
  
    ```  
  
7.  Use a instrução `DELETE` para remover todas as linhas da tabela `Products` :  
  
    ```  
    DELETE FROM Products;  
    GO  
  
    ```  
  
8.  Use a instrução `DROP` para remover a tabela `Products` :  
  
    ```  
    DROP Table Products;  
    GO  
  
    ```  
  
9. Você não pode remover o banco de dados `TestData` durante seu acesso; portanto, primeiro alterne o contexto para outro banco de dados e, em seguida, use a instrução `DROP` para remover o banco de dados `TestData` :  
  
    ```  
    USE MASTER;  
    GO  
    DROP DATABASE TestData;  
    GO  
  
    ```  
  
Isso conclui o tutorial Escrevendo Instruções [!INCLUDE[tsql](../includes/tsql-md.md)] . Lembre-se, este tutorial é uma visão geral e não descreve todas as opções de instruções que são usadas. Projetar e criar uma estrutura de banco de dados eficiente e configurar acesso seguro aos dados requer um banco de dados mais complexo do que o mostrado neste tutorial.  
  
## Retorne ao portal Ferramentas do SQL Server  
[Tutorial: Gravando instruções Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
## Consulte também  
[REVOKE &#40;Transact-SQL&#41;](../t-sql/statements/revoke-transact-sql.md)  
[DROP USER &#40;Transact-SQL&#41;](../t-sql/statements/drop-user-transact-sql.md)  
[DROP LOGIN &#40;Transact-SQL&#41;](../t-sql/statements/drop-login-transact-sql.md)  
[DROP PROCEDURE &#40;Transact-SQL&#41;](../t-sql/statements/drop-procedure-transact-sql.md)  
[DROP VIEW &#40;Transact-SQL&#41;](../t-sql/statements/drop-view-transact-sql.md)  
[DELETE &#40;Transact-SQL&#41;](../t-sql/statements/delete-transact-sql.md)  
[DROP TABLE &#40;Transact-SQL&#41;](../t-sql/statements/drop-table-transact-sql.md)  
[DROP DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/drop-database-transact-sql.md)  
  
  
  
