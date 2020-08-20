---
description: sys.index_columns (Transact-SQL)
title: sys. index_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.index_columns
- sys.index_columns_TSQL
- index_columns
- index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.index_columns catalog view
ms.assetid: 211471aa-558a-475c-9b94-5913c143ed12
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a7ab62980770499214f05fce8cfc1096aa7d088f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469935"
---
# <a name="sysindex_columns-transact-sql"></a>sys.index_columns (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Contém uma linha por coluna que faz parte de um índice **Sys.** Indexes ou de uma tabela não ordenada (heap).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto em que o índice está definido.|  
|**index_id**|**int**|ID do índice no qual a coluna está definida.|  
|**index_column_id**|**int**|ID da coluna de índice. **index_column_id** só é exclusiva no **index_id**.|  
|**column_id**|**int**|ID da coluna em **object_id**.<br /><br /> 0 = RID (Identificador de linha) em um índice não clusterizado.<br /><br /> **column_id** só é exclusiva no **object_id**.|  
|**key_ordinal**|**tinyint**|Ordinal (com base em 1) dentro do conjunto de colunas chave.<br /><br /> 0 = Não é uma coluna de chave ou é um índice XML, índice columnstore ou índice espacial.<br /><br /> Observação: um índice XML ou espacial não pode ser uma chave porque as colunas subjacentes não são comparáveis, o que significa que seus valores não podem ser ordenados.|  
|**partition_ordinal**|**tinyint**|Ordinal (com base em 1) dentro do conjunto de colunas de particionamento. Um índice columnstore clusterizado pode ter, no máximo, uma coluna de particionamento.<br /><br /> 0 = Não é uma coluna de particionamento.|  
|**is_descending_key**|**bit**|1 = A coluna de chave do índice tem uma classificação decrescente.<br /><br /> 0 = A coluna de chave do índice tem uma classificação crescente, ou a coluna faz parte de um índice de hash.|  
|**is_included_column**|**bit**|1 = A coluna é uma coluna não chave adicionada ao índice através da cláusula CREATE INDEX INCLUDE, ou a coluna faz parte de um índice columnstore.<br /><br /> 0 = A coluna não é uma coluna incluída.<br /><br /> As colunas adicionadas implicitamente porque fazem parte da chave de clustering não estão listadas em **Sys. index_columns**.<br /><br /> Colunas adicionadas implicitamente porque são uma coluna de particionamento são retornadas como 0.| 
|**column_store_order_ordinal**</br> Aplica-se a: SQL Data Warehouse do Azure (versão prévia)|**tinyint**|Ordinal (baseado em 1) dentro do conjunto de colunas de ordem em um índice columnstore clusterizado ordenado.|
  
## <a name="permissions"></a>Permissões

 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos

 O exemplo a seguir retorna todos os índices e colunas de índice para a tabela `Production.BillOfMaterials`.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,ic.key_ordinal  
,ic.is_included_column  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
WHERE i.object_id = OBJECT_ID('Production.BillOfMaterials');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
  
index_name                                                 column_name        index_column_id key_ordinal is_included_column  
---------------------------------------------------------- -----------------  --------------- ----------- -------------  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate ProductAssemblyID  1               1           0  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate ComponentID        2               2           0  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate StartDate          3               3           0  
PK_BillOfMaterials_BillOfMaterialsID                       BillOfMaterialsID  1               1           0  
IX_BillOfMaterials_UnitMeasureCode                         UnitMeasureCode    1               1           0  
  
(5 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
