---
title: RENAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 0907cfd9-33a6-4fa6-91da-7d6679fee878
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 9ba9202ae949122d83c2690e62a645246b7796bb
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="rename-transact-sql"></a>RENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Renomeia uma tabela criada pelo usuário no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Renomeia uma tabela ou um banco de dados criado pelo usuário em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
> [!NOTE]  
>  Para renomear um banco de dados no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], use [ALTER DATABASE (SQL Data Warehouse do Azure](alter-database-azure-sql-data-warehouse.md).  Para renomear um banco de dados no Banco de Dados SQL do Azure, use a instrução [ALTER DATABASE (Banco de Dados SQL do Azure)](alter-database-azure-sql-database.md). Para renomear um banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o procedimento armazenado [sp_renamedb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-renamedb-transact-sql.md).
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for Azure SQL Data Warehouse  
  
-- Rename a table.  
RENAME OBJECT [::] [ [ database_name .  [schema_name ] ] . ] | [schema_name . ] ] table_name TO new_table_name  
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
 RENAME OBJECT [::] [ [*database_name*. [ *schema_name* ]. ] | [ *schema_name* . ] ]*table_name* TO *new_table_name*  
 **APLICA-SE A:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Altere o nome de uma tabela definida pelo usuário. Especifique a tabela a ser renomeada com um nome de uma, duas ou três partes.    Especifique a nova tabela *new_table_name* como um nome de uma parte.  
  
 RENAME DATABASE [::] [ *database_name* TO *new_database_name*  
 **APLICA-SE A:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Altere o nome de um banco de dados definido pelo usuário de *database_name* para *new_database_name*.  Não é possível renomear um banco de dados para qualquer um destes nomes de banco de dados reservados[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]:  
  
-   master  
  
-   modelo  
  
-   msdb  
  
-   tempdb  
  
-   pdwtempdb1  
  
-   pdwtempdb2  
  
-   DWConfiguration  
  
-   DWDiagnostics  
  
-   DWQueue  
  
## <a name="permissions"></a>Permissões  
 Para executar esse comando, é necessário ter esta permissão:  
  
-   Permissão **ALTER** na tabela  
   
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
  
### <a name="cannot-rename-an-external-table-indexes-or-views"></a>Não é possível renomear uma tabela externa, índices ou exibições
Não é possível renomear uma tabela externa, índices ou exibições. Em vez de renomeá-la, você pode remover a tabela externa, o índice ou a exibição e, em seguida, recriá-la com o novo nome.

### <a name="cannot-rename-a-table-in-use"></a>Não é possível renomear uma tabela em uso  
 Não é possível renomear uma tabela ou um banco de dados enquanto ele está em uso. A renomeação de uma tabela exige um bloqueio exclusivo na tabela. Se a tabela estiver em uso, você precisará encerrar as sessões que usam a tabela. Para terminar uma sessão, use o comando KILL. Use KILL com cuidado, pois quando uma sessão for terminada, qualquer trabalho não confirmado será revertido. As sessões no SQL Data Warehouse são prefixadas com 'SID'. Inclua o ‘SID’ e o número da sessão ao invocar o comando KILL. Este exemplo exibe uma lista de sessões ativas ou ociosas e, em seguida, termina a sessão 'SID1234'.  
  
### <a name="views-are-not-updated"></a>As exibições não são atualizadas  
 Ao renomear um banco de dados, todas as exibições que usam o nome antigo do banco de dados se tornarão inválidas. Esse comportamento se aplica às exibições dentro e fora do banco de dados. Por exemplo, se o banco de dados Sales for renomeado, uma exibição que contém `SELECT * FROM Sales.dbo.table1` se tornará inválida. Para resolver esse problema, evite usar nomes de três partes em exibições ou atualizar as exibições para elas referenciarem o novo nome de banco de dados.  
  
 Ao renomear uma tabela, as exibições não são atualizadas para referenciar o novo nome da tabela. Toda exibição, dentro ou fora do banco de dados, que referencia o nome da tabela antiga se tornará inválida. Para resolver esse problema, atualize cada exibição para ela referenciar o novo nome da tabela.  
  
## <a name="locking"></a>Bloqueio  
 A renomeação de uma tabela usa um bloqueio compartilhado no objeto DATABASE, um bloqueio compartilhado no objeto SCHEMA e um bloqueio exclusivo na tabela.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-rename-a-database"></a>A. Renomear um banco de dados  
 **APLICA-SE A:** somente ao [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Esse exemplo renomeia o banco de dados definido pelo usuário AdWorks como AdWorks2.  
  
```  
-- Rename the user defined database AdWorks  
RENAME DATABASE AdWorks to AdWorks2;  
  
```  
  
 Ao renomear uma tabela, todas as propriedades e todos os objetos associados à tabela são atualizados para referenciar o novo nome da tabela. Por exemplo, definições de tabela, índices, restrições e permissões são atualizados. Exibições não são atualizadas.  
  
### <a name="b-rename-a-table"></a>B. Renomear uma tabela  
 **APLICA-SE A:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Este exemplo renomeia a tabela Customer como Customer1.  
  
```  
-- Rename the customer table  
RENAME OBJECT Customer TO Customer1;  
  
RENAME OBJECT mydb.dbo.Customer TO Customer1;  
```  
  
 Ao renomear uma tabela, todas as propriedades e todos os objetos associados à tabela são atualizados para referenciar o novo nome da tabela. Por exemplo, definições de tabela, índices, restrições e permissões são atualizados. Exibições não são atualizadas.  
   
  
### <a name="c-move-a-table-to-a-different-schema"></a>C. Mover uma tabela para outro esquema  
 **APLICA-SE A:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Se sua intenção for mover o objeto para outro esquema, use [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md). Por exemplo, a instrução a seguir move o item de tabela do esquema de produto ao esquema de dbo.  
  
```  
ALTER SCHEMA dbo TRANSFER OBJECT::product.item;  
```  
  
### <a name="d-terminate-sessions-before-renaming-a-table"></a>D. Encerrar sessões antes de renomear uma tabela  
 **APLICA-SE A:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 É importante se lembrar de que não é possível renomear uma tabela enquanto ela está em uso. Uma renomeação de uma tabela exige um bloqueio exclusivo na tabela. Se a tabela estiver em uso, você precisará encerrar a sessão usando a tabela. Para terminar uma sessão, use o comando KILL. Use KILL com cuidado, pois quando uma sessão for terminada, qualquer trabalho não confirmado será revertido. As sessões no SQL Data Warehouse são prefixadas com 'SID'. Será necessário incluir o ‘SID’ e o número da sessão ao invocar o comando KILL. Este exemplo exibe uma lista de sessões ativas ou ociosas e, em seguida, termina a sessão 'SID1234'.  
  
```  
-- View a list of the current sessions  
SELECT session_id, login_name, status   
FROM sys.dm_pdw_exec_sessions   
WHERE status='Active' OR status='Idle';  
  
-- Terminate a session using the session_id.  
KILL 'SID1234';  
```  
  
  
