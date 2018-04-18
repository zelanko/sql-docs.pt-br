---
title: sys.fn_listextendedproperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_listextendedproperty
- fn_listextendedproperty_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_listextendedproperty function
- displaying extended properties
- database extended properties [SQL Server]
- viewing extended properties
- column extended properties [SQL Server]
- sys.fn_listextendedproperties function
- database objects [SQL Server], extended properties
- extended properties [SQL Server], columns
- table extended properties [SQL Server]
ms.assetid: 59bbb91f-a277-4a35-803e-dcb91e847a49
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cdd9b448d0d8e6a6c57a6bae2c9c52a94952f380
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysfnlistextendedproperty-transact-sql"></a>sys.fn_listextendedproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna valores de propriedade estendidos de objetos de banco de dados.  
 
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_listextendedproperty (   
    { default | 'property_name' | NULL }   
  , { default | 'level0_object_type' | NULL }   
  , { default | 'level0_object_name' | NULL }   
  , { default | 'level1_object_type' | NULL }   
  , { default | 'level1_object_name' | NULL }   
  , { default | 'level2_object_type' | NULL }   
  , { default | 'level2_object_name' | NULL }   
  )   
```  
  
## <a name="arguments"></a>Argumentos  
 {padrão | '*property_name*' | NULL}  
 É o nome da propriedade. *Property_Name* é **sysname**. As entradas válidas são default, NULL ou um nome de propriedade.  
  
 {padrão | '*level0_object_type*' | NULL}  
 É o usuário ou tipo definido pelo usuário. *level0_object_type* é **varchar (128)**, com um padrão NULL. As entradas válidas são ASSEMBLY, CONTRACT, EVENT NOTIFICATION, FILEGROUP, MESSAGE TYPE, PARTITION FUNCTION, PARTITION SCHEME, REMOTE SERVICE BINDING, ROUTE, SCHEMA, SERVICE, TRIGGER, TYPE, USER e NULL.  
  
> [!IMPORTANT]  
>  USER e TYPE como tipos de nível 0 serão removidos em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses recursos em novo trabalho de desenvolvimento e planeje modificar os aplicativos que os usam atualmente. Use SCHEMA como o tipo de nível 0 em vez de USER. Para TYPE, use SCHEMA como o tipo de nível 0 e TYPE como o tipo de nível 1.  
  
 {padrão | '*level0_object_name*' | NULL}  
 É o nome do tipo de objeto de nível 0 especificado. *level0_object_name* é **sysname** com um padrão NULL. As entradas válidas são default, NULL ou um nome de objeto.  
  
 {padrão | '*level1_object_type*' | NULL}  
 É o tipo de objeto de nível 1. *level1_object_type* é **varchar (128)** com um padrão NULL. As entradas válidas são AGGREGATE, DEFAULT, FUNCTION, LOGICAL FILE NAME, PROCEDURE, QUEUE, RULE, SYNONYM, TABLE, TYPE, VIEW, XML SCHEMA COLLECTION e NULL.  
  
> [!NOTE]  
>  O padrão é mapeado para NULL e 'default' é mapeado para o tipo de objeto DEFAULT.  
  
 {padrão | '*level1_object_name*' | NULL}  
 É o nome do tipo de objeto de nível 1 especificado. *level1_object_name* é **sysname** com um padrão NULL. As entradas válidas são default, NULL ou um nome de objeto.  
  
 {padrão | '*level2_object_type*' | NULL}  
 É o tipo de objeto de nível 2. *level2_object_type* é **varchar (128)** com um padrão NULL. As entradas válidas são DEFAULT, default (mapeado para NULL) e NULL. As entradas válidas para *level2_object_type* são coluna, restrição, notificação de eventos, índice, parâmetro, TRIGGER e NULL.  
  
 {padrão | '*level2_object_name*' | NULL}  
 É o nome do tipo de objeto de nível 2 especificado. *level2_object_name* é **sysname** com um padrão NULL. As entradas válidas são default, NULL ou um nome de objeto.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 Este é o formato das tabelas retornadas por fn_listextendedproperty.  
  
|Nome da coluna|Tipo de dados|  
|-----------------|---------------|  
|objtype|**sysname**|  
|objname|**sysname**|  
|nome|**sysname**|  
|value|**sql_variant**|  
  
 Se a tabela retornada estiver vazia, o objeto não terá propriedades estendidas ou o usuário não terá permissões para listar as propriedades estendidas do objeto. Ao retornar propriedades estendidas do próprio banco de dados, as colunas objtype e objname serão NULL.  
  
## <a name="remarks"></a>Remarks  
 Se o valor de *property_name* for NULL ou default, fn_listextendedproperty retornará todas as propriedades para o objeto especificado.  
  
 Quando o tipo do objeto for especificado e o valor do nome do objeto correspondente for NULL ou default, fn_listextendedproperty retornará todas as propriedades estendidas de todos os objetos do tipo especificado.  
  
 Os objetos são diferenciados de acordo com níveis, em que nível 0 é o mais alto e nível 2 é o mais baixo. Se um objeto de nível inferior, nível 1 ou 2, um tipo e um nome forem especificados, o tipo e o nome do objeto pai deverão receber valores que não sejam NULL ou default. Caso contrário, a função retornará um conjunto de resultados vazio.  
  
 **objname** é fixo como Latin1_General_CI_AI. No entanto, você pode solucionar esse problema isso substituindo o agrupamento em comparação.  
  
```  
SELECT o.[object_id] AS 'table_id', o.[name] 'table_name',  
0 AS 'column_order', NULL AS 'column_name', NULL AS 'column_datatype',  
NULL AS 'column_length', Cast(e.value AS varchar(500)) AS 'column_description'  
FROM AdventureWorks.sys.objects AS o  
LEFT JOIN sys.fn_listextendedproperty(N'MS_Description', N'user',N'HumanResources',N'table', N'Employee', null, default) AS e  
    ON o.name = e.objname COLLATE SQL_Latin1_General_CP1_CI_AS  
WHERE o.name = 'Employee';  
```  
  
## <a name="permissions"></a>Permissões  
 As permissões para listar propriedades estendidas de objetos variam por tipo de objeto.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-extended-properties-on-a-database"></a>A. Exibindo propriedades estendidas em um banco de dados  
 O exemplo a seguir exibe todas as propriedades estendidas definidas no próprio objeto do banco de dados.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT objtype, objname, name, value  
FROM fn_listextendedproperty(default, default, default, default, default, default, default);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `objtype    objname     name            value`  
  
 `---------  ---------   -----------     ----------------------------`  
  
 `NULL       NULL        MS_Description  AdventureWorks2008 Sample OLTP Database`  
  
 `(1 row(s) affected)`  
  
### <a name="b-displaying-extended-properties-on-all-columns-in-a-table"></a>B. Exibindo propriedades estendidas em todas as colunas de uma tabela  
 O exemplo a seguir lista as propriedades estendidas para colunas de `ScrapReason` tabela. Isto está contido no esquema `Production`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT objtype, objname, name, value  
FROM fn_listextendedproperty (NULL, 'schema', 'Production', 'table', 'ScrapReason', 'column', default);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `objtype objname      name            value`  
  
 `------- -----------  -------------   ------------------------`  
  
 `COLUMN ScrapReasonID MS_Description  Primary key for ScrapReason records.`  
  
 `COLUMN Name          MS_Description  Failure description.`  
  
 `COLUMN ModifiedDate  MS_Description  Date the record was last updated.`  
  
 `(3 row(s) affected)`  
  
### <a name="c-displaying-extended-properties-on-all-tables-in-a-schema"></a>C. Exibindo propriedades estendidas em todas as tabelas de um esquema  
 O exemplo a seguir lista as propriedades estendidas para todas as tabelas contidas no `Sales` esquema.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT objtype, objname, name, value  
FROM fn_listextendedproperty (NULL, 'schema', 'Sales', 'table', default, NULL, NULL);  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_addextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sp_updateextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)   
 [sys.extended_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
