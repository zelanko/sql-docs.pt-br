---
title: sys.system_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4e7f9cf8cb5b7dfc0aba7858e3a042d9793e26c6
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999140"
---
# <a name="syssystem_columns-transact-sql"></a>sys.system_columns (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Contém uma linha para cada coluna de objetos do sistema que têm colunas.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual esta coluna pertence.|  
|**name**|**sysname**|Nome da coluna. É exclusiva no objeto.|  
|**column_id**|**int**|ID da coluna. É exclusiva no objeto.<br /><br /> Os IDs de coluna podem não ser sequenciais.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema da coluna|  
|**user_type_id**|**int**|ID do tipo da coluna, como definido pelo usuário.<br /><br /> Para retornar o nome do tipo, ingresse na exibição do catálogo [Sys. Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) nesta coluna.|  
|**max_length**|**smallint**|Comprimento máximo (em bytes) da coluna.<br /><br /> -1 = o tipo de dados da coluna é **varchar (max)**, **nvarchar (max)**, **varbinary (max)** ou **XML**.<br /><br /> Para colunas de **texto** , o valor de **max_length** será 16 ou o valor definido por **sp_tableoption** ' texto na linha '.|  
|**precisão**|**tinyint**|Precisão da coluna com base numérica, caso contrário é 0.|  
|**scale**|**tinyint**|Escala da coluna com base numérica, caso contrário é 0.|  
|**collation_name**|**sysname**|Nome da ordenação da coluna, se for baseado em caracteres; caso contrário, será NULL.|  
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
|**is_xml_document**|**bit**|1 = O conteúdo é um documento XML completo.<br /><br /> 0 = o conteúdo é um fragmento de documento ou o tipo de dados da coluna não é **XML**.|  
|**xml_collection_id**|**int**|Diferente de zero se o tipo de dados da coluna for **XML** e o XML for digitado. O valor será a ID da coleção que contém o namespace do esquema XML de validação da coluna.<br /><br /> 0 = Nenhuma coleção de esquemas XML.|  
|**default_object_id**|**int**|ID do objeto padrão, independentemente de ser um [Sys autônomo. sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)ou uma restrição padrão em nível de coluna, ou embutida. A coluna **parent_object_id** de um objeto padrão em nível de coluna embutida é uma referência de volta para a tabela em si. Ou 0, se não houver padrão.|  
|**rule_object_id**|**int**|ID da regra autônoma associada à coluna usando **Sys. sp_bindrule**.<br /><br /> 0 = Nenhuma regra autônoma.<br /><br /> Para restrições de verificação em nível de coluna, consulte [Sys. check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md).|  
|is_sparse|**bit**|1 = A coluna é esparsa. Para obter mais informações, veja [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).|  
|is_column_set|**bit**|1 = A coluna é um conjunto de colunas. Para obter mais informações, veja [Usar conjuntos de colunas](../../relational-databases/tables/use-column-sets.md).|  
|generated_always_type|**tinyint**|O valor numérico que representa o tipo de coluna:<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END|  
|generated_always_type_desc|**nvarchar(60)**|A descrição de texto do tipo de coluna:<br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [&#41;sys. Columns &#40;Transact-SQL](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys. all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys. computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)  
  
  
