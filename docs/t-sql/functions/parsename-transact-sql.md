---
title: PARSENAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 908eb510f3916717065ff7d61f8162b222c1552e
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="parsename-transact-sql"></a>PARSENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Retorna a parte especificada de um nome de objeto. As partes de um objeto que podem ser recuperadas são o nome do objeto, o nome do proprietário, o nome do banco de dados e o nome do servidor.  
  
> [!NOTE]  
>  A função PARSENAME não indica se existe um objeto pelo nome especificado. PARSENAME apenas retorna a parte especificada do nome de objeto especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
PARSENAME ( 'object_name' , object_piece )   
```  
  
## <a name="arguments"></a>Argumentos  
 '*object_name*'  
 É o nome do objeto para o qual a parte de objeto especificada deve ser recuperada. *object_name* é **sysname**. Este parâmetro é um nome de objeto opcionalmente qualificado. Se todas as partes do nome do objeto forem qualificadas, esse nome poderá ter quatro partes: o nome do servidor, o nome do banco de dados, o nome do proprietário e o nome do objeto.  
  
 *object_piece*  
 É a parte do objeto a ser retornada. *object_piece* é do tipo **int** e pode ter estes valores:  
  
 1 = Nome do objeto  
  
 2 = Nome do esquema  
  
 3 = Nome do banco de dados  
  
 4 = Nome do servidor  
  
## <a name="return-types"></a>Tipos de retorno  
 **nchar**  
  
## <a name="remarks"></a>Remarks  
 PARSENAME retornará o NULL se uma das seguintes condições for verdadeira:  
  
-   *object_name* ou *object_piece* é NULL.  
  
-   Um erro de sintaxe ocorre.  
  
 A parte do objeto solicitada tem um tamanho igual a 0 e não é um identificador do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido. Um nome de objeto de comprimento zero processa o nome qualificado completo como não válido.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `PARSENAME` para retornar informações sobre a tabela `Person` no banco de dados `AdventureWorks2012`.  
  
```  
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
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

