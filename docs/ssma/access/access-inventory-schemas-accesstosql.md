---
description: Esquemas de inventário de acesso (AccessToSQL)
title: Esquemas de inventário de acesso (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 593c36c193b95d1484f3d478018992ea130d5417
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418632"
---
# <a name="access-inventory-schemas-accesstosql"></a>Esquemas de inventário de acesso (AccessToSQL)
As seções a seguir descrevem as tabelas criadas pelo SSMA quando você exporta esquemas de acesso para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="databases"></a>Bancos de dados  
Os metadados do banco de dados são exportados para a tabela de **SSMA_Access_InventoryDatabases** . Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Um GUID que identifica exclusivamente cada banco de dados. Essa coluna também é a chave primária para a tabela.|  
|**DatabaseName**|**nvarchar(4000)**|O nome do banco de dados do Access.|  
|**Exporttime**|**datetime**|A data e a hora em que esses metadados foram criados pelo SSMA.|  
|**FilePath**|**nvarchar(4000)**|O caminho completo e o nome do arquivo do banco de dados do Access.|  
|**Tamanho**|**bigint**|O tamanho do banco de dados do Access em KB.|  
|**Fileproprietário**|**nvarchar(4000)**|A conta do Windows que é especificada como o proprietário do banco de dados do Access.|  
|**DateCreated**|**datetime**|A data e a hora em que o banco de dados do Access foi criado.|  
|**DateModified**|**datetime**|A data e a hora da última modificação do banco de dados do Access.|  
|**TablesCount**|**int**|O número de tabelas no banco de dados do Access.|  
|**QueriesCount**|**int**|O número de consultas no banco de dados do Access.|  
|**FormsCount**|**int**|O número de formulários no banco de dados do Access.|  
|**ModulesCount**|**int**|O número de módulos no banco de dados do Access.|  
|**ReportsCount**|**int**|O número de relatórios no banco de dados do Access.|  
|**MacrosCount**|**int**|O número de macros no banco de dados do Access.|  
|**AccessVersion**|**nvarchar(4000)**|A versão de acesso do banco de dados.|  
|**Ordenação**|**nvarchar(4000)**|O agrupamento do banco de dados do Access. Agrupamentos determinam como um banco de dados classifica e compara Cadeias de caracteres.|  
|**JetVersion**|**nvarchar(4000)**|A versão do mecanismo de banco de dados Jet. Bancos de dados do Access usam o mecanismo de banco de dados Jet subjacente.|  
|**Isatualizável**|**bit**|Indica se o banco de dados pode ser atualizado. Se o valor for 1, o banco de dados será atualizável. Se o valor for 0, o banco de dados será somente leitura.|  
|**QueryTimeout**|**int**|O valor de tempo limite de consulta ODBC configurado para o banco de dados, em segundos. O padrão é 60 segundos.|  
  
## <a name="tables"></a>Tabelas  
Os metadados de tabela são exportados para a tabela de **SSMA_Access_InventoryTables** . Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém esta tabela.|  
|**TableId**|**uniqueidentifier**|Um GUID que identifica exclusivamente a tabela. Essa coluna também é a chave primária para a tabela.|  
|**TableName**|**nvarchar(4000)**|O nome da tabela.|  
|**RowsCount**|**int**|O número de linhas da tabela.|  
|**ValidationRule**|**nvarchar(4000)**|A regra que define a entrada válida para a tabela. Se nenhuma regra de validação existir, o campo conterá uma cadeia de caracteres vazia.|  
|**Vinculadotable**|**nvarchar(4000)**|Outra tabela, se houver, que está vinculada à tabela. A vinculação de tabelas permite adições, exclusões e atualizações à outra tabela usando essa tabela.|  
|**ExternalSource**|**nvarchar(4000)**|A fonte de dados, se houver, associada à tabela. Se uma tabela estiver vinculada, ela terá uma fonte de dados externa especificada nesse campo.|  
  
## <a name="columns"></a>Colunas  
Os metadados de coluna são exportados para a tabela de **SSMA_Access_InventoryColumns** . Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém esta coluna.|  
|**TableId**|**uniqueidentifier**|Identifica a tabela que contém esta coluna.|  
|**ColumnId**|**int**|Um inteiro de incremento que identifica a coluna. **Columnid** é a chave primária para a tabela.|  
|**ColumnName**|**nvarchar(4000)**|O nome da coluna.|  
|**IsNullable**|**bit**|Especifica se a coluna pode conter valores nulos. Se o valor for 1, a coluna poderá conter valores nulos. Se o valor for 0, a coluna não poderá conter valores nulos. Observe que a regra de validação também pode ser usada para evitar valores nulos.|  
|**DataType**|**nvarchar(4000)**|O tipo de dados de acesso da coluna, como **texto** ou **longo**.|  
|**IsAutoIncrement**|**bit**|Especifica se a coluna incrementa automaticamente valores inteiros. Se o valor for 1, os inteiros serão incrementados automaticamente.|  
|**Numera**|**smallint**|A ordem da coluna na tabela, começando em zero.|  
|**DefaultValue**|**nvarchar(4000)**|O valor padrão da coluna.|  
|**ValidationRule**|**nvarchar(4000)**|A regra usada para validar os dados adicionados ou atualizados na coluna.|  
  
## <a name="indexes"></a>Índices  
Os metadados do índice são exportados para a tabela de **SSMA_Access_InventoryIndexes** . Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém este índice.|  
|**TableId**|**uniqueidentifier**|Identifica a tabela que contém este índice.|  
|**IndexId**|**int**|Um inteiro de incremento que identifica o índice. Esta coluna é a chave primária para a tabela.|  
|**IndexName**|**nvarchar(4000)**|O nome do índice.|  
|**ColumnsIncluded**|**nvarchar(4000)**|Lista as colunas que estão incluídas no índice. Os nomes de coluna são separados por ponto e vírgula.|  
|**IsUnique**|**bit**|Especifica se cada item no índice deve ser exclusivo. Em um índice de várias colunas, a combinação de valores deve ser exclusiva. Se o valor for 1, o índice aplicará valores exclusivos.|  
|**IsPK**|**bit**|Especifica se o índice foi criado automaticamente como parte da definição da chave primária.|  
|**IsClustered**|**bit**|Especifica se o índice está clusterizado. Um índice clusterizado reordena o armazenamento físico dos dados. Uma tabela pode ter apenas um índice clusterizado.|  
  
## <a name="foreign-keys"></a>Chaves estrangeiras  
Os metadados de chave estrangeira são exportados para a tabela de **SSMA_Access_InventoryForeignKeys** . Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém essa chave estrangeira.|  
|**TableId**|**uniqueidentifier**|Identifica a tabela que contém essa chave estrangeira.|  
|**ForeignKeyId**|**int**|Um inteiro de incremento que identifica a chave estrangeira. Esta coluna é a chave primária para a tabela.|  
|**ForeignKeyName**|**nvarchar(4000)**|O nome do índice.|  
|**ReferencedTableId**|**uniqueidentifier**|Identifica a tabela que contém as colunas de origem.|  
|**SourceColumns**|**nvarchar(4000)**|Lista a coluna de chave estrangeira ou colunas.|  
|**ReferencedColumns**|**nvarchar(4000)**|Lista a coluna de chave primária ou as colunas que são referenciadas pela chave estrangeira.|  
|**IsCascadeForUpdate**|**bit**|Especifica que, se o valor da chave primária for atualizado, todas as linhas que fazem referência a esse valor de chave também serão atualizadas.|  
|**IsCascadeForDelete**|**bit**|Especifica que, se o valor da chave primária for excluído, todas as linhas que fazem referência a esse valor de chave também serão excluídas.|  
|**Isimpord**|**bit**|Especifica que a restrição de chave estrangeira é imposta.|  
  
## <a name="queries"></a>Consultas  
Os metadados de consulta são exportados para a tabela de **SSMA_Access_InventoryQueries** . Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém essa consulta.|  
|**QueryId**|**int**|Um inteiro de incremento que identifica a consulta. Esta coluna é a chave primária para a tabela.|  
|**QueryName**|**nvarchar(4000)**|O nome da consulta.|  
|**QueryText**|**nvarchar(4000)**|O código de consulta SQL, como uma instrução SELECT.|  
|**Isatualizável**|**bit**|Especifica se a consulta é atualizável ou somente leitura.|  
|**QueryType**|**nvarchar(4000)**|Especifica o tipo de consulta, como **Select** ou **setoperation**.|  
|**ExternalSource**|**nvarchar(4000)**|Se a consulta fizer referência a uma fonte de dados externa, essa será a cadeia de conexão usada pela consulta.|  
  
## <a name="forms"></a>Formulários  
Os metadados de formulário são exportados para a tabela de **SSMA_Access_InventoryForms** . Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém este formulário.|  
|**FormId**|**int**|Um inteiro de incremento que identifica o formulário. Esta coluna é a chave primária para a tabela.|  
|**Tipo de formulário**|**nvarchar(4000)**|O nome do formulário.|  
  
## <a name="macros"></a>Macros  
Os metadados de macro são exportados para a tabela de **SSMA_Access_InventoryMacros** . Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém a macro.|  
|**Macroid**|**int**|Um inteiro de incremento que identifica a macro. Esta coluna é a chave primária para a tabela.|  
|**Nomedamacro**|**nvarchar(4000)**|O nome da macro.|  
  
## <a name="reports"></a>Relatórios  
Os metadados do relatório são exportados para a tabela de **SSMA_Access_InventoryReports** . Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém o relatório.|  
|**ReportId**|**int**|Um inteiro de incremento que identifica o relatório. Esta coluna é a chave primária para a tabela.|  
|**ReportName**|**nvarchar(4000)**|O nome do relatório.|  
  
## <a name="modules"></a>Módulos  
Os metadados do módulo são exportados para a tabela **SSMA_Access_InventoryModules** . Esta tabela contém as seguintes colunas:  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica o banco de dados que contém o módulo.|  
|**ModuleId**|**int**|Um inteiro de incremento que identifica o módulo. Esta coluna é a chave primária para a tabela.|  
|**ModuleName**|**nvarchar(4000)**|O nome do módulo.|  
  
## <a name="see-also"></a>Consulte Também  
[Exportar um inventário do Access](exporting-an-access-inventory-accesstosql.md)  
  
