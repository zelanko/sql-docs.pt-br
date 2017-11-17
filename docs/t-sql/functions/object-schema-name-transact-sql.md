---
title: OBJECT_SCHEMA_NAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECT_SCHEMA_NAME
- OBJECT_SCHEMA_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], names
- schemas [SQL Server], names
- displaying schema names
- database objects [SQL Server], names
- OBJECT_SCHEMA_NAME function
ms.assetid: 5ba90bb9-d045-4164-963e-e9e96c0b1e8b
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 621a58fcc00b95626f3e4eb7d34d79af608436fe
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="objectschemaname-transact-sql"></a>OBJECT_SCHEMA_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o nome de esquema de banco de dados para objetos no escopo do esquema. Para obter uma lista de objetos no escopo do esquema, consulte [sys. Objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
OBJECT_SCHEMA_NAME ( object_id [, database_id ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 É a ID do objeto a ser usado. *object_id* é **int** e é considerado como um objeto no escopo do esquema de banco de dados especificado ou no contexto do banco de dados atual.  
  
 *database_id*  
 É a ID do banco de dados onde o objeto deve ser pesquisado. *database_id* é **int**.  
  
## <a name="return-types"></a>Tipos de retorno  
 **sysname**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto. Se o banco de dados de destino tiver a opção AUTO_CLOSE definida como ON, a função abrirá o banco de dados.  
  
 Um usuário só pode exibir metadados de protegíveis de sua propriedade ou para os quais recebeu permissão. Isso significa que as funções internas emissoras de metadados, como OBJECT_DEFINITIONSCHEMA_NAME, podem retornar NULL se o usuário não tiver permissão no objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ANY para o objeto. Para especificar uma identificação de banco de dados, é exigida também a permissão CONNECT para o banco de dados ou a conta de convidado deve ser habilitada.  
  
## <a name="remarks"></a>Comentários  
 As funções de sistema podem ser usadas na lista de seleção, na cláusula WHERE e em qualquer local onde uma expressão for permitida. Para obter mais informações, consulte [expressões](../../t-sql/language-elements/expressions-transact-sql.md) e [onde](../../t-sql/queries/where-transact-sql.md).  
  
 O conjunto de resultados retornado por esta função de sistema usa o agrupamento do banco de dados atual.  
  
 Se *database_id* não for especificado, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] supõe que *object_id* está no contexto do banco de dados atual. Uma consulta que faz referência a um *object_id* em outro banco de dados retorna NULL ou resultados incorretos. Por exemplo, na consulta a seguir o contexto do banco de dados atual é [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] tenta retornar um nome de esquema de objeto para a identificação do objeto especificado naquele banco de dados, em lugar do banco de dados especificado na cláusula FROM da consulta. Portanto, informações incorretas são retornadas.  
  
```  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id)  
FROM master.sys.objects;  
  
```  
  
 O exemplo a seguir especifica a identificação de banco de dados para o banco de dados `master` na função `OBJECT_SCHEMA_NAME` e retorna os resultados corretos.  
  
```  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id, 1) AS schema_name  
FROM master.sys.objects;  
  
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-object-schema-name-and-object-name"></a>A. Retornando o nome do esquema do objeto e o nome do objeto  
 O exemplo a seguir retorna o nome de esquema do objeto, nome de objeto e texto de SQL para todos os planos de consulta em cache que não sejam instruções ad hoc ou preparadas.  
  
```  
SELECT DB_NAME(st.dbid) AS database_name,   
    OBJECT_SCHEMA_NAME(st.objectid, st.dbid) AS schema_name,  
    OBJECT_NAME(st.objectid, st.dbid) AS object_name,   
    st.text AS query_statement  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
WHERE st.objectid IS NOT NULL;  
GO  
```  
  
### <a name="b-returning-three-part-object-names"></a>B. Retornando nomes de objetos de três partes  
 O exemplo a seguir retorna o banco de dados, esquema e nome de objeto juntamente com todas as outras colunas na exibição de gerenciamento dinâmico `sys.dm_db_index_operational_stats` de todos os objetos em todos os bancos de dados.  
  
```  
SELECT QUOTENAME(DB_NAME(database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_SCHEMA_NAME(object_id, database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_NAME(object_id, database_id))  
    , *   
FROM sys.dm_db_index_operational_stats(null, null, null, null);  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_ID &#40; Transact-SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [Object_name &#40; Transact-SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [Protegíveis](../../relational-databases/security/securables.md)  
  
  

