---
title: DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DB_NAME
- DB_NAME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- database names [SQL Server], DB_NAME
- names [SQL Server], databases
- viewing database names
- displaying database names
- DB_NAME function
ms.assetid: e21fb33a-a3ea-49b0-bb6b-8f789a675a0e
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3ca4b497be936701205b2be245f76a52eb372c2a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="dbname-transact-sql"></a>DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna o nome do banco de dados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*database_id*  
É o número de identificação (ID) do banco de dados a ser retornado. *database_id* é **int**, sem padrão. Se  nenhuma ID for especificada, o nome do banco de dados atual será retornado.
  
## <a name="return-types"></a>Tipos de retorno
**nvarchar (128)**
  
## <a name="permissions"></a>Permissões  
Se o chamador de **DB_NAME** não é o proprietário do banco de dados e o banco de dados não **mestre** ou **tempdb**, são as permissões mínimas necessárias para ver a linha correspondente Permissão de nível de servidor ALTER ANY DATABASE ou VIEW ANY DATABASE ou permissão CREATE DATABASE no **mestre** banco de dados. O banco de dados ao qual o chamador está conectado sempre pode ser exibido em **sys.databases**.
  
> [!IMPORTANT]  
>  Por padrão, a função pública tem a permissão VIEW ANY DATABASE, permitindo que todos os logons ver informações de banco de dados. Para bloquear um logon da capacidade de detectar um banco de dados, REVOGAR a permissão VIEW ANY DATABASE de pública ou negar a permissão VIEW ANY DATABASE para logons individuais.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-current-database-name"></a>A. Retornando o nome do banco de dados atual  
O exemplo a seguir retorna o nome do banco de dados atual.
  
```sql
SELECT DB_NAME() AS [Current Database];  
GO  
```  
  
### <a name="b-returning-the-database-name-of-a-specified-database-id"></a>B. Retornando o nome do banco de dados de uma ID de banco de dados especificada  
O exemplo a seguir retorna o nome do banco de dados para a ID de banco de dados `3`.
  
```sql
USE master;  
GO  
SELECT DB_NAME(3)AS [Database Name];  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>C. Retornar o nome do banco de dados atual  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. Retornar o nome de um banco de dados usando a ID de banco de dados  
O exemplo a seguir retorna o nome do banco de dados e database_id para cada banco de dados.
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>Consulte também
[DB_ID &#40; Transact-SQL &#41;](../../t-sql/functions/db-id-transact-sql.md)  
[Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

