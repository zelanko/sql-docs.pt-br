---
title: DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DB_NAME
- DB_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database names [SQL Server], DB_NAME
- names [SQL Server], databases
- viewing database names
- displaying database names
- DB_NAME function
ms.assetid: e21fb33a-a3ea-49b0-bb6b-8f789a675a0e
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3f16a13c9fb93d17ecb4efaa62b6ba0eb6cd879d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65945633"
---
# <a name="dbname-transact-sql"></a>DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Essa função retorna o nome de um banco de dados especificado.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*database_id*  

O número de identificação (ID) do banco de dados cujo nome `DB_NAME` será retornado. Se a chamada para `DB_NAME` omite *database_id*, `DB_NAME` retorna o nome do banco de dados atual.
  
## <a name="return-types"></a>Tipos de retorno
**nvarchar(128)**
  
## <a name="permissions"></a>Permissões  

Se o chamador de `DB_NAME` não é proprietário de um banco de dados específico não **mestre** ou não **tempdb**, são necessárias no mínimo as permissões de nível de servidor `ALTER ANY DATABASE` ou `VIEW ANY DATABASE` para ver a linha `DB_ID` correspondente. Para o banco de dados **mestre**, `DB_ID` precisa, no mínimo, da permissão `CREATE DATABASE`. O banco de dados ao qual o chamador se conecta será sempre exibido em **sys.databases**.
  
> [!IMPORTANT]  
>  Por padrão, a função pública tem a permissão `VIEW ANY DATABASE`, que permite que todos os logons vejam informações do banco de dados. Para impedir a detecção de um banco de dados por um logon, aplique `REVOKE` na permissão `VIEW ANY DATABASE` da função pública, ou aplique `DENY` na permissão `VIEW ANY DATABASE` para logons individuais.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-current-database-name"></a>A. Retornando o nome do banco de dados atual  
Este exemplo retorna o nome do banco de dados atual.
  
```sql
SELECT DB_NAME() AS [Current Database];  
GO  
```  
  
### <a name="b-returning-the-database-name-of-a-specified-database-id"></a>B. Retornando o nome do banco de dados de uma ID de banco de dados especificada  
Este exemplo retorna o nome do banco de dados para a ID de banco de dados `3`.
  
```sql
USE master;  
GO  
SELECT DB_NAME(3)AS [Database Name];  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>C. Retornar o nome do banco de dados atual  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. Retornar o nome de um banco de dados usando a ID de banco de dados  
Este exemplo retorna o nome do banco de dados e a database_id de cada banco de dados.
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>Confira também
[DB_ID &#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)  
[Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

