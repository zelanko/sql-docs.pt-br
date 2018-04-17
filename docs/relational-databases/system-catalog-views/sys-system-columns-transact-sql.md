---
title: sys.system_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- system_columns_TSQL
- system_columns
- sys.system_columns
- sys.system_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_columns catalog view
ms.assetid: 4ab1d48a-d57a-4e76-a08c-9627eeaf4588
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 26caf28ed53d6c2dce5baf3f2c7f290d80afaa16
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="syssystemcolumns-transact-sql"></a>sys.system_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada coluna de objetos do sistema que têm colunas.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**Int**|ID do objeto ao qual esta coluna pertence.|  
|**name**|**sysname**|Nome da coluna. É exclusiva no objeto.|  
|**column_id**|**Int**|ID da coluna. É exclusiva no objeto.<br /><br /> Os IDs de coluna podem não ser sequenciais.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema da coluna|  
|**user_type_id**|**Int**|ID do tipo da coluna, como definido pelo usuário.<br /><br /> Para retornar o nome do tipo, unir o [Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) essa coluna de exibição do catálogo.|  
|**max_length**|**smallint**|Comprimento máximo (em bytes) da coluna.<br /><br /> -1 = a coluna de tipo de dados é **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, ou **xml**.<br /><br /> Para **texto** colunas, o **max_length** valor será 16 ou o valor definido por **sp_tableoption** 'text in row'.|  
|**precisão**|**tinyint**|Precisão da coluna se tiver base numérica; Caso contrário, 0.|  
|**scale**|**tinyint**|Escala da coluna com base numérica, caso contrário é 0.|  
|**collation_name**|**sysname**|Nome do agrupamento da coluna com base em caractere; Caso contrário, nulo.|  
|**is_nullable**|**bit**|1 = A coluna permite valor nulo.|  
|**is_ansi_padded**|**bit**|1 = A coluna usa o comportamento ANSI_PADDING ON se for de caractere, binária, ou variante.<br /><br /> 0 = A coluna não é de caractere, binária nem variante.|  
|**is_rowguidcol**|**bit**|1 = A coluna é uma ROWGUIDCOL declarada.|  
|**is_identity**|**bit**|1 = A coluna tem valores de identidade.|  
|**is_computed**|**bit**|1 = A coluna é computada.|  
|**is_filestream**|**bit**|1 = A coluna está declarada para usar armazenamento de fluxo de arquivos.|  
|**is_replicated**|**bit**|1 = A coluna é replicada.|  
|**is_non_sql_subscribed**|**bit**|1 = A coluna tem um assinante não pertencente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**is_merge_published**|**bit**|1 = A coluna é publicada por mesclagem.|  
|**is_dts_replicated**|**bit**|1 = A coluna é replicada usando o [!INCLUDE[ssIS](../../includes/ssis-md.md)].|  
|**is_xml_document**|**bit**|1 = O conteúdo é um documento XML completo.<br /><br /> 0 = o conteúdo é um fragmento de documento, ou o tipo de dados de coluna não é **xml**.|  
|**xml_collection_id**|**Int**|Diferente de zero se o tipo de dados de coluna for **xml** e o XML for digitado. O valor será a ID da coleção que contém o namespace do esquema XML validação da coluna.<br /><br /> 0 = Nenhuma coleção de esquemas XML.|  
|**default_object_id**|**Int**|ID do objeto padrão, independentemente de ser autônoma [sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md), ou em uma linha, restrição de padrão de nível de coluna. O **parent_object_id** coluna de um objeto embutido padrão no nível de coluna é uma referência à própria tabela. Ou 0, se não houver padrão.|  
|**rule_object_id**|**Int**|ID da regra autônoma associada à coluna usando **sp_bindrule**.<br /><br /> 0 = Nenhuma regra autônoma.<br /><br /> Para restrições de verificação de nível de coluna, consulte [sys. CHECK_CONSTRAINTS &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md).|  
|is_sparse|**bit**|1 = A coluna é esparsa. Para obter mais informações, veja [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).|  
|is_column_set|**bit**|1 = A coluna é um conjunto de colunas. Para obter mais informações, veja [Usar conjuntos de colunas](../../relational-databases/tables/use-column-sets.md).|  
|generated_always_type|**tinyint**|O valor numérico que representa o tipo de coluna:<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END|  
|generated_always_type_desc|**nvarchar(60)**|A descrição de texto do tipo de coluna:<br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [. computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)  
  
  
