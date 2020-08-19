---
description: PARSENAME (Transact-SQL)
title: PARSENAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PARSENAME_TSQL
- PARSENAME
dev_langs:
- TSQL
helpviewer_keywords:
- PARSENAME function
- parsing [SQL Server], PARSENAME function
- names [SQL Server], objects
- objects [SQL Server], names
- part of object names [SQL Server]
ms.assetid: abf34f99-9ee9-460b-85b2-930ca5c4b5ae
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 047b760e2b3e7101cd471a4e1a8c65cbc970c023
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459636"
---
# <a name="parsename-transact-sql"></a>PARSENAME (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna a parte especificada de um nome de objeto. As partes de um objeto que podem ser recuperadas são o nome do objeto, o nome do esquema, o nome do banco de dados e o nome do servidor. 
  
> [!NOTE]  
>  A função PARSENAME não indica se existe um objeto pelo nome especificado. PARSENAME apenas retorna a parte especificada do nome de objeto especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql 
PARSENAME ('object_name' , object_piece )
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

*' object_name '* é o parâmetro que contém o nome do objeto para o qual a parte de objeto especificada deve ser recuperada. Este parâmetro é um nome de objeto opcionalmente qualificado. Se todas as partes do nome do objeto forem qualificadas, esse nome poderá ter quatro partes: o nome do servidor, o nome do banco de dados, o nome do esquema e o nome do objeto.  Cada parte da cadeia de caracteres "object_name" é do tipo *sysname* que é equivalente a nvarchar(128) ou 256 bytes. Se qualquer parte da cadeia de caracteres exceder 256 bytes, PARSENAME retornará NULL para essa parte, pois não é um sysname válido.
  
*object_piece*  
É a parte do objeto a ser retornada. *object_piece* é do tipo **int** e pode ter estes valores:  
    1 = Nome do objeto  
    2 = Nome do esquema  
    3 = Nome do banco de dados  
    4 = Nome do servidor  
  
## <a name="return-type"></a>Tipo de retorno

 **sysname**
  
## <a name="remarks"></a>Comentários

 PARSENAME retornará o NULL se uma das seguintes condições for verdadeira:  
  
-   *object_name* ou *object_piece* é NULL.  
  
-   Um erro de sintaxe ocorre.  
  
 A parte do objeto solicitada tem um tamanho igual a 0 e não é um identificador do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido. Um nome de objeto de comprimento zero processa o nome qualificado completo como não válido.  
  
## <a name="examples"></a>Exemplos

 O exemplo a seguir usa `PARSENAME` para retornar informações sobre a tabela `Person` no banco de dados `AdventureWorks2012`.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 1) AS 'Object Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 2) AS 'Schema Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 3) AS 'Database Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 4) AS 'Server Name';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
Object Name
------------------------------
DimCustomer

(1 row(s) affected)

Schema Name
------------------------------
dbo

(1 row(s) affected)

Database Name
------------------------------
AdventureWorksPDW2012

(1 row(s) affected)

Server Name
------------------------------
(null)

(1 row(s) affected)
```
  
## <a name="see-also"></a>Consulte Também

- [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
- [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
- [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
- [Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  

