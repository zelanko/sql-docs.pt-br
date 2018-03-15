---
title: SCHEMA_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8ff63abb8b74497b05045a2892067d7b4e49140a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="schemaid-transact-sql"></a>SCHEMA_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a ID de esquema associada a um nome de esquema.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SCHEMA_ID ( [ schema_name ] )   
```  
  
## <a name="arguments"></a>Argumentos  
  
|Termo|Definição|  
|----------|----------------|  
|*schema_name*|É o nome do esquema. *schema_name* é **sysname**. Se *schema_name* não for especificado, SCHEMA_ID retornará a ID do esquema padrão do chamador.|  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
 NULL será retornado se *schema_name* não for um esquema válido.  
  
## <a name="remarks"></a>Remarks  
 SCHEMA_ID retornará IDs de esquemas de sistema e de esquemas definidos pelo usuário. SCHEMA_ID pode ser chamado em uma lista de seleção, em uma cláusula WHERE e em qualquer lugar em que uma expressão seja permitida.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>A. Retornando a ID do esquema padrão de um chamador  
  
```  
SELECT SCHEMA_ID();  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>B. Retornando a ID de um esquema nomeado  
  
```  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/schema-name-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  

