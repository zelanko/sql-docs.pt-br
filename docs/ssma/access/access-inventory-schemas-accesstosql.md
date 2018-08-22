---
title: Acessar os esquemas de estoque (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- columns table
- databases table
- exported metadata
- exporting, schemas of exported metadata
- foreign keys table
- forms table
- indexes, table
- inventory schemas
- macros table
- modules table
- queries table
- reference, inventory schemas
- reports table
- schemas of exported metadata
- schemas, exported metadata
- SSMA_Access_InventoryColumns
- SSMA_Access_InventoryDatabases
- SSMA_Access_InventoryForeignKeys
- SSMA_Access_InventoryForms
- SSMA_Access_InventoryIndexes
- SSMA_Access_InventoryMacros
- SSMA_Access_InventoryModules
- SSMA_Access_InventoryQueries
- SSMA_Access_InventoryReports
- SSMA_Access_InventoryTables
- tables, inventory
ms.assetid: fdd3cff2-4d62-4395-8acf-71ea8f17f524
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b0344fcfa5a5b174ef080a5eac431cebf6372842
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392455"
---
# <a name="access-inventory-schemas-accesstosql"></a>Esquemas de inventário do Access (AccessToSQL)
As seções a seguir descrevem as tabelas que são criadas por SSMA quando você exporta os esquemas de acesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="databases"></a>Bancos de dados  
Metadados de banco de dados são exportados para o **SSMA_Access_InventoryDatabases** tabela. Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Um GUID que identifica exclusivamente cada banco de dados. Essa coluna também é a chave primária da tabela.|  
|**DatabaseName**|**nvarchar(4000)**|O nome do banco de dados do Access.|  
|**ExportTime**|**datetime**|A data e hora que esses metadados foi criado por SSMA.|  
|**FilePath**|**nvarchar(4000)**|O nome de arquivo e caminho completo do banco de dados do Access.|  
|**FileSize**|**bigint**|O tamanho do banco de dados de acesso em KB.|  
|**FileOwner**|**nvarchar(4000)**|A conta do Windows que é especificada como o proprietário do banco de dados do Access.|  
|**DateCreated**|**datetime**|A data e hora que o banco de dados foi criado.|  
|**DateModified**|**datetime**|A data e hora que o banco de dados foi modificado pela última vez.|  
|**TablesCount**|**int**|O número de tabelas no banco de dados do Access.|  
|**QueriesCount**|**int**|O número de consultas no banco de dados do Access.|  
|**FormsCount**|**int**|O número de formulários no banco de dados do Access.|  
|**ModulesCount**|**int**|O número de módulos no banco de dados do Access.|  
|**ReportsCount**|**int**|O número de relatórios no banco de dados do Access.|  
|**MacrosCount**|**int**|O número de macros no banco de dados do Access.|  
|**AccessVersion**|**nvarchar(4000)**|A versão do banco de dados do Access.|  
|**Agrupamento**|**nvarchar(4000)**|O agrupamento do banco de dados do Access. Agrupamentos determinam como um banco de dados classifica e compara cadeias de caracteres.|  
|**JetVersion**|**nvarchar(4000)**|A versão do mecanismo de banco de dados Jet. Acessar bancos de dados usam o mecanismo de banco de dados Jet subjacente.|  
|**IsUpdatable**|**bit**|Indica se o banco de dados pode ser atualizado. Se o valor for 1, o banco de dados é atualizável. Se o valor for 0, o banco de dados é somente leitura.|  
|**QueryTimeout**|**int**|O ODBC consulta tempo limite valor configurado para o banco de dados, em segundos. O padrão é 60 segundos.|  
  
## <a name="tables"></a>Tabelas  
Metadados de tabela é exportado para o **SSMA_Access_InventoryTables** tabela. Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém esta tabela.|  
|**TableId**|**uniqueidentifier**|Um GUID que identifica exclusivamente a tabela. Essa coluna também é a chave primária da tabela.|  
|**TableName**|**nvarchar(4000)**|O nome da tabela.|  
|**RowsCount**|**int**|O número de linhas da tabela.|  
|**ValidationRule**|**nvarchar(4000)**|A regra que define uma entrada válida para a tabela. Se não existir nenhuma regra de validação, o campo conterá uma cadeia de caracteres vazia.|  
|**LinkedTable**|**nvarchar(4000)**|Outra tabela, se houver, que é vinculada com a tabela. Vinculando tabelas permite adições, exclusões e atualizações para a outra tabela usando essa tabela.|  
|**ExternalSource**|**nvarchar(4000)**|A fonte de dados, se houver, que está associado com a tabela. Se uma tabela estiver vinculada, ele tem uma fonte de dados externa especificada nesse campo.|  
  
## <a name="columns"></a>Colunas  
Metadados da coluna é exportado para o **SSMA_Access_InventoryColumns** tabela. Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém esta coluna.|  
|**TableId**|**uniqueidentifier**|Identifica a tabela que contém esta coluna.|  
|**ColumnId**|**int**|Um inteiro incrementado que identifica a coluna. **ColumnId** é a chave primária da tabela.|  
|**ColumnName**|**nvarchar(4000)**|O nome da coluna.|  
|**IsNullable**|**bit**|Especifica se a coluna pode conter valores nulos. Se o valor for 1, a coluna pode conter valores nulos. Se o valor for 0, a coluna não pode conter valores nulos. Observe que a regra de validação também pode ser usada para impedir que valores nulos.|  
|**DataType**|**nvarchar(4000)**|Digite os acessar os dados da coluna, como **texto** ou **longo**.|  
|**IsAutoIncrement**|**bit**|Especifica se a coluna incrementa automaticamente valores inteiros. Se o valor for 1, os inteiros são incremento automático.|  
|**Ordinal**|**smallint**|A ordem da coluna na tabela, começando em zero.|  
|**DefaultValue**|**nvarchar(4000)**|O valor padrão da coluna.|  
|**ValidationRule**|**nvarchar(4000)**|A regra que é usada para validar os dados adicionados ou atualizados na coluna.|  
  
## <a name="indexes"></a>Índices  
Os metadados do índice é exportado para o **SSMA_Access_InventoryIndexes** tabela. Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém esse índice.|  
|**TableId**|**uniqueidentifier**|Identifica a tabela que contém esse índice.|  
|**IndexId**|**int**|Um inteiro incrementado que identifica o índice. Esta coluna é a chave primária da tabela.|  
|**IndexName**|**nvarchar(4000)**|O nome do índice.|  
|**ColumnsIncluded**|**nvarchar(4000)**|Lista as colunas que estão incluídas no índice. Os nomes de coluna são separados por ponto e vírgula.|  
|**IsUnique**|**bit**|Especifica se cada item no índice deve ser exclusivo. Em um índice de várias colunas, a combinação de valores deve ser exclusiva. Se o valor for 1, o índice impõe valores exclusivos.|  
|**IsPK**|**bit**|Especifica se o índice foi criado automaticamente como parte da definição de chave primária.|  
|**IsClustered**|**bit**|Especifica se o índice é clusterizado. Um índice clusterizado reorganiza o armazenamento físico dos dados. Uma tabela pode ter apenas um índice clusterizado.|  
  
## <a name="foreign-keys"></a>Chaves estrangeiras  
Metadados de chave estrangeira é exportado para o **SSMA_Access_InventoryForeignKeys** tabela. Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém esse foreign key.|  
|**TableId**|**uniqueidentifier**|Identifica a tabela que contém esse foreign key.|  
|**ForeignKeyId**|**int**|Um inteiro incrementado que identifica a chave estrangeira. Esta coluna é a chave primária da tabela.|  
|**ForeignKeyName**|**nvarchar(4000)**|O nome do índice.|  
|**ReferencedTableId**|**uniqueidentifier**|Identifica a tabela que contém as colunas de origem.|  
|**SourceColumns**|**nvarchar(4000)**|Lista as colunas de chave estrangeira ou colunas.|  
|**ReferencedColumns**|**nvarchar(4000)**|Lista a coluna de chave primária ou colunas que são referenciadas pela chave estrangeira.|  
|**IsCascadeForUpdate**|**bit**|Especifica que, se o valor de chave primária for atualizado, todas as linhas que fazem referência a esse valor de chave também são atualizadas.|  
|**IsCascadeForDelete**|**bit**|Especifica que, se o valor de chave primária é excluído, todas as linhas que fazem referência a esse valor de chave também são excluídas.|  
|**IsEnforced**|**bit**|Especifica que a restrição de chave estrangeira é imposta.|  
  
## <a name="queries"></a>Consultas  
Metadados de consulta é exportado para o **SSMA_Access_InventoryQueries** tabela. Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém esta consulta.|  
|**QueryId**|**int**|Um inteiro incrementado que identifica a consulta. Esta coluna é a chave primária da tabela.|  
|**QueryName**|**nvarchar(4000)**|O nome da consulta.|  
|**QueryText**|**nvarchar(4000)**|O código de consulta SQL, como uma instrução SELECT.|  
|**IsUpdateable**|**bit**|Especifica se a consulta é atualizável ou somente leitura.|  
|**QueryType**|**nvarchar(4000)**|Especifica o tipo de consulta, tais como **selecionar** ou **SetOperation**.|  
|**ExternalSource**|**nvarchar(4000)**|Se a consulta faz referência a uma fonte de dados externa, essa é a cadeia de conexão usada pela consulta.|  
  
## <a name="forms"></a>Formulários  
Metadados do formulário é exportado para o **SSMA_Access_InventoryForms** tabela. Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém esse formulário.|  
|**FormId**|**int**|Um inteiro incrementado que identifica o formulário. Esta coluna é a chave primária da tabela.|  
|**Nome do formulário**|**nvarchar(4000)**|O nome do formulário.|  
  
## <a name="macros"></a>Macros  
Metadados de macro é exportado para o **SSMA_Access_InventoryMacros** tabela. Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém a macro.|  
|**MacroId**|**int**|Um inteiro incrementado que identifica a macro. Esta coluna é a chave primária da tabela.|  
|**MacroName**|**nvarchar(4000)**|O nome da macro.|  
  
## <a name="reports"></a>Relatórios  
Os metadados do relatório é exportado para o **SSMA_Access_InventoryReports** tabela. Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém o relatório.|  
|**ReportId**|**int**|Um inteiro incrementado que identifica o relatório. Esta coluna é a chave primária da tabela.|  
|**ReportName**|**nvarchar(4000)**|O nome do relatório.|  
  
## <a name="modules"></a>Módulos  
Metadados do módulo são exportados para o **SSMA_Access_InventoryModules** tabela. Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém o módulo.|  
|**ModuleId**|**int**|Um inteiro incrementado que identifica o módulo. Esta coluna é a chave primária da tabela.|  
|**ModuleName**|**nvarchar(4000)**|O nome do módulo.|  
  
## <a name="see-also"></a>Consulte também  
[Exportar um inventário do Access](exporting-an-access-inventory-accesstosql.md)  
  
