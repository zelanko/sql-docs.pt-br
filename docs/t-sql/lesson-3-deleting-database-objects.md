---
title: 'Tutorial do T-SQL: excluir objetos de banco de dados | Microsoft Docs'
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- deleting database objects
ms.assetid: ecf26dd5-4535-4ed6-86fc-c73f9d9dedec
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7381d5c4786fcd67a69029e158a0a931b8e8f628
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43071519"
---
# <a name="lesson-3-delete-database-objects"></a>Lição 3: excluir objetos de banco de dados
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
Esta lição curta remove os objetos que você criou nas Lições 1 e 2 e, em seguida, libera o banco de dados.  
  
Antes de excluir objetos, tenha certeza de selecionar o banco de dados correto:
  
  ```sql  
  USE TestData;  
  GO  
  ```  

## <a name="revoke-stored-procedure-permissions"></a>Revogar permissões de procedimento armazenado
  
Use a instrução `REVOKE` para remover a permissão de execução para `Mary` no procedimento armazenado:
  
  ```sql  
  REVOKE EXECUTE ON pr_Names FROM Mary;  
  GO  
  ```  
  
## <a name="drop-permissions"></a>Remover permissões

1. Use a instrução `DROP` para remover a permissão de `Mary` para acessar o banco de dados `TestData` :
  
  ```sql  
  DROP USER Mary;  
  GO  
  ```  


2. Use a instrução `DROP` para remover a permissão de `Mary` para acessar esta instância do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]:
  
  ```sql  
    DROP LOGIN [<computer_name>\Mary];  
    GO   
  ```  
  
3.   Use a instrução `DROP` para remover ao procedimento armazenado `pr_Names`:  
  
    ```sql  
    DROP PROC pr_Names;  
    GO  
    ```  
  
6.  Use a instrução `DROP` para remover a exibição `vw_Names`:  
  
    ```sql  
    DROP VIEW vw_Names;  
    GO  
  
    ```  

## <a name="delete-table"></a>Excluir tabela
  
1. Use a instrução `DELETE` para remover todas as linhas da tabela `Products` :  
  
    ```sql  
    DELETE FROM Products;  
    GO  
    ```  
  
2.  Use a instrução `DROP` para remover a tabela `Products` :  
  
    ```sql  
    DROP TABLE Products;  
    GO    
    ```  

## <a name="remove-database"></a>Remover banco de dados
  
Você não pode remover o banco de dados `TestData` durante seu acesso; portanto, primeiro alterne o contexto para outro banco de dados e, em seguida, use a instrução `DROP` para remover o banco de dados `TestData` :  
  
  ```sql  
  USE MASTER;  
  GO  
  DROP DATABASE TestData;  
  GO   
  ```  
  
Isso conclui o tutorial Escrevendo Instruções [!INCLUDE[tsql](../includes/tsql-md.md)] . Lembre-se, este tutorial é uma visão geral e não descreve todas as opções de instruções que são usadas. Projetar e criar uma estrutura de banco de dados eficiente e configurar acesso seguro aos dados requer um banco de dados mais complexo do que o mostrado neste tutorial.  

  
  
