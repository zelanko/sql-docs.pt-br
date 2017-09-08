---
title: SCHEMA_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SCHEMA_ID
- SCHEMA_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], schemas
- schemas [SQL Server], IDs
- SCHEMA_ID function
- IDs [SQL Server], schemas
- default schema IDs
ms.assetid: c8e34df5-3eea-459f-ae40-050909ce9fda
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e364abf5b75159600715be0a4823ba8fce847e2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="schemaid-transact-sql"></a>SCHEMA_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a ID de esquema associada a um nome de esquema.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SCHEMA_ID ( [ schema_name ] )   
```  
  
## <a name="arguments"></a>Argumentos  
  
|Termo|Definição|  
|----------|----------------|  
|*schema_name*|É o nome do esquema. *schema_name* é um **sysname**. Se *schema_name* não for especificado, SCHEMA_ID retornará a ID do esquema padrão do chamador.|  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
 NULL será retornado se *schema_name* não é um esquema válido.  
  
## <a name="remarks"></a>Comentários  
 SCHEMA_ID retornará IDs de esquemas de sistema e de esquemas definidos pelo usuário. SCHEMA_ID pode ser chamado em uma lista de seleção, em uma cláusula WHERE e em qualquer lugar em que uma expressão seja permitida.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>A. Retornando a ID do esquema padrão de um chamador  
  
```  
SELECT SCHEMA_ID();  
GO  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>B. Retornando a ID de um esquema nomeado  
  
```  
USE AdventureWorks2012;  
GO  
SELECT SCHEMA_ID('HumanResources');  
GO   
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-the-default-schema-id-of-a-caller"></a>C. Retornando a ID do esquema padrão de um chamador  
  
```  
SELECT SCHEMA_ID();  
```  
  
### <a name="d-returning-the-schema-id-of-a-named-schema"></a>D. Retornando a ID de um esquema nomeado  
  
```  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME &#40; Transact-SQL &#41;](../../t-sql/functions/schema-name-transact-sql.md)   
 [schemas &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  


