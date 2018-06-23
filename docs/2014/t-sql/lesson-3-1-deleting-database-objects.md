---
title: Excluindo objetos de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deleting database objects
ms.assetid: dbb94fdf-c85b-477b-8e84-f830d259bade
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 555c51cca7b853a39831eebbd736794b0f0ffd69
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007625"
---
# <a name="deleting-database-objects"></a>Excluindo objetos de bancos de dados
  Para remover todos os rastreamentos deste tutorial, você pode simplesmente excluir o banco de dados. No entanto, neste tópico, você passará pelas etapas para reverter todas as ações feitas durante o tutorial.  
  
### <a name="removing-permissions-and-objects"></a>Removendo permissões e objetos  
  
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
  
## <a name="return-to-sql-server-tools-portal"></a>Retorne ao portal Ferramentas do SQL Server  
 [Tutorial: Gravando instruções Transact-SQL](tutorial-writing-transact-sql-statements.md)  
  
## <a name="see-also"></a>Consulte também  
 [REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql)   
 [DROP USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-user-transact-sql)   
 [DROP LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-login-transact-sql)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-procedure-transact-sql)   
 [DROP VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-view-transact-sql)   
 [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql)   
 [DROP TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-table-transact-sql)   
 [DROP DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)  
  
  
