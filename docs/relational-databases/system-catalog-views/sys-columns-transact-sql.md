---
title: sys. Columns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.columns_TSQL
- sys.columns
- columns_TSQL
- columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.columns catalog view
ms.assetid: 323ac9ea-fc52-4b8c-8a7e-e0e44f8ed86c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: baf6cff936e446dce22a3d6c7fe7431f09272d58
ms.sourcegitcommit: 19e1c4067142d33e8485cb903a7a9beb7d894015
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2017
---
# <a name="syscolumns-transact-sql"></a>sys.columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada coluna de um objeto que tem colunas, como exibições ou tabelas. A seguir, uma lista de tipos de objeto que têm colunas.  
  
-   Funções de assembly com valor de tabela (FT)  
  
-   Funções SQL embutidas com valor de tabela (IF)  
  
-   Tabelas internas (IT)  
  
-   Tabelas do sistema (S)  
  
-   Funções SQL com valor de tabela (TF)  
  
-   Tabelas de usuário (U)  
  
-   Exibições (V)  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID do objeto ao qual esta coluna pertence.|  
|name|**sysname**|Nome da coluna. É exclusiva no objeto.|  
|column_id|**int**|ID da coluna. É exclusiva no objeto.<br /><br /> Os IDs de coluna podem não ser sequenciais.|  
|system_type_id|**tinyint**|ID de coluna do tipo de sistema.|  
|user_type_id|**int**|ID do tipo da coluna, como definido pelo usuário.<br /><br /> Para retornar o nome do tipo, unir o [Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) essa coluna de exibição do catálogo.|  
|max_length|**smallint**|Comprimento máximo (em bytes) da coluna.<br /><br /> -1 = a coluna de tipo de dados é **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, ou **xml**.<br /><br /> Para **texto** colunas, o valor de max_length será 16 ou o valor definido por sp_tableoption 'text in row'.|  
|precisão|**tinyint**|Precisão da coluna se tiver base numérica; Caso contrário, 0.|  
|scale|**tinyint**|Escala da coluna se numérica; caso contrário é 0.|  
|collation_name|**sysname**|Nome do agrupamento da coluna com base em caractere; Caso contrário, nulo.|  
|is_nullable|**bit**|1 = A coluna permite valor nulo.|  
|is_ansi_padded|**bit**|1 = A coluna usa o comportamento ANSI_PADDING ON se for de caractere, binária, ou variante.<br /><br /> 0 = A coluna não é de caractere, binária nem variante.|  
|is_rowguidcol|**bit**|1 = A coluna é uma ROWGUIDCOL declarada.|  
|is_identity|**bit**|1 = A coluna tem valores de identidade|  
|is_computed|**bit**|1 = A coluna é computada.|  
|is_filestream|**bit**|1 = A coluna é uma coluna de FILESTREAM.|  
|is_replicated|**bit**|1 = A coluna é replicada.|  
|is_non_sql_subscribed|**bit**|1 = A coluna tem um assinante não SQL Server.|  
|is_merge_published|**bit**|1 = A coluna é publicada por mesclagem.|  
|is_dts_replicated|**bit**|1 = A coluna é replicada usando o [!INCLUDE[ssIS](../../includes/ssis-md.md)].|  
|is_xml_document|**bit**|1 = O conteúdo é um documento XML completo.<br /><br /> 0 = o conteúdo é um fragmento de documento ou o tipo de dados de coluna não é **xml**.|  
|xml_collection_id|**int**|Diferente de zero se o tipo de dados da coluna for **xml** e o XML for digitado. O valor será a ID da coleção que contém o namespace do esquema XML validação da coluna.<br /><br /> 0 = Nenhuma coleção de esquemas XML.|  
|default_object_id|**int**|ID do objeto padrão, independentemente de ser um objeto autônomo [sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md), ou em uma linha, restrição de padrão de nível de coluna. A coluna parent_object_id de um objeto embutido padrão no nível da coluna é uma referência à própria tabela.<br /><br /> 0 = Sem padrão.|  
|rule_object_id|**int**|ID da regra autônoma associada à coluna usando sys.sp_bindrule.<br /><br /> 0 = Nenhuma regra autônoma. Para restrições de verificação de nível de coluna, consulte [sys. CHECK_CONSTRAINTS &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md).|  
|is_sparse|**bit**|1 = A coluna é esparsa. Para obter mais informações, veja [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).|  
|is_column_set|**bit**|1 = A coluna é um conjunto de colunas. Para obter mais informações, veja [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).|  
|generated_always_type|**tinyint**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Identifica quando o valor da coluna é gerado (sempre será 0 para colunas em tabelas do sistema):<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END<br /><br /> Para obter mais informações, consulte [tabelas temporais &#40; Bancos de dados relacionais &#41; ](../../relational-databases/tables/temporal-tables.md).|  
|generated_always_type_desc|**nvarchar (60)**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Descrição textual do `generated_always_type`do valor (sempre NOT_APPLICABLE para colunas em tabelas do sistema) <br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END|  
|encryption_type|**int**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Tipo de criptografia:<br /><br /> 1 = a criptografia determinística<br /><br /> 2 = criptografia aleatória|  
|encryption_type_desc|**nvarchar (64)**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Descrição do tipo de criptografia:<br /><br /> ALEATÓRIA<br /><br /> DETERMINISTIC|  
|encryption_algorithm_name|**sysname**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Nome do algoritmo de criptografia.<br /><br /> AEAD_AES_256_CBC_HMAC_SHA_512 só tem suporte.|  
|column_encryption_key_id|**int**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> ID da CEK.|  
|column_encryption_key_database_name|**sysname**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDW_md](../../includes/sssds-md.md)].<br /><br /> O nome do banco de dados onde a chave de criptografia de coluna se for diferente do banco de dados da coluna. NULL se a chave existir no mesmo banco de dados da coluna.|  
|is_hidden|**bit**|**Aplica-se a**: [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Indica se a coluna está oculta:<br /><br /> 0 = a coluna regular, visível não-oculto<br /><br /> 1 = a coluna oculta|  
|is_masked|**bit**|**Aplica-se a**: [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Indica se a coluna é mascarada por uma máscara de dados dinâmico:<br /><br /> 0 = a coluna regular, mascarado não<br /><br /> 1 = coluna é mascarada|  


 
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições de catálogo de objeto &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [all_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.system_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)  
  
  
