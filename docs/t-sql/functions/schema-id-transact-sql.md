---
description: SCHEMA_ID (Transact-SQL)
title: SCHEMA_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2cd9fc9bc52a69fb5200abaf2bd5f678fe4a1f73
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91379945"
---
# <a name="schema_id-transact-sql"></a>SCHEMA_ID (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna a ID de esquema associada a um nome de esquema.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
SCHEMA_ID ( [ schema_name ] )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
  
|Termo|Definição|  
|----------|----------------|  
|*schema_name*|É o nome do esquema. *schema_name* é **sysname**. Se *schema_name* não for especificado, SCHEMA_ID retornará a ID do esquema padrão do chamador.|  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
 NULL será retornado se *schema_name* não for um esquema válido.  
  
## <a name="remarks"></a>Comentários  
 SCHEMA_ID retornará IDs de esquemas de sistema e de esquemas definidos pelo usuário. SCHEMA_ID pode ser chamado em uma lista de seleção, em uma cláusula WHERE e em qualquer lugar em que uma expressão seja permitida.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>a. Retornando a ID do esquema padrão de um chamador  
  
```sql  
SELECT SCHEMA_ID();  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>B. Retornando a ID de um esquema nomeado  
  
```sql  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/schema-name-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  

