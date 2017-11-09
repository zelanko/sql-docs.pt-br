---
title: RENAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/13/2016
ms.prod: 
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 0907cfd9-33a6-4fa6-91da-7d6679fee878
caps.latest.revision: 15
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d58470957ab58085ddd6a733cf30dbc77ce7439a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="rename-transact-sql"></a>RENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Renomeia uma tabela criada pelo usuário em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Renomeia uma tabela criada pelo usuário ou o banco de dados em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
> [!NOTE]  
>  Para renomear um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssSDS](../../includes/sssds-md.md)] use o procedimento armazenado [sp_renamedb &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-renamedb-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for Azure SQL Data Warehouse  
  
-- Rename a table.  
RENAME OBJECT [ :: ]  [ [ database_name .  [schema_name ] ] . ] | [schema_name . ] ] table_name TO new_table_name  
[;]  
  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- Rename a table  
RENAME OBJECT [::] [ [ database_name . [ schema_name ] . ] | [ schema_name . ] ] table_name TO new_table_name  
[;]  
  
-- Rename a database  
RENAME DATABASE [::] database_name TO new_database_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 RENOMEAR O OBJETO [:]   
          [[*database_name* . [ *schema_name* ]. ] | [ *schema_name* . ]]*table_name* para *new_table_name*  
 **APLICA-SE A:**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)],  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Altere o nome de uma tabela definida pelo usuário. Especifique a tabela a ser renomeado com um uma, duas ou nome de três partes.    Especifique a nova tabela *new_table_name* como um nome de parte única.  
  
 RENOMEAR O BANCO DE DADOS [:]   
          [ *database_name* para *new_database_name*  
 **APLICA-SE A:**  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Alterar o nome de um banco de dados definido pelo usuário *database_name* para *new_database_name*.  Você não pode renomear um banco de dados para qualquer um desses [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]reservadas para nomes de banco de dados:  
  
-   mestre  
  
-   modelo  
  
-   msdb  
  
-   tempdb  
  
-   pdwtempdb1  
  
-   pdwtempdb2  
  
-   : DWConfiguration  
  
-   DWDiagnostics  
  
-   DWQueue  
  
## <a name="permissions"></a>Permissões  
 Essa permissão é necessária para executar este comando:  
  
-   **ALTER** permissão na tabela  
   
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
  
### <a name="cannot-rename-an-external-table-indexes-or-views"></a>Não é possível renomear uma tabela externa, índices ou exibições
Você não pode renomear uma tabela externa, índices ou exibições. Em vez de renomear, você pode descartar a tabela externa, índice ou exibição e, em seguida, recriá-la com o novo nome.

### <a name="cannot-rename-a-table-in-use"></a>Não é possível renomear uma tabela em uso  
 Você não pode renomear uma tabela ou banco de dados enquanto ele está em uso. Renomear uma tabela requer um bloqueio exclusivo na tabela. Se a tabela estiver em uso, você precisará encerrar sessões que usam a tabela. Para terminar uma sessão, você pode usar o comando KILL. Use KILL com cuidado, pois quando uma sessão é encerrada qualquer trabalho não confirmado será revertido. Sessões no SQL Data Warehouse são prefixadas por 'SID'. Você precisará incluir isso e o número de sessão ao invocar o comando KILL. Este exemplo exibe uma lista de sessões ativas ou ociosas e, em seguida, encerra a sessão 'SID1234'.  
  
### <a name="views-are-not-updated"></a>Modos de exibição não são atualizados.  
 Ao renomear um banco de dados, todas as exibições que usam o nome antigo do banco de dados se tornarão inválidas. Isso se aplica a modos de exibição dentro e fora do banco de dados. Por exemplo, se o banco de dados de vendas for renomeado, uma exibição que contém `SELECT * FROM Sales.dbo.table1` se tornarão inválidos. Para resolver isso, evite usar nomes de três partes em exibições ou atualizar os modos de exibição para o novo nome de banco de dados de referência.  
  
 Ao renomear uma tabela, os modos de exibição não são atualizados para o novo nome de tabela de referência. Cada modo de exibição, dentro ou fora do banco de dados, que referencia o nome da tabela antiga se tornarão inválido. Para resolver esse problema, você pode atualizar cada modo de exibição para o novo nome de tabela de referência.  
  
## <a name="locking"></a>Bloqueio  
 Renomear uma tabela tem um bloqueio compartilhado no objeto de banco de dados, um bloqueio compartilhado no objeto de esquema e um bloqueio exclusivo na tabela.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-rename-a-database"></a>A. Renomear um banco de dados  
 **Aplica-se a:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] somente    
  
 Este exemplo renomeia o banco de dados definido pelo usuário AdWorks para AdWorks2.  
  
```  
-- Rename the user defined database AdWorks  
RENAME DATABASE AdWorks to AdWorks2;  
  
```  
  
 Ao renomear uma tabela, todos os objetos e propriedades associadas à tabela são atualizadas para referenciar o novo nome de tabela. Por exemplo, tabela de definições, índices, restrições e permissões são atualizadas. Modos de exibição não são atualizados.  
  
### <a name="b-rename-a-table"></a>B. Renomear uma tabela  
 **APLICA-SE A:**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)],  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Este exemplo renomeia a tabela de clientes para Customer1.  
  
```  
-- Rename the customer table  
RENAME OBJECT Customer TO Customer1;  
  
RENAME OBJECT mydb.dbo.Customer TO Customer1;  
```  
  
 Ao renomear uma tabela, todos os objetos e propriedades associadas à tabela são atualizadas para referenciar o novo nome de tabela. Por exemplo, tabela de definições, índices, restrições e permissões são atualizadas. Modos de exibição não são atualizados.  
   
  
### <a name="c-move-a-table-to-a-different-schema"></a>C. Mover uma tabela para um esquema diferente  
 **APLICA-SE A:**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)],  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Se sua intenção for mover o objeto para um esquema diferente, use [ALTER SCHEMA &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-schema-transact-sql.md). Por exemplo, isso move o item de tabela do esquema de produto ao esquema dbo.  
  
```  
ALTER SCHEMA dbo TRANSFER OBJECT::product.item;  
```  
  
### <a name="d-terminate-sessions-before-renaming-a-table"></a>D. Encerrar sessões antes de renomear uma tabela  
 **APLICA-SE A:**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)],  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 É importante lembrar-se de que você não pode renomear uma tabela enquanto ela está em uso. Renomear uma tabela requer um bloqueio exclusivo na tabela. Se a tabela estiver em uso, você precisará encerrar a sessão usando a tabela. Para terminar uma sessão, você pode usar o comando KILL. Use KILL com cuidado, pois quando uma sessão é encerrada qualquer trabalho não confirmado será revertido. Sessões no SQL Data Warehouse são prefixadas por 'SID'. Você precisará incluir isso e o número de sessão ao invocar o comando KILL. Este exemplo exibe uma lista de sessões ativas ou ociosas e, em seguida, encerra a sessão 'SID1234'.  
  
```  
-- View a list of the current sessions  
SELECT session_id, login_name, status   
FROM sys.dm_pdw_exec_sessions   
WHERE status='Active' OR status='Idle';  
  
-- Terminate a session using the session_id.  
KILL 'SID1234';  
```  
  
  

