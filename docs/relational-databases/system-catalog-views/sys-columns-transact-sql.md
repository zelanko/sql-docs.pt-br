---
description: sys.columns (Transact-SQL)
title: sys. Columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f87df71c8159eb1da023f5d7d4800f15a72ebc4e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486471"
---
# <a name="syscolumns-transact-sql"></a>sys.columns (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha para cada coluna de um objeto que tem colunas, como exibições ou tabelas. A seguir, uma lista de tipos de objeto que têm colunas.  
  
-   Funções de assembly com valor de tabela (FT)  
  
-   Funções SQL embutidas com valor de tabela (IF)  
  
-   Tabelas internas (IT)  
  
-   Tabelas do sistema (S)  
  
-   Funções SQL com valor de tabela (TF)  
  
-   Tabelas de usuário (U)  
  
-   Exibições (V)  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID do objeto ao qual esta coluna pertence.|  
|name|**sysname**|Nome da coluna. É exclusiva no objeto.|  
|column_id|**int**|ID da coluna. É exclusiva no objeto.<br /><br /> Os IDs de coluna podem não ser sequenciais.|  
|system_type_id|**tinyint**|ID do tipo de sistema da coluna.|  
|user_type_id|**int**|ID do tipo da coluna, como definido pelo usuário.<br /><br /> Para retornar o nome do tipo, ingresse na exibição do catálogo [Sys. Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) nesta coluna.|  
|max_length|**smallint**|Comprimento máximo (em bytes) da coluna.<br /><br /> -1 = o tipo de dados da coluna é **varchar (max)**, **nvarchar (max)**, **varbinary (max)** ou **XML**.<br /><br /> Para colunas de **texto** , o valor de max_length será 16 ou o valor definido por sp_tableoption ' texto na linha '.|  
|precisão|**tinyint**|Precisão da coluna com base numérica, caso contrário é 0.|  
|scale|**tinyint**|Escala da coluna se numérica; caso contrário é 0.|  
|collation_name|**sysname**|Nome da ordenação da coluna, se for baseado em caracteres; caso contrário, será NULL.|  
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
|is_xml_document|**bit**|1 = O conteúdo é um documento XML completo.<br /><br /> 0 = o conteúdo é um fragmento de documento ou o tipo de dados da coluna não é **XML**.|  
|xml_collection_id|**int**|Diferente de zero se o tipo de dados da coluna for **XML** e o XML for digitado. O valor será a ID da coleção que contém o namespace do esquema XML de validação da coluna.<br /><br /> 0 = Nenhuma coleção de esquemas XML.|  
|default_object_id|**int**|ID do objeto padrão, independentemente de ser um objeto autônomo [Sys. sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)ou uma restrição padrão em nível de coluna em linha. A coluna parent_object_id de um objeto embutido padrão no nível da coluna é uma referência à própria tabela.<br /><br /> 0 = Sem padrão.|  
|rule_object_id|**int**|ID da regra autônoma associada à coluna usando sys.sp_bindrule.<br /><br /> 0 = Nenhuma regra autônoma. Para restrições de verificação em nível de coluna, consulte [Sys. check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md).|  
|is_sparse|**bit**|1 = A coluna é esparsa. Para obter mais informações, veja [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).|  
|is_column_set|**bit**|1 = A coluna é um conjunto de colunas. Para obter mais informações, veja [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).|  
|generated_always_type|**tinyint**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Identifica quando o valor da coluna é gerado (sempre será 0 para colunas em tabelas do sistema):<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END<br /><br /> Para obter mais informações, consulte [tabelas temporais &#40;bancos de dados relacionais&#41;](../../relational-databases/tables/temporal-tables.md).|  
|generated_always_type_desc|**nvarchar(60)**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Descrição textual do `generated_always_type` valor (sempre NOT_APPLICABLE para colunas em tabelas do sistema) <br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END|  
|encryption_type|**int**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Tipo de criptografia:<br /><br /> 1 = criptografia determinística<br /><br /> 2 = criptografia aleatória|  
|encryption_type_desc|**nvarchar (64)**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Descrição do tipo de criptografia:<br /><br /> ALEATÓRIA<br /><br /> DETERMINISTIC|  
|encryption_algorithm_name|**sysname**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Nome do algoritmo de criptografia.<br /><br /> Há suporte apenas para AEAD_AES_256_CBC_HMAC_SHA_512.|  
|column_encryption_key_id|**int**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> ID do CEK.|  
|column_encryption_key_database_name|**sysname**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior, [!INCLUDE[ssSDW_md](../../includes/sssds-md.md)].<br /><br /> O nome do banco de dados em que a chave de criptografia de coluna existe se for diferente do banco de dados da coluna. NULL se a chave existir no mesmo banco de dados que a coluna.|  
|is_hidden|**bit**|**Aplica-se a**: [!INCLUDE[ssCurrentLong](../../includes/sscurrent-md.md)] e posterior, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Indica se a coluna está oculta:<br /><br /> 0 = regular, não-oculta, coluna visível<br /><br /> 1 = coluna oculta|  
|is_masked|**bit**|**Aplica-se a**: [!INCLUDE[ssCurrentLong](../../includes/sscurrent-md.md)] e posterior, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Indica se a coluna é mascarada por uma máscara de dados dinâmicos:<br /><br /> 0 = coluna regular, não mascarada<br /><br /> 1 = a coluna está mascarada|  


 
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL ](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys. all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.system_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)  
  
  
