---
title: DB_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DB_ID_TSQL
- DB_ID
dev_langs:
- TSQL
helpviewer_keywords:
- viewing database ID numbers
- IDs [SQL Server], databases
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
- displaying database ID numbers
- DB_ID function
ms.assetid: 7b3aef89-a6fd-4144-b468-bf87ebf381b8
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d9908d99f81094b8b8d3c2afd5c82ad870c2de22
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68995746"
---
# <a name="db_id-transact-sql"></a>DB_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esta função retorna o número da ID (identificação) de um banco de dados especificado.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DB_ID ( [ 'database_name' ] )   
```  
  
## <a name="arguments"></a>Argumentos  
'*database_name*'  
O nome do banco de dados cujo número de identificação retornará `DB_ID`. Se a chamada para `DB_ID` omite *database_name*, `DB_ID` retorna a ID do banco de dados atual.
  
## <a name="return-types"></a>Tipos de retorno
**int**

## <a name="remarks"></a>Comentários
O `DB_ID` só pode ser usado para retornar o identificador do banco de dados atual no Banco de Dados SQL. NULL será retornado se o nome do banco de dados especificado for diferente do atual.

> [!NOTE]
> Quando usado com o Banco de Dados SQL do Azure, `DB_ID` pode não retornar o mesmo resultado de uma consulta por `database_id` do **sys.databases**. Se o chamador de `DB_ID` estiver comparando o resultado a outras exibições **sys**, deve-se consultar **sys.databases**.
  
## <a name="permissions"></a>Permissões  
Se o chamador de `DB_ID` não é proprietário de um banco de dados específico não **mestre** ou não **tempdb**, são necessárias no mínimo as permissões de nível de servidor `ALTER ANY DATABASE` ou `VIEW ANY DATABASE` para ver a linha `DB_ID` correspondente. Para o banco de dados **mestre**, `DB_ID` precisa, no mínimo, da permissão `CREATE DATABASE`. O banco de dados ao qual o chamador se conecta será sempre exibido em **sys.databases**.
  
> [!IMPORTANT]  
>  Por padrão, a função pública tem a permissão `VIEW ANY DATABASE`, que permite que todos os logons vejam informações do banco de dados. Para impedir a detecção de um banco de dados por um logon, aplique `REVOKE` na permissão `VIEW ANY DATABASE` da função pública, ou aplique `DENY` na permissão `VIEW ANY DATABASE` para logons individuais.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-database-id-of-the-current-database"></a>a. Retornando a ID do banco de dados atual  
Este exemplo retorna a ID do banco de dados atual.
  
```sql
SELECT DB_ID() AS [Database ID];  
GO  
```  
  
### <a name="b-returning-the-database-id-of-a-specified-database"></a>B. Retornando a ID de um banco de dados especificado  
Este exemplo retorna a ID do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql
SELECT DB_ID(N'AdventureWorks2008R2') AS [Database ID];  
GO  
```  
  
### <a name="c-using-db_id-to-specify-the-value-of-a-system-function-parameter"></a>C. Usando DB_ID para especificar o valor de um parâmetro de função do sistema  
Este exemplo usa `DB_ID` para retornar a ID do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] na função do sistema `sys.dm_db_index_operational_stats`. A função aceita um ID de banco de dados como o primeiro parâmetro.
  
```sql
DECLARE @db_id int;  
DECLARE @object_id int;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
IF @db_id IS NULL   
  BEGIN;  
    PRINT N'Invalid database';  
  END;  
ELSE IF @object_id IS NULL  
  BEGIN;  
    PRINT N'Invalid object';  
  END;  
ELSE  
  BEGIN;  
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);  
  END;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-return-the-id-of-the-current-database"></a>D. Retornar a ID do banco de dados atual  
Este exemplo retorna a ID do banco de dados atual.
  
```sql
SELECT DB_ID();  
```  
  
### <a name="e-return-the-id-of-a-named-database"></a>E. Retornar a ID de um banco de dados nomeado.  
Este exemplo retorna a ID do banco de dados AdventureWorksDW2012.
  
```sql
SELECT DB_ID('AdventureWorksPDW2012');  
```  
  
## <a name="see-also"></a>Confira também
[DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
[Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)
  
  

